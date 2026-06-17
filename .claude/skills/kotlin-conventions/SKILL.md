---
name: kotlin-conventions
description: "Kotlin style and convention rules for the mobile team. Load when reviewing Kotlin code — any .kt file in a diff."
---

## Rules

1. **Naming** `[LOW]` — Classes are UpperCamelCase; functions and properties are
   lowerCamelCase; compile-time constants are SCREAMING_SNAKE_CASE. A mutable property named
   `API_KEY` is both a naming smell and a security smell. Booleans read as `is`/`has`/`can`.
2. **Coroutines** `[MEDIUM]` — Launch coroutines from a structured scope: `viewModelScope`
   in a `ViewModel`, `lifecycleScope` in UI. `GlobalScope.launch` is a violation — it leaks
   work that outlives the screen and ignores cancellation.
3. **Jetpack / lifecycle** `[MEDIUM]` — Screen state is exposed from a `ViewModel` as
   `StateFlow` (or `LiveData`). Views observe state; they do not perform data access. Don't
   hold `Context`/`View` references in a `ViewModel`.

Severity guidance: naming issues are `[LOW]`; coroutine-scope and lifecycle issues are
`[MEDIUM]`; a leaked secret surfaced here is `[HIGH]` (defer to the security review).

## Template

Compliant:

```kotlin
class TripViewModel(private val tripRepository: TripRepository) : ViewModel() {
    private val _trips = MutableStateFlow<List<Trip>>(emptyList())
    val trips: StateFlow<List<Trip>> = _trips
    fun loadTrips(userId: String) = viewModelScope.launch { _trips.value = tripRepository.recent(userId) }
}
```

Non-compliant:

```kotlin
class TripViewModel(private val apiClient: ApiClient) : ViewModel() {
    fun loadTrips(userId: String) = GlobalScope.launch {        // [MEDIUM] use viewModelScope
        _trips.value = apiClient.get("/users/$userId/trips")     // bypasses the repository
    }
}
```

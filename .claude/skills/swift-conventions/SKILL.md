---
name: swift-conventions
description: "Swift style and convention rules for the mobile team. Load when reviewing Swift code — any .swift file in a diff."
---

## Rules

1. **Naming** — Types are UpperCamelCase; functions, methods, and properties are
   lowerCamelCase. A function named `FetchProfile` is a violation; it should be
   `fetchProfile`. Booleans read as a question: `isLoading`, `hasSession`, `canRetry` — a
   bare `loading` is a violation. Avoid abbreviations and snake_case.
2. **Concurrency** — New asynchronous code uses `async/await`. Completion-handler APIs
   (`completion: @escaping (...) -> Void`) must not be added to new code. `Task { }` is fine;
   blocking the main actor is not.
3. **UIKit / SwiftUI** — New screens are built in SwiftUI with an `ObservableObject` view
   model exposing `@Published` state. Reaching for `UIKit` / `UIViewController` in a new
   screen without a stated reason is a violation.

## Template

Compliant:

```swift
@MainActor
final class ProfileViewModel: ObservableObject {
    @Published private(set) var isLoading = false
    func fetchProfile(id: String) async throws -> Profile { /* ... */ }
}
```

Non-compliant:

```swift
final class ProfileViewModel {            // not a SwiftUI ObservableObject
    var loading = false                   // boolean missing is/has/can
    func FetchProfile(id: String,         // should be lowerCamelCase
                      completion: @escaping (Profile?) -> Void) { /* ... */ }  // use async/await
}
```

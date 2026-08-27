# mqiu's UI Library

A polished set of UI components in different languages. Actively used in my apps.

## SwiftUI

### Modular Settings

[`SwiftUI/ModularSettings/ModularSettings.swift`](SwiftUI/ModularSettings/ModularSettings.swift)
is a macOS 13+ SwiftUI settings foundation for apps with multiple settings pages. It
provides:

- `ModularSettingsTab` for sidebar destinations.
- `ModularSettingsNavigationState` for searchable settings registration and scroll-to-row navigation.
- `ModularSettingsContainer` for padded, scrollable tab content.
- `ModularSettingsSection` and `ModularSettingsRow` for consistent grouped settings UI.
- `ModularSettingsInfoButton` and `ModularSettingsWarningButton` for contextual popovers.
- `modularSettingsHighlightedText` for highlighting search matches.

The file is intentionally self-contained and has no dependency on the source app's
models or services. Add it to a SwiftUI target, create one shared navigation state,
and inject it with `.environmentObject(...)`:

```swift
@StateObject private var navigationState = ModularSettingsNavigationState()

var body: some View {
    ModularSettingsContainer(accountTab) {
        ModularSettingsSection("Account") {
            ModularSettingsRow("Display name", helperText: "Shown to other users.") {
                TextField("Name", text: $name)
                    .frame(width: 180)
            }
        }
    }
    .environmentObject(navigationState)
}
```

Follow the repository's existing Swift style: four-space indentation, same-line
braces, `camelCase` symbols, narrow access control, and Conventional Commit messages.
Keep user-visible text localizable and preserve the macOS 13 deployment target unless
the consuming app has a deliberate reason to raise it.

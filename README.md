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
- `ModularSettingsRequirement` and `ModularSettingsRequirementWarning` for showing
  missing capabilities directly on affected rows.
- `ModularSettingsSliderRow` for resettable, animated numeric settings.
- `ModularSettingsShortcutRow` for reusable shortcut display, recording, and reset controls.
- `ModularSettingsReorderableList` for native macOS 27 reordering with a drag-and-drop fallback.
- `ModularSettingsPermissionStatusIcon` for consistent permission state indicators.
- `ModularSettingsAnimatedValue` and `withModularSettingsAnimation` for compact value transitions.
- `modularSettingsHighlightedText` for highlighting search matches.
- `ModularSettingsTabBar` for native, horizontally scrollable tab groups with
  centered tabs, progressive edge fades, and optional add/delete controls.

[`SwiftUI/ModularSettings/ModularSettingsPermissions.swift`](SwiftUI/ModularSettings/ModularSettingsPermissions.swift)
provides `ModularSettingsPermissionManager`, a reusable macOS TCC manager for
Accessibility, event synthesis, and Screen Recording permissions. It refreshes
while System Settings is open and can relaunch the current app after a permission
change. App-specific permissions and diagnostics should remain in the consuming app.

The components are intentionally self-contained and have no dependency on a source
app's models or services. Add the SwiftUI files to a macOS target, create one shared
navigation state, and inject it with `.environmentObject(...)`:

```swift
@StateObject private var navigationState = ModularSettingsNavigationState()
@StateObject private var permissionManager = ModularSettingsPermissionManager.shared

var body: some View {
    ModularSettingsContainer(accountTab) {
        ModularSettingsSection("Account") {
            ModularSettingsRow("Display name", helperText: "Shown to other users.") {
                TextField("Name", text: $name)
                    .frame(width: 180)
            }

            ModularSettingsRow(
                "Window automation",
                requirements: [
                    .accessibility(isGranted: permissionManager.hasAccessibilityPermission)
                ]
            ) {
                Button("Settings") {
                    permissionManager.requestAccessibilityPermission()
                }
            }
        }
    }
    .environmentObject(navigationState)
}
```

#### Tab bar template

`ModularSettingsTabBar` keeps a native `.tabs` picker on macOS 27 and a native
segmented picker on earlier macOS versions. It centers the picker while the
items fit, then enables horizontal scrolling and fades the clipped edges when
the tab group is wider than its available space. The add and delete controls
are optional and remain outside the scrolling region.

```swift
ModularSettingsTabBar(
    "Dock Set",
    items: dockSets,
    selection: $selectedDockSetID,
    onAdd: addDockSet,
    onDelete: deleteDockSet,
    canDelete: { _ in dockSets.count > 1 },
    accessibilityLabel: { $0.name }
) { dockSet in
    Text(dockSet.name)
}
```

The component is intentionally generic: the consuming app owns item identity,
selection state, labels, and destructive-action confirmation. Keep those
policies outside the reusable tab-bar template.

After a confirmed deletion, use `ModularSettingsTabBarSelection` to preserve
the current selection when deleting another tab, select the preceding tab when
deleting the selected tab, and fall back to the new first tab when deleting the
first one. It returns `nil` when no tabs remain. Compute the replacement from
the pre-deletion order, then remove the item and apply the returned selection.

Follow the repository's existing Swift style: four-space indentation, same-line
braces, `camelCase` symbols, narrow access control, and Conventional Commit messages.
Keep user-visible text localizable and preserve the macOS 13 deployment target unless
the consuming app has a deliberate reason to raise it.

## Web

### Editorial Portfolio Website

[`Web/EditorialPortfolio/main.css`](Web/EditorialPortfolio/main.css) is a reusable,
CSS-only foundation extracted from the shared styling system used by the mqiu.dev
portfolio and product websites. It includes responsive editorial layouts, light and
dark theme tokens, typography, glass surfaces, navigation, cards, hover treatments,
and animation hooks.

See [`Web/EditorialPortfolio/README.md`](Web/EditorialPortfolio/README.md) for usage
guidance and the intended boundary between the template and a consuming website.

### Zensical Documentation Site

[`Web/Zensical/`](Web/Zensical/) is a reusable Zensical configuration and theme
foundation extracted from the shared settings in the mqiu.dev blog and
DesktopRenamer documentation sites. It includes a placeholder project config,
light/dark palette setup, Markdown extensions, theme overrides, branded footer
override, and optional sheet-table and pan/zoom styles.

See [`Web/Zensical/README.md`](Web/Zensical/README.md) for setup instructions and
the boundary between reusable settings and site-specific content.

# SwiftUI Animation Tips

A few patterns I keep coming back to.

## Prefer `withAnimation` for state changes

Wrap the state change, not the view, when you need a one-off animation:

```swift
withAnimation(.snappy) {
    isExpanded.toggle()
}
```

## Use `animation(_:value:)` for conditional animations

Attach it to the view and give it a single value to watch:

```swift
Text(isExpanded ? "More" : "Less")
    .animation(.easeInOut(duration: 0.2), value: isExpanded)
```

## Keep transitions on the view

If a view appears/disappears, add a transition and pair it with `withAnimation`:

```swift
if isExpanded {
    DetailView()
        .transition(.move(edge: .bottom))
}
```

## Avoid animating layout jumps

Animate `frame`/`padding` changes only when needed; prefer `matchedGeometryEffect` for shared element motion.

## Check list

- [ ] Animation matches the gesture? Use `animation(.interactiveSpring(), value: dragAmount)`.
- [ ] Reduced motion respected? Wrap animations in `@Environment(\.accessibilityReduceMotion)` checks.

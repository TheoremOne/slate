# RangeRef API

`RangeRef` objects keep a specific range in a document synced over time as new operations are applied to the editor. You can access their property `current` at any time for the up-to-date `Range` value.
When you no longer need to track this location, call `unref()` to free the resources.

```typescript
interface RangeRef {
  current: Range | null
  affinity: 'forward' | 'backward' | 'outward' | 'inward' | null
  unref(): Range | null
}
```

For example:

```typescript
const selectionRef = Editor.rangeRef(editor, editor.selection, {
  affinity: 'inward',
})
// Allow the user to do stuff which might change the selection
Transforms.unwrapNodes(editor)
Transforms.select(editor, selectionRef.unRef())
```

- [Instance methods](range-ref.md#instance-methods)
- [Static methods](range-ref.md#static-methods)
  - [Transform methods](range-ref.md#transform-methods)

## Instance methods

#### `unRef() => Range`

Call this when you no longer need to sync this range.
It also returns the current value.

## Static methods

### Transform methods

#### `RangeRef.transform(ref: RangeRef, op: Operation)`

Transform the range refs current value by an `op`.
The editor calls this as needed, so normally you won't need to.

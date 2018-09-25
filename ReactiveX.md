## Reactive X

- ReactiveX operates on discrete values that are emitted over time.
- The ReactiveX Observable model allows you to treat streams of asynchronous events with the same sort of simple, composable operations that you use for collections of data items like arrays
- ReactiveX provides a collection of operators with which you can filter, select, transform, combine, and compose Observables. This allows for efficient execution and composition
- In ReactiveX an observer subscribes to an Observable. Then that observer reacts to whatever item or sequence of items the Observable emits. This pattern facilitates concurrent operations because it does not need to block while waiting for the Observable to emit objects, but instead it creates a sentry in the form of an observer that stands ready to react appropriately at whatever future time the Observable does so
- we can use mobX Devtools for debugging
- @computed values do not change our state/
- @observer produces a side-effect

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk2NTU2NzgxOF19
-->
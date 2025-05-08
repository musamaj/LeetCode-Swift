### 🔄 Concept
Undo Stack: Holds actions that can be undone.

Redo Stack: Holds actions that were undone and can be redone.

Every time a new action is performed, it's pushed to the undo stack, and the redo stack is cleared.

### ✅ Pseudo-code Implementation
```swift
class UndoManager<T> {
    
    private var undoStack: [(T) -> Void] = []
    private var redoStack: [(T) -> Void] = []
    private var state: T

    init(initialState: T) {
        self.state = initialState
    }

    func perform(action: @escaping (inout T) -> Void) {
        // Save current state before changing
        let previousState = state

        // Apply the action
        action(&state)

        // Push undo action (to revert to previous state)
        undoStack.append { _ in
            self.state = previousState
        }

        // Clear redo stack as new action breaks the redo chain
        redoStack.removeAll()
    }

    func undo() {
        guard let lastUndo = undoStack.popLast() else { return }
        
        let currentState = state
        lastUndo(state) // Undo

        // Push redo action (to redo to the state we just undid from)
        redoStack.append { _ in
            self.state = currentState
        }
    }

    func redo() {
        guard let lastRedo = redoStack.popLast() else { return }

        let currentState = state
        lastRedo(state) // Redo

        // Push back to undo stack
        undoStack.append { _ in
            self.state = currentState
        }
    }

    func getState() -> T {
        return state
    }
}
```

### 🧠 Key Notes (Good for Interview)
This models UIUndoManager conceptually, though UIUndoManager uses NSInvocation-style actions.

You could enhance this by:

Giving actions labels (for UI).

Making it generic over command types (Command Pattern).

Limiting stack size to save memory.

Works well for value types (struct) as state.

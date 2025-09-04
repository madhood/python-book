## Your Digital Assistant: Console To-Do List

**Task:** Develop a command-line to-do list application. This program will enable users to add, view, toggle the completion status, remove tasks, and perform `undo` and `redo` operations on their actions. The core state management must strictly adhere to the **reducer pattern** with a functional programming style, emphasizing pure functions and isolation of side effects.

**Key Features:**

*   **Add Task:** Add a new task to the list.
*   **Remove Task:** Delete a specific task by its number.
*   **Toggle Mark:** Change a task's completion status (undone `[ ]` ↔ done `[✓]`).
*   **View Tasks:** Display all tasks.
*   **Undo:** Revert the last state-changing action.
*   **Redo:** Reapply a previously undone action.

**Inputs & Outputs:**

*   **Command Prompt:** Always use `>` for user input.
*   **Command formating** Command should by in the format of command type then argument ex. `add` my first task 
*   **Output after Modification:** The full task list should be displayed immediately after any `add`, `toggle`, `remove`, `undo`, or `redo` operation.
*   **Completed Task Mark:** Use `[✓]` for completed tasks and `[ ]` for incomplete tasks.

**Example Interaction:**

```
Welcome to your To-Do List!
> add Learn Reducer Pattern
1. [ ] Learn Reducer Pattern
> add Build ToDo App
1. [ ] Learn Reducer Pattern
2. [ ] Build ToDo App
> view
1. [ ] Learn Reducer Pattern
2. [ ] Build ToDo App
> toggle 1
1. [✓] Learn Reducer Pattern
2. [ ] Build ToDo App
> undo
1. [ ] Learn Reducer Pattern
2. [ ] Build ToDo App
> redo
1. [✓] Learn Reducer Pattern
2. [ ] Build ToDo App
> remove 2
1. [✓] Learn Reducer Pattern
> exit
Goodbye!
```

**Technical Requirements:**

1.  **State Structure:**
    *   `tasks`: A list of dictionaries. Each task dictionary: `{'text': '...', 'completed': False/True}`.
    *   `commands_history`: A list of all user commands executed.  
    *   `history_index`: An integer used to manage `undo` and `redo` operations. 

2.  **Reducer Pattern for State Evolution:**
    *   Create a `reducer(current_state, command)` function.
    *   It must be a **pure function**: no side effects, always returns a *new* state object.
    *   you cn refer to the following code snippet from the lecture:
```python
from functools import reduce

initial_state = 0
# inc, dec, reset, set, undo, redo
command_history = [
    {'type': 'inc'},
    {'type': 'inc'},
    {'type': 'inc'},
    {'type': 'inc'},
    {'type': 'inc'},
    {'type': 'dec'},
    {'type': 'reset'},
    {'type': 'set', 'value': 10},
    {'type': 'inc'},
    {'type': 'inc'},
    {'type': 'inc'},
    {'type': 'inc'},
    {'type': 'dec'}
]
index = 7


def reducer(current_state, command):
    if command['type'] == 'inc':
        return current_state + 1
    if command['type'] == 'dec':
        return current_state - 1
    if command['type'] == 'reset':
        return 0
    if command['type'] == 'set':
        return command['value']

final_state = reduce(reducer, command_history[:index], initial_state)
print(final_state)
```
3.  **Follow function programming style:**
    *   Most of the functions should be **pure**.
    *   Isolate side effects.

**Bonus Challenge: Test-Driven Development (TDD)**

Implement your application's core logic using TDD.

**TDD Code Snippet (for your `if __name__ == '__main__':` block):**

```python
def add(a, b):
    return a + b

if __name__ == '__main__':
    tests = [
        {'func': add, 'args': (0, 0), 'expected': 0},
        {'func': add, 'args': (1, 2), 'expected': 3},
        {'func': add, 'args': (-1, -2), 'expected': -3},
        {'func': add, 'args': (0, -1), 'expected': -1},
    ]
    for test in tests:
        assert test['func'](*test['args']) == test['expected'], f'{test['func'].__name__} with args {test["args"]} expected {test["expected"]} but got {test['func'](*test['args'])}'
```
---
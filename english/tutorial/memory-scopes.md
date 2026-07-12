---
icon: database
---

# Memory scopes

A variable's scope controls where it can be read and how long it exists. SER has local, global, and ephemeral variables.

## Local variables

Assignments are local by default:

```ser
$message = "Hello"
@targets = @all
```

Local variables belong to the current script execution and disappear when that execution finishes. Two scripts can have local variables with the same name without affecting each other.

Use local variables for almost everything unless another scope solves a specific problem.

## Global variables

Global variables can be shared by scripts during the round:

```ser
global $eventEnabled = true
global $eventScore = 0
```

Read a global variable normally:

```ser
if $eventEnabled is true
    Print "The event is enabled."
end
```

Use `global` every time you create or change it:

```ser
global $eventScore = $eventScore + 1
```

Without `global`, the assignment creates or updates a local variable with the same name instead.

Check before reading a global that may not have been created:

```ser
if {VarExists $eventScore} is false
    global $eventScore = 0
end
```

## Ephemeral variables

`ephm` creates temporary variables for short-lived work, especially inside functions:

```ser
func $BuildWelcome with @player
    ephm $name = @player -> name
    return "Welcome {$name}!"
end
```

An ephemeral variable is intended for the current function or statement context and is discarded with that context. It prevents helper variables from leaking into the surrounding script.

## Delete variables

Use `delete` when a variable should stop existing before its normal scope ends:

```ser
global $temporaryEventState = "active"

# Later, when the system is finished:
delete $temporaryEventState
```

After deletion, `VarExists` returns `false`.

## Inspect global state

`GlobalVariables` returns the names of all global variables:

```ser
&globalNames = GlobalVariables

over &globalNames with $name
    Print $name
end
```

This is useful while debugging namespace collisions.

## Choosing a scope

| Scope | Use it when |
|---|---|
| Local | Only the current script execution needs the value |
| Global | Multiple scripts must share round state |
| Ephemeral | A helper value is needed only inside a function or statement |

Prefer local variables. Global state makes scripts depend on execution order, so initialize it from a predictable event such as `WaitingForPlayers` or `RoundStarted`.

### What's next?

Continue with [Functions](functions.md) to organize reusable logic.

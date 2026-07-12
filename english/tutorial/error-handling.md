---
icon: triangle-exclamation
---

# Error handling

SER normally stops a script when an instruction throws a runtime error. Use validation to prevent expected problems and `attempt`/`on_error` when an operation may still fail.

## Prevent errors first

Check player counts before using a property that requires exactly one player:

```ser
@target = Take @alivePlayers 1

if {AmountOf @target} isnt 1
    Print "No target was found."
    stop
end

Print {@target -> name}
```

Validate references:

```ser
*room = GetRoomByName "LczToilets"

if {*room -> isInvalid}
    Print "The room could not be found."
    stop
end
```

Check optional variables:

```ser
if {VarExists @evAttacker} is false
    stop
end
```

These checks are clearer than catching an error after it happens.

## The `attempt` statement

`attempt` prevents an error inside its body from terminating the whole script:

```ser
&values = Coll.Create

attempt
    Print {Coll.Fetch &values 2}
end

Print "The script continues."
```

When an error occurs, the remaining instructions inside `attempt` are skipped.

## Handle the error

Add `on_error` before the shared `end`:

```ser
&values = Coll.Create

attempt
    Print {Coll.Fetch &values 2}
on_error with $message $type $stackTrace
    Error "Could not fetch the value: {$message}"
end
```

The variables are:

- `$message`: readable error information;
- `$type`: the exception type;
- `$stackTrace`: internal diagnostic details, mainly useful for developers.

Usually, log `$message` and add context describing what the script was trying to do.

## Keep attempts small

Avoid wrapping an entire script in one `attempt`. A small block makes it obvious which operation failed:

```ser
attempt
    *config = Config.Read "my_event"
on_error with $message
    Error "Could not read my_event config: {$message}"
    stop
end
```

## When to stop

Use `stop` when continuing would produce incorrect behavior. If the failed action is optional, log it and continue after the block.

For cancellable events, `IsAllowed false` changes the game event; `stop` independently controls whether the SER script executes later instructions.

### What's next?

Continue with [Debugging scripts](debugging.md) for a repeatable troubleshooting workflow.

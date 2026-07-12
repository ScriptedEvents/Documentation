---
icon: bug
---

# Debugging scripts

When a script fails, reduce the problem to one instruction and check what SER expected. Guessing method names or argument order is slower than using `serhelp`.

## Start with the server error

Run the script from the server console while developing:

```text
serrun myScript
```

Read the first SER error. Later errors are often consequences of the first one.

## Inspect a method

```text
serhelp Broadcast
serhelp Take
serhelp CRole.Register
```

The output tells you:

- whether the method returns a value;
- which variable prefix stores that value;
- argument order and accepted types;
- optional arguments and defaults;
- custom errors defined by the method.

Use `_` to keep an optional argument's default when a later argument is needed.

## Discover available symbols

```text
serhelp methods
serhelp variables
serhelp keywords
serhelp flags
serhelp events
serhelp enums
serhelp properties
```

Use a specific name after discovering it:

```text
serhelp ProcessingPlayer
serhelp RoleTypeId
serhelp properties player
```

## Print intermediate values

`Print` writes to the server console:

```ser
$count = AmountOf @alivePlayers
Print "Alive players: {$count}"
```

`LogVar` formats any existing variable for diagnostics:

```ser
Print {LogVar @alivePlayers}
```

Add temporary prints before and after the suspected instruction to see how far execution gets.

## Check assumptions

```ser
if {VarExists $score}
    Print "Score exists: {$score}"
else
    Print "Score was not initialized."
end
```

For player values, check `AmountOf`. For references, check `isInvalid`. For collections, check `length` before fetching.

## Isolate the smallest reproduction

Create a utility script containing only the failing method:

```ser
@target = Take @all 1
Print {LogVar @target}
```

If the small script works, the issue is probably earlier state, event data, or a variable overwritten elsewhere.

## Reload changed flagged scripts

Utility scripts run with `serrun`. Flagged scripts are loaded and bound to commands or events; after editing them on a live server, reload SER using the command supported by your installation.

Check the server console after reload so registration errors are not missed.

## A useful checklist

1. Is the method or event name present in `serhelp`?
2. Does capitalization match exactly?
3. Are text values with spaces quoted?
4. Does each variable use the correct prefix?
5. Does the method receive the documented argument types and order?
6. Does a player property receive exactly one player?
7. Was a reference checked with `isInvalid`?
8. Can an event variable be absent?
9. Does every `if`, loop, function, and attempt have the correct `end`?
10. Does every `forever` loop yield with `wait` or `wait_until`?

### What's next?

Continue with [Script flags](script-flags.md) to run scripts from commands and events.

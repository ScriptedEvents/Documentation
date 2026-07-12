---
icon: flag
---

# Script flags

A utility script runs only when someone calls it with `serrun` or another script starts it. A flag binds a script to a command, game event, custom-role event, or custom trigger.

A script can have one flag. Put it at the top of the file before executable instructions.

Use `serhelp flags` to list available flags and `serhelp FlagName` to inspect one.

## Custom commands

`CustomCommand` creates a command that executes the script:

```ser
!-- CustomCommand healme
-- availableFor Player RemoteAdmin
-- description "Heals the command sender."
-- cooldown 30s

Heal @sender
Reply "You have been healed."
```

The inline value after `CustomCommand` is the command name.

`@sender` is injected when a player runs the command. It is not available when the server console runs the command, so do not enable `Server` for scripts that require `@sender`.

### Command arguments

Declare arguments with `-- arguments`:

```ser
!-- CustomCommand announce
-- availableFor Player RemoteAdmin
-- arguments message
-- cooldown 1m

Broadcast @all 8s $message
```

Each command argument becomes a local literal variable. Here, `message` creates `$message`.

Add `?` to make an argument optional:

```ser
!-- CustomCommand report
-- availableFor Player
-- arguments player reason?

if {VarExists $reason}
    Print "Report about {$player}: {$reason}"
else
    Print "Report about {$player}, no reason supplied."
end
```

The variable name does not include the `?`.

### Access and limits

Common options are:

| Option | Purpose |
|---|---|
| `-- availableFor Player RemoteAdmin Server` | Allowed consoles |
| `-- neededPermission command.use` | Any required RA permission |
| `-- neededRank admin moderator` | Any required rank |
| `-- cooldown 30s` | Per-player cooldown |
| `-- globalCooldown 10s` | Shared cooldown |
| `-- maxUses 2` | Per-player use limit |
| `-- globalMaxUses 10` | Shared use limit |

Each restriction has a corresponding custom-message option. Run `serhelp CustomCommand` for the complete list.

## Game events

`OnEvent` executes a script when a LabAPI event occurs:

```ser
!-- OnEvent Joined
-- require @evPlayer

Broadcast @evPlayer 8s "Welcome to the server!"
```

Find event names with:

```text
serhelp events
serhelp Joined
```

The specific event help shows:

- whether the event is cancellable;
- which variables it injects;
- the type of each injected value.

### Required event variables

`-- require` skips the script unless all listed variables are available:

```ser
!-- OnEvent Hurt
-- require @evPlayer @evAttacker *evDamageHandler

Hint @evAttacker 1s "Hit {@evPlayer -> name} for {Round {*evDamageHandler -> damage}} HP"
```

Use it when the script cannot do useful work without those values. If absence is a case you want to handle, omit that variable from `-- require` and check it with `VarExists`.

### Cancel an event

Only events reported as cancellable by `serhelp EventName` can be cancelled:

```ser
!-- OnEvent Dying
-- require @evPlayer

if {@evPlayer -> role} is "Tutorial"
    IsAllowed false
    stop
end
```

`IsAllowed false` cancels the game event. `stop` independently prevents later SER instructions from running.

## Custom-role events

`OnCRole` listens for custom roles being assigned or removed:

```ser
!-- OnCRole spawned
-- forRoles janitor senior_guard

Broadcast @evPlayer 5s "Custom role: {*evCRole -> displayName}"
```

The inline event is `spawned` or `removed`. The optional `-- forRoles` list limits which role IDs trigger the script. The flag injects `@evPlayer` and `*evCRole`.

See [Custom roles with CRole](custom-roles.md) for registration and spawn systems.

## Custom triggers

`OnCustomTrigger` lets scripts communicate without sharing a game event.

Listener:

```ser
!-- OnCustomTrigger evacuation

Broadcast @all 8s "Evacuation has started."
```

Caller:

```ser
!-- CustomCommand evacuate
-- availableFor RemoteAdmin

Trigger evacuation
```

Every script bound to the same trigger name executes when `Trigger` is called.

## Interactable Toy events

This flag works with interactable toys created by SER:

```ser
!-- InteractableToyEvent

Broadcast @evPlayer 5s "You interacted with a toy."
Hint @evPlayer 3s "Interaction duration: {*evToy -> interactionDuration}s"
```

It injects `@evPlayer` and `*evToy`.

## Legacy function scripts

The `Function` flag makes a separate script require specific variables:

```ser
!-- Function
-- argument $message
-- argument @target

Broadcast @target 5s $message
```

It is called with the `RunFunc` method. This is different from an inline `func` definition.

Use inline [Functions](functions.md) for new logic contained in one script. Keep function scripts only when compatibility or cross-file reuse requires them.

## Reloading flagged scripts

Flags register commands and event handlers. After changing a flagged script on a live server, reload SER so the binding is rebuilt. Check the server console for duplicate command names, invalid events, or missing arguments.

## Quick reference

| Flag | Runs when |
|---|---|
| `CustomCommand` | Its registered command is used |
| `OnEvent` | A LabAPI event fires |
| `OnCRole` | A custom role is assigned or removed |
| `OnCustomTrigger` | `Trigger` fires a matching name |
| `InteractableToyEvent` | A SER interactable is used |
| `Function` | `RunFunc` calls the function script |

### What's next?

Continue with [Custom roles](custom-roles.md) or one of the practical projects.

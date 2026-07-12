---
icon: flag
metaLinks:
  alternates:
    - /broken/spaces/cuMKPytdZ4h8yad4Mib4/pages/WNqab5g1vTxtwnC9eBhv
---

# Script Flags

{% hint style="warning" %}
This is an archived draft kept for reference. New readers should use the current [Script flags](script-flags.md) tutorial.
{% endhint %}

Scripts don't always have to be run by an admin! **Flags** allow you to change how a given script executes — whether that be a custom command, a base game event, or a custom trigger.

{% hint style="info" %}
A script can only have **one** flag. If you need multiple entry points, create separate scripts and have them call each other.
{% endhint %}

---

## Where to find valid flags?

Using the `serhelp flags` command will give you a list of all available flags.

```
> CustomCommand
> Function
> InteractableToyEvent
> OnCRole
> OnCustomTrigger
> OnEvent
```

{% hint style="info" %}
## serhelp flags

```
Flags are a way to change script behavior depending on your needs.

This how they are used:
!-- SomeFlag argValue1 argValue2
-- customFlagArgument "some value"

Flags should be used at the top of the script.

Below is a list of all flags available in SER:
(for more info about their usage, use 'serhelp flagName')
> CustomCommand
> Function
> InteractableToyEvent
> OnCRole
> OnCustomTrigger
> OnEvent
```
{% endhint %}

---

## How to use a flag?

Let's use the `CustomCommand` flag as an example. Running `serhelp CustomCommand` provides documentation like this:

```
===== CustomCommand =====
> Creates a command and binds it to the script. When the command is ran, it executes the script.

Usage:
!-- CustomCommand ...
-- arguments ...
-- availableFor ...
-- description ...

Arguments:
  Inline argument 'command name':
  > The name of the command to create

  Additional argument 'arguments':
  > The arguments that this command expects in order to run.
  > When the command is ran, the provided values become local literal variables.
  > For example: an argument 'name' creates a local variable $name in your script.
  > Side note: when a player runs the command, a @sender local variable is also created.

  Additional argument 'availableFor':
  > Specifies from which console the command can be executed.
  > Accepts ConsoleType enum values.

  Additional argument 'description':
  > The description of the command.
```

{% hint style="info" %}
## serhelp CustomCommand

```
===== CustomCommand =====
Creates a command and binds it to the script. When the command is ran, it executes the script.

Injects the following variables into the script:
> @sender (the player who ran the command, NOT added when command is ran by the server console)
> *command (reference to this 'CustomCommand', used for resetting cooldown)

Usage:
!-- CustomCommand ...
-- availableFor ...
-- description ...
-- neededPermission ...
-- noPermissionMessage ...
-- neededRank ...
-- invalidRankMessage ...
-- cooldown ...
-- onCooldownMessage ...
-- globalCooldown ...
-- onGlobalCooldownMessage ...
-- maxUses ...
-- onMaxUsesMessage ...
-- globalMaxUses ...
-- onGlobalMaxUsesMessage ...
-- arguments ...

+++ Arguments +++
> Required inline argument 'command name':
The name of the command to create
> Example usage
!-- CustomCommand myban

> Optional argument 'availableFor':
Specifies from which console the command can be executed from. Accepts: Player or RemoteAdmin or Server
> Example usage
-- availableFor Player RemoteAdmin

> Optional argument 'description':
The description of the command.
> Example usage
-- description "Used to ban a player"

> Optional argument 'neededPermission':
The permission that the player has to have in order to be able to use this command.
You can provide multiple permissions, and if the player has any of the listed permissions, they will be able to use the command.
> Example usage
-- neededPermission ban.use ban.bypass

> Optional argument 'noPermissionMessage':
Defines a message for when the sender does not have the needed permission (defined in 'neededPermission' argument).
> Example usage
-- noPermissionMessage "You do not have the required permissions to ban a player!"

> Optional argument 'neededRank':
The required remote admin rank in order to have access to this command.
You can provide multiple ranks, and if the player has any of the listed ranks, they will be able to use the command.
> Example usage
-- neededRank owner admin moderator staff

> Optional argument 'invalidRankMessage':
Defines a message for when the sender does not have the needed rank (defined in 'neededRank' argument).
> Example usage
-- invalidRankMessage "You are not server staff!"

> Optional argument 'cooldown':
The time the player has to wait before being able to use the command again.
> Example usage
-- cooldown 30s

> Optional argument 'onCooldownMessage':
Defines a message for when the player tries to run a command but is on cooldown.
Additionally, you can use %time% in the message to show the remaining time (in seconds) the player has to wait before being able to use this command again.
> Example usage
-- onCooldownMessage "You are on cooldown! You can use this command in %time% seconds."

> Optional argument 'globalCooldown':
The time all players have to wait before being able to use the command again.
If anyone uses a command, everyone else will be unable to use it for the specified duration.
This also applies to the server console.
> Example usage
-- globalCooldown 30s

> Optional argument 'onGlobalCooldownMessage':
Defines a message for when someone tries to run a command but is on global cooldown.
Additionally, you can use %time% in the message to show the remaining time (in seconds) someone has to wait before being able to use this command.
> Example usage
-- onGlobalCooldownMessage "This command is on cooldown! You can use this command in %time% seconds"

> Optional argument 'maxUses':
The maximum number of times a player can use this command.
> Example usage
-- maxUses 5

> Optional argument 'onMaxUsesMessage':
Defines a message for when the player tries to run a command but has reached their maximum usage limit.
> Example usage
-- onMaxUsesMessage "You have already used this command 5 times!"

> Optional argument 'globalMaxUses':
The maximum number of times this command can be used globally.
> Example usage
-- globalMaxUses 10

> Optional argument 'onGlobalMaxUsesMessage':
Defines a message for when the command has reached its global usage limit.
> Example usage
-- onGlobalMaxUsesMessage "This command has reached its global usage limit!"

> Optional argument 'arguments':
The arguments that this command expects in order to run.
The script cannot run unless every single argument is specified.

When the command is ran, the provided values for the arguments turn into their own literal local variables for you to use in the script.
For example: making a command with an argument 'name' will then create a local variable '$name' in your script.

If you want some arguments to be optional, you can use the '?' symbol after the argument name.
For example: 'reason?' argument will be optional, and if the sender does not provide a value for it, the script will still run.
Then, the '$reason' command will not be created in your script.

(the '?' suffix is NOT added to the variable names)
> Example usage
-- arguments id time reason?
```
{% endhint %}

That's a lot to go through! But don't worry — it's not as scary as it seems.

---

### Declaring a flag

```ser
!-- CustomCommand hi
```

`!-- CustomCommand` is the flag itself. It **must** be placed at the very top of the script. This defines which flag we are using.

### Inline argument

After `!-- CustomCommand` you can see `...` — this symbolizes that we need to put something there. This is the **inline argument** of that flag.

In this case, the inline argument is the **command name**. Let's create a command called "hi":

```ser
!-- CustomCommand hi
```

### Additional arguments

All of these are optional arguments that we can add below the flag:

```ser
-- arguments ...
-- availableFor ...
-- description ...
```

> Flag arguments don't have to be in the same order as shown, but they do need to be below the flag itself.

Let's add the `arguments` first! This lets us pass information into the script when the command is run.

```ser
!-- CustomCommand hi
-- arguments name
```

Thanks to this, when someone runs `/hi John`, a local variable `$name` will be created with the value `"John"`. We can use it directly:

```ser
!-- CustomCommand hi
-- arguments name
-- availableFor Player RemoteAdmin Server
-- description "Says hi!"

Reply "Hi, I'm Cheese! Let me guess, your name is:"
Reply $name
```

{% hint style="info" %}
When a command has an `arguments` flag, the values provided by the player become local literal variables. In this case, running `/hi John` creates `$name = "John"`.
{% endhint %}

Let's specify the `availableFor` argument next. This argument accepts the `ConsoleType` enum values:

```
Enum ConsoleType has the following values:
> None
> Player
> RemoteAdmin
> Server
```

{% hint style="info" %}
## serhelp ConsoleType

```
Enum ConsoleType has the following values:
> None
> Player
> RemoteAdmin
> Server
```
{% endhint %}

We want our command to work everywhere, so we provide all 3 options:

```ser
!-- CustomCommand hi
-- arguments name
-- availableFor Player RemoteAdmin Server
-- description "Says hi!"

Reply "Hi, I'm Cheese! Let me guess, your name is:"
Reply $name
```

And that's it! We have the entire flag set up.

---

## OnEvent Flag

The `OnEvent` flag binds a script to an in-game event. When that event occurs, the script automatically executes.

**Usage:**
```ser
!-- OnEvent EventName
-- require @evPlayer
```

**Example:**
```ser
!-- OnEvent RoundStarted

Broadcast @all 5s "A new round has started!"
```

When the round starts, all players will see the broadcast message.

### Available Events

To see all available events, use the `serhelp events` command. Some common events include:
- `RoundStarted` — When a round begins
- `RoundEnded` — When a round ends
- `Dying` — When a player is about to die
- `Death` — When a player has died
- `Joined` — When a player joins the server
- `Left` — When a player leaves the server

{% hint style="info" %}
## serhelp events

```
Event is a signal that something happened on the server.
If the round has started, server will invoke an event (signal) called RoundStarted.
You can use this functionality to run your scripts when a certain event happens.

By putting `!-- OnEvent RoundStarted` at the top of your script, you will run your script when the round starts.
You can put something different there, e.g. `!-- OnEvent Death`, which will run when someone has died.

Some events have additional information attached to them in a form of variables.
If you wish to know what variables are available for a given event, just use 'serhelp <eventName>'!

Here are all events that SER can use:
--- ObjectiveEvents ---
Completing, Completed, KillingEnemyCompleting, KilledEnemyCompleted, EscapingCompleting, EscapedCompleted, ActivatingGeneratorCompleting, ActivatedGeneratorCompleted, DamagingScpCompleting, DamagedScpCompleted, PickingScpItemCompleting, PickedScpItemCompleted
--- PlayerEvents ---
Joined, Left, ReceivingVoiceMessage, SendingVoiceMessage, PreAuthenticating, PreAuthenticated, UsingIntercom, UsedIntercom, Banning, Banned, Kicking, Kicked, Muting, Muted, Unmuting, Unmuted, ReportingCheater, ReportedCheater, ReportingPlayer, ReportedPlayer, TogglingNoclip, ToggledNoclip, RequestingRaPlayerList, RequestedRaPlayerList, RaPlayerListAddingPlayer, RaPlayerListAddedPlayer, RequestedCustomRaInfo, RequestingRaPlayersInfo, RequestedRaPlayersInfo, RequestingRaPlayerInfo, RequestedRaPlayerInfo, ChangingBadgeVisibility, ChangedBadgeVisibility, ChangingNickname, ChangedNickname, GroupChanging, GroupChanged, UpdatingEffect, UpdatedEffect, Dying, Death, Hurting, Hurt, ChangingRole, ChangedRole, Cuffing, Cuffed, Uncuffing, Uncuffed, ReceivingLoadout, ReceivedLoadout, Spawning, Spawned, ChangingItem, ChangedItem, DroppingAmmo, DroppedAmmo, DroppingItem, DroppedItem, PickingUpAmmo, PickedUpAmmo, PickingUpArmor, PickedUpArmor, PickingUpItem, PickedUpItem, PickingUpScp330, PickedUpScp330, SearchedAmmo, SearchingArmor, SearchedArmor, SearchingPickup, InteractedToy, SearchedPickup, SearchingAmmo, ThrowingItem, ThrewItem, ThrowingProjectile, ThrewProjectile, InspectingKeycard, InspectedKeycard, SpinningRevolver, SpinnedRevolver, ToggledDisruptorFiringMode, InspectingItem, InspectedItem, UsingItem, UsedItem, ItemUsageEffectsApplying, UsingRadio, UsedRadio, AimedWeapon, DryFiringWeapon, DryFiredWeapon, UnloadingWeapon, UnloadedWeapon, ReloadingWeapon, ReloadedWeapon, ShootingWeapon, ShotWeapon, ChangingAttachments, ChangedAttachments, SendingAttachmentsPrefs, SentAttachmentsPrefs, CancellingUsingItem, CancelledUsingItem, ChangingRadioRange, ChangedRadioRange, ProcessingJailbirdMessage, ProcessedJailbirdMessage, TogglingFlashlight, ToggledFlashlight, TogglingWeaponFlashlight, ToggledWeaponFlashlight, TogglingRadio, ToggledRadio, Jumped, MovementStateChanged, ProcessingScp1509Message, ProcessedScp1509Message, Scp1509Resurrecting, Scp1509Resurrected, DamagingShootingTarget, DamagedShootingTarget, DamagingWindow, DamagedWindow, EnteringPocketDimension, EnteredPocketDimension, LeavingPocketDimension, LeftPocketDimension, TriggeringTesla, TriggeredTesla, Escaping, Escaped, FlippingCoin, FlippedCoin, SearchingToy, SearchedToy, SearchToyAborted, IdlingTesla, IdledTesla, InteractingDoor, InteractedDoor, InteractingElevator, InteractedElevator, InteractingGenerator, InteractedGenerator, OpeningGenerator, OpenedGenerator, ActivatingGenerator, ActivatedGenerator, DeactivatingGenerator, DeactivatedGenerator, UnlockingGenerator, UnlockedGenerator, ClosingGenerator, ClosedGenerator, InteractingLocker, InteractedLocker, InteractingScp330, InteractedScp330, InteractingShootingTarget, InteractedShootingTarget, PlacingBlood, PlacedBlood, PlacingBulletHole, PlacedBulletHole, SpawningRagdoll, SpawnedRagdoll, UnlockingWarheadButton, UnlockedWarheadButton, ReceivedAchievement, RoomChanged, ZoneChanged, InteractingWarheadLever, InteractedWarheadLever, SendingHitmarker, SentHitmarker, CheckedHitmarker, ChangedSpectator, EnteringHazard, EnteredHazard, StayingInHazard, LeavingHazard, LeftHazard, ValidatedVisibility, DetectedByScp1344
--- Scp0492Events ---
StartingConsumingCorpse, StartedConsumingCorpse, ConsumingCorpse, ConsumedCorpse
--- Scp049Events ---
StartingResurrection, ResurrectingBody, ResurrectedBody, UsingDoctorsCall, UsedDoctorsCall, UsingSense, UsedSense, Attacking, Attacked, SenseLostTarget, SenseKilledTarget
--- Scp079Events ---
BlackingOutRoom, BlackedOutRoom, BlackingOutZone, BlackedOutZone, ChangingCamera, ChangedCamera, CancellingRoomLockdown, CancelledRoomLockdown, GainingExperience, GainedExperience, LevelingUp, LeveledUp, LockingDoor, LockedDoor, LockingDownRoom, LockedDownRoom, Recontaining, Recontained, UnlockingDoor, UnlockedDoor, UsingTesla, UsedTesla, Pinging, Pinged
--- Scp096Events ---
AddingTarget, AddedTarget, ChangingState, ChangedState, Charging, Charged, Enraging, Enraged, PryingGate, PriedGate, StartCrying, StartedCrying, TryingNotToCry, TriedNotToCry
--- Scp106Events ---
ChangingStalkMode, ChangedStalkMode, ChangingVigor, ChangedVigor, UsedHunterAtlas, UsingHunterAtlas, ChangingSubmersionStatus, ChangedSubmersionStatus, TeleportingPlayer, TeleportedPlayer
--- Scp127Events ---
GainingExperience, GainExperience, LevellingUp, LevelUp, Talking, Talked
--- Scp173Events ---
BreakneckSpeedChanging, BreakneckSpeedChanged, AddingObserver, AddedObserver, RemovingObserver, RemovedObserver, CreatingTantrum, CreatedTantrum, PlayingSound, PlayedSound, Teleporting, Teleported, Snapping, Snapped
--- Scp3114Events ---
Disguising, Disguised, Revealing, Revealed, StrangleStarting, StrangleStarted, StrangleAborting, Dance, StartDancing, StrangleAborted
--- Scp914Events ---
Activating, Activated, KnobChanging, KnobChanged, ProcessingPickup, ProcessedPickup, ProcessingPlayer, ProcessedPlayer, ProcessingInventoryItem, ProcessedInventoryItem
--- Scp939Events ---
Attacking, Attacked, CreatingAmnesticCloud, CreatedAmnesticCloud, Lunging, Lunged, Focused, MimickingEnvironment, MimickedEnvironment
--- ScpEvents ---
HumeShieldBroken
--- ServerEvents ---
WaitingForPlayers, RoundRestarted, Shutdown, DeadmanSequenceActivated, DeadmanSequenceActivating, RoundEndingConditionsCheck, RoundEnding, RoundEnded, RoundStarting, RoundStarted, BanIssuing, BanIssued, BanRevoking, BanRevoked, BanUpdating, BanUpdated, CommandExecuting, CommandExecuted, CassieQueuingScpTermination, CassieQueuedScpTermination, WaveRespawning, WaveRespawned, WaveTeamSelecting, WaveTeamSelected, LczDecontaminationAnnounced, LczDecontaminationStarting, LczDecontaminationStarted, MapGenerating, MapGenerated, PickupCreated, PickupDestroyed, SendingAdminChat, SentAdminChat, ItemSpawning, ItemSpawned, CassieAnnouncing, CassieAnnounced, ProjectileExploding, ProjectileExploded, ExplosionSpawning, ExplosionSpawned, GeneratorActivating, GeneratorActivated, ElevatorSequenceChanged, ModifyingFactionInfluence, ModifiedFactionInfluence, AchievingMilestone, AchievedMilestone, BlastDoorChanging, BlastDoorChanged, RoomLightChanged, RoomColorChanged, DoorLockChanged, DoorRepairing, DoorRepaired, DoorDamaging, DoorDamaged, CheckpointDoorSequenceChanging, CheckpointDoorSequenceChanged, PluginsEnabled
--- WarheadEvents ---
Starting, Started, Stopping, Stopped, Detonating, Detonated
```
{% endhint %}

### Event Variables

Different events provide different variables. For example, the `Dying` event provides:
- `@evPlayer` — The player who is dying
- `@evAttacker` — The player who caused the damage (if applicable)

Use `-- require` when the script cannot do useful work without an event variable:

```ser
!-- OnEvent Dying
-- require @evPlayer @evAttacker

Broadcast @evAttacker 5s "You dealt damage!"
```

{% hint style="warning" %}
`-- require` skips the script when a required value is unavailable. If missing data is an expected case that your script should handle differently, check it with `VarExists` instead.
{% endhint %}

### Event Cancellation

You can cancel a cancellable base-game event with `IsAllowed false`. Use `stop` afterwards when no later code in the script should run:

```ser
!-- OnEvent ProcessingPlayer
-- require @evPlayer $evKnobSetting

if $evKnobSetting is "Rough"
    IsAllowed false
    stop
end
```

{% hint style="warning" %}
`ProcessingPlayer` is cancellable, as shown by `serhelp ProcessingPlayer`. `IsAllowed false` cancels the game event; `stop` only controls the rest of this SER script.
{% endhint %}

---

## OnCustomTrigger Flag

The `OnCustomTrigger` flag makes a script execute when a trigger with a matching name is fired using the `Trigger` method.

**Usage:**
```ser
!-- OnCustomTrigger triggerName
```

**Example:**

First, create a script with the trigger:

```ser
!-- OnCustomTrigger myTrigger

Print "Trigger was fired!"
Broadcast @all 5s "Something happened!"
```

Then, in another script, fire the trigger:

```ser
!-- CustomCommand fireEvent
-- description "Fires the custom trigger"

Trigger myTrigger
```

Now when someone runs `/fireEvent`, the trigger fires and the first script executes!

---

## InteractableToyEvent Flag

The `InteractableToyEvent` flag triggers whenever a player interacts with an InteractableToy (a toy created with SER).

**Usage:**
```ser
!-- InteractableToyEvent
```

**Provided Variables:**
- `@evPlayer` — The player who interacted with the toy
- `*evToy` — The toy that was interacted with

**Example:**

```ser
!-- InteractableToyEvent

Broadcast @evPlayer 5s "You interacted with a toy!"
Hint @evPlayer 3s "Interaction duration: {*evToy -> interactionDuration}s"
```

---

## Legacy Function Flag (Deprecated)

The `Function` flag is a legacy system for creating reusable functions as separate scripts. It predates the modern inline `func`/`end` syntax and is kept for backward compatibility.

**Usage:**
```ser
!-- Function
-- argument $parameterName
-- argument @parameterName
```

**Example:**

Create a function script:

```ser
!-- Function
-- argument $message
-- argument @target

Broadcast @target 5s $message
```

Then call it from another script:

```ser
!-- CustomCommand announce
-- arguments message

RunFunc "MyFunction" $message @all
```

{% hint style="warning" %}
For new code, prefer **inline functions** using `func`/`end` and the `run` keyword. They are more flexible and easier to maintain. See the language specification for details.
{% endhint %}

---

## Quick Reference

| Flag | Purpose | Key Arguments |
|------|---------|---------------|
| `CustomCommand` | Create a custom chat/RA command | `commandName`, `arguments`, `availableFor`, `description` |
| `OnEvent` | React to game events | `EventName`, `-- require` |
| `OnCustomTrigger` | React to custom triggers | `triggerName` |
| `InteractableToyEvent` | React to toy interactions | *(none)* |
| `OnCRole` | React to custom-role lifecycle events | See `serhelp OnCRole` |
| `Function` | Legacy reusable functions | `-- argument` |

---

## What's Next?

Now that you know how to make scripts run automatically, you can start building more complex systems. The next tutorials cover the core language features you'll need:

* [Conditionals](conditionals.md) — `if`/`elif`/`else` statements
* [Loops](loops.md) — `repeat`, `while`, `over`, `forever`
* [Properties](properties.md) — Accessing player and object data with `->`

---
icon: arrow-right
---

# Properties

Methods *do* things — but how do you *get information* about a player? Things like their name, health, or current role? That's what **properties** are for.

---

## A Practical Example

Here's a script that tells a player their own stats:

```ser
!-- CustomCommand inspect
-- availableFor player
-- description "Shows your stats"

$name = @sender -> name
$role = @sender -> role
$health = @sender -> health

Reply "Name: {$name}"
Reply "Role: {$role}"
Reply "Health: {$health}"
```

The `->` operator reads a property from a player. `@sender -> name` gives you the player's username. Let's see what else you can read.

---

## Common Player Properties

| Property | What it gives you | Example |
|----------|-------------------|---------|
| `name` | Username | `@plr -> name` |
| `role` | Current role | `@plr -> role` |
| `team` | Current team | `@plr -> team` |
| `health` | Health points | `@plr -> health` |
| `roomRef` | The room they're in | `@plr -> roomRef` |

```ser
$myHealth = @sender -> health
Broadcast @sender 5s "You have {$myHealth} HP"
```

{% hint style="info" %}
## serhelp properties

```
Properties allow you to access internal data of SER values and SCP:SL objects using the '->' operator.

Syntax:
$hp = @player -> hp               - Accesses 'hp' property of a player variable.
$type = *item -> type             - Accesses 'type' property of a reference variable.
$key = *json -> someKey           - Accesses 'someKey' from a JSON object.

Print {@sender -> name}           - You can use {} brackets to contain the expression into a single argument.

if {@sender -> role} is "ClassD"  - Or use {} when in a condition.


--- Enhanced serhelp properties ---
You can now inspect properties without knowing the exact type name:

From a global variable:
> serhelp properties *myVar

From a local variable from a running script:
> serhelp properties *target script:round_start

From the return value of a method:
> serhelp properties run:GetFromMap doors

You can also specify the assembly:
> serhelp properties Door@LabAPI


--- Basic SER value properties ---

Player:
- accessTier, artificialHealth, auxiliaryPower, cRole, customInfo, etc. (see 'serhelp properties player' for full list)

Collection:
- average, first, isEmpty, last, length, etc. (see 'serhelp properties collection' for full list)

Number:
- abs, ceil, floor, isEven, isOdd, etc. (see 'serhelp properties number' for full list)

Text:
- isEmpty, length, lower, trim, upper, etc. (see 'serhelp properties text' for full list)

Bool:
- asNumber, asString, not, valType

Color:
- a, b, g, hex, r, etc. (see 'serhelp properties color' for full list)

Duration:
- h, m, ms, s, totalH, etc. (see 'serhelp properties duration' for full list)


--- Registered SCP:SL objects ---
Use 'serhelp properties <objectName>' to see available properties for these types:
> Item
> Door
> Pickup
> Room
> DamageHandlerBase
> RespawnWave
> JObject
> JToken
> IPInfo
> Player
and many more not listed here!
```
{% endhint %}

---

## Chaining Properties

You can chain properties together with multiple `->`:

```ser
# Get the player's room, then get the room's name
$roomName = @sender -> roomRef -> name
Broadcast @sender 5s "You are in: {$roomName}"
```

---

## Using Properties in Conditions

When you use a property inside an `if` statement, wrap it in brackets:

```ser
if {@sender -> health} < 50
    Broadcast @sender 5s "You're low on health!"
end
```

{% hint style="info" %}
Brackets are needed in conditions and text, but **not** when assigning to a variable:

✅ `$name = @sender -> name`  
✅ `if {@sender -> health} < 50`  
✅ `"Hello {@sender -> name}"`
{% endhint %}

---

## Checking Reference Validity

Reference variables (rooms, items) can become invalid. Always check first:

```ser
*room = @sender -> roomRef

if {*room -> isInvalid}
    Print "Room no longer exists!"
    stop
end

$roomName = *room -> name
```

{% hint style="warning" %}
C# objects can become null at any time. **Always** check `isInvalid` before using a reference.
{% endhint %}

---

## Enum Strings in Conditions

Properties return enums as **text strings**. Compare them with quotes:

```ser
# In a method — bare enum (no quotes)
SetRole @sender ClassD

# In a condition — quoted string
if {@sender -> role} is "ClassD"
    Broadcast @sender 5s "You're Class-D!"
end
```

---

## Quick Reference

| What you want | How to do it |
|---------------|--------------|
| Read a property | `@plr -> name` |
| Chain properties | `@plr -> roomRef -> name` |
| Use in a variable | `$name = @plr -> name` |
| Use in a condition | `if {@plr -> role} is "ClassD"` |
| Use in text | `"Hello {@plr -> name}"` |
| Check if valid | `if {*room -> isInvalid}` |

---

## What's Next?

Now you can read player data with properties, make decisions with conditionals, and repeat actions with loops. You have the core building blocks of SER scripting.

### [Conditionals](conditionals.md)

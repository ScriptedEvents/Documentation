---
icon: square-pen
metaLinks:
  alternates:
    - /broken/spaces/cuMKPytdZ4h8yad4Mib4/pages/qWB10KW8F31Gl6pxNoyq
---

# Variables

Variables let you store data and reuse it later. In SER, every variable has a **prefix** that tells the engine what kind of data it holds.

---

## Why do I need variables?

Without variables, you'd have to type everything out every time:

```ser
# Without variables — hard to read and update
Broadcast @all 5s "Welcome to Script Mania!"
wait 10s
Broadcast @all 5s "Welcome to Script Mania!"
```

With variables, you write it once and reuse it:

```ser
# With variables — clean and reusable
$msg = "Welcome to Script Mania!"
Broadcast @all 5s $msg
wait 10s
Broadcast @all 5s $msg
```

---

## The Four Prefixes

Every variable starts with one of these symbols:

| Prefix | Type | What it stores |
|--------|------|----------------|
| `@` | Player | One or more players |
| `$` | Literal | Numbers, text, time, true/false |
| `*` | Reference | Rooms, doors, items |
| `&` | Collection | Lists of things |

```ser
# Examples of each type
$serverName = "Script Mania"      # Literal — text
$delay = 5s                       # Literal — time
@targets = @all                   # Player — everyone
*room = @sender -> roomRef        # Reference — a room
```

Think of the prefix as part of the name. You can never leave it off.

```text
# ✅ Correct
$health = 100
@target = @all

# 🚫 Wrong — missing prefix
health = 100
target = @all
```

---

## Creating a Variable

Use `=` to create or update a variable:

```ser
$myText = "Hello!"
$myNumber = 42
$myTime = 3m

@myPlayers = @classDPlayers
```

{% hint style="info" %}
Variable names can only use **letters**, **digits**, and **underscores**. SER follows `camelCase`: `$myVariable`, `@alivePlayers`.
{% endhint %}

---

## Predefined Variables

SER comes with many ready-made variables. The most common one is `@all` — every player on the server.

```ser
Broadcast @all 5s "Hello everyone!"
```

You'll learn more predefined variables in the next tutorial.

---

## What's Next?

Now you know what variables are and how to create them. The next tutorial focuses on **player variables** (`@`) — the type you'll use most often.

### [Player variables](player-variables.md)

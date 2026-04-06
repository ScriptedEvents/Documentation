---
icon: flag
metaLinks:
  alternates:
    - /broken/spaces/cuMKPytdZ4h8yad4Mib4/pages/WNqab5g1vTxtwnC9eBhv
---

# Script Flags

Scripts don't always have to be ran by an admin! Flags allow you to change how a given script executes, whether that be a custom command, base game events and more.

## Where to find valid flags?

Using the `serhelp flags` command you will be granted with a list of flags available. Here is the command response (as of `29.10.2025`):

```
> CustomCommand
> Function
> InteractableToyEvent
> OnCustomTrigger
> OnEvent
```

## How to use a flag?

Let's use the `CustomCommand` flag as an example. Running the `serhelp CustomCommand` command provides us with this documentation (as of `29.10.2025`):

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
  > The arguments that this command expects in order to run. The script cannot run unless every single argument is specified. When the command is ran, the provided values for the arguments turn into their own literal local variables for you to use in the script. For example: making a command with an argument 'name' will then create a local variable $name in your script. Side note: when a player is running the command, a @sender local player variable will also be created.
  > This argument is not required for the flag to operate

  Additional argument 'availableFor':
  > Specifies from which console the command can be executed from. Accepts ConsoleType enum values.
  > This argument is not required for the flag to operate

  Additional argument 'description':
  > The description of the command.
  > This argument is not required for the flag to operate
```

That's a lot to go through! But don't worry, it's not as scary as it seems.

### Flag description

We can read that the `CustomCommand` creates a command, and when that command is executed, the script executes as result!

### Flag usage

We can see a pseudo example of how flags are used:

```
!-- CustomCommand ...
-- arguments ...
-- availableFor ...
-- description ...
```

Let that be the start of our new script, and while we're at it, explain what are we actually looking at.

#### Declaring a flag

```
!-- CustomCommand ...
```

`!-- CustomCommand` is the flag itself. It should be placed at the top of the script. This defines which flag we are using.

#### Inline argument

After `!-- CustomCommand` you can see `...`, these symbolize that we need to put something there. This is the **inline argument** of that flag.

The documentation states this about the inline argument:

```
Inline argument 'command name':
> The name of the command to create
```

So we need to put the command name there, simple! Let's create a command called "hi"

```
!-- CustomCommand hi
```

#### Arguments

All of these are arguments that we can add to the main flag:

```
-- arguments ...
-- availableFor ...
-- description ...
```

> Flag arguments don't have to be in the same order as shown, but they do need to be below the flag itself.

Let's add the `arguments` first! Please read the description of this argument.

Done? Good. Let's add a 'name' argument as the description says.

```
!-- CustomCommand hi
-- arguments name
```

Thanks to it, we will be able to provide more information into the script.

Let's specify the `availableFor` argument next. This argument accepts the `ConsoleType` enum values, shown below (as of `29.10.2025`):

```
Enum ConsoleType has the following values:
> None
> Player
> RemoteAdmin
> Server
```

We want our command to work everywhere, so we can provide all 3 options:

```
!-- CustomCommand hi
-- arguments name
-- availableFor Player RemoteAdmin Server
```

And the description:

```
!-- CustomCommand hi
-- arguments name
-- availableFor Player RemoteAdmin Server
-- description "Says hi!"
```

And that's it! We have the entire flag set up, so let's add a simple reply message to the script and test it:

```
!-- CustomCommand hi
-- arguments name
-- availableFor Player RemoteAdmin Server
-- description "Says hi!"

Reply "Hi, I'm Cheese! Let me guess, your name is:"
Reply $name
```

---

## Other Flags

Now that you understand how flags work, let's explore the other available flags!

### OnEvent Flag

The `OnEvent` flag binds a script to an in-game event. When that event occurs, the script automatically executes.

**Usage:**
```
!-- OnEvent EventName
```

**Example:**
```
!-- OnEvent RoundStarted

Broadcast @all 5s "A new round has started!"
```

When the round starts, all players will see the broadcast message.

**Available Events:**

To see all available events, use the `serhelp events` command. Some common events include:
- `RoundStarted` - When a round begins
- `RoundEnded` - When a round ends
- `PlayerDying` - When a player is about to die
- `PlayerDied` - When a player dies
- `Joined` - When a player joins the server
- `Left` - When a player leaves the server

**Event Variables:**

Different events provide different variables. For example, the `PlayerDying` event provides:
- `@evPlayer` - The player who is dying
- `@evAttacker` - The player who caused the damage (if applicable)

Always check if event variables exist before using them:

```
!-- OnEvent PlayerDying

if {VarExists @evAttacker} is false
    stop
end

Broadcast @evAttacker 5s "You dealt damage!"
```

### OnCustomTrigger Flag

The `OnCustomTrigger` flag makes a script execute when a trigger with a matching name is fired using the `Trigger` method.

**Usage:**
```
!-- OnCustomTrigger triggerName
```

**Example:**

First, create a script with the trigger:

```
!-- OnCustomTrigger myTrigger

Print "Trigger was fired!"
Broadcast @all 5s "Something happened!"
```

Then, in another script, fire the trigger:

```
!-- CustomCommand fireEvent
-- description "Fires the custom trigger"

Trigger myTrigger
```

Now when someone runs `/fireEvent`, the trigger fires and the first script executes!

### InteractableToyEvent Flag

The `InteractableToyEvent` flag triggers whenever a player interacts with an InteractableToy (a toy created with SER).

**Usage:**
```
!-- InteractableToyEvent
```

**Provided Variables:**
- `@evPlayer` - The player who interacted with the toy
- `*evToy` - The toy that was interacted with

**Example:**

```
!-- InteractableToyEvent

Broadcast @evPlayer 5s "You interacted with a toy!"
Hint @evPlayer 3s "Toy name: {ToyInfo *evToy name}"
```

### Function Flag

The `Function` flag marks a script as a reusable function that can be called from other scripts using the `RunFunc` method.

**Usage:**
```
!-- Function
-- argument $parameterName
-- argument @parameterName
```

**Example:**

Create a function script:

```
!-- Function
-- argument $message
-- argument @target

Broadcast @target 5s $message
```

Then call it from another script:

```
!-- CustomCommand announce
-- arguments message

RunFunc "MyFunction" $message @all
```

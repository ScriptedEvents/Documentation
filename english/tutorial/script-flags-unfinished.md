---
icon: flag
metaLinks:
  alternates:
    - /broken/spaces/cuMKPytdZ4h8yad4Mib4/pages/WNqab5g1vTxtwnC9eBhv
---

# Script flags - UNFINISHED

Scripts don't always have to be ran by an admin! Flags allow you to change how a given script executes, whether that be a custom command, base game events and more.

## Where to find valid flags?

Using the `serhelp flags` command you will be granted with a list of flags available. Here is the command response (as of `29.10.2025`):

```
> CustomCommand
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

For the sake of this example, let's create a script available for&#x20;

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

`!-- CustomCommand` is the flag itself. It should be placed at the top of the script. This defines which flag we are using.&#x20;

#### Inline argument&#x20;

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

{% hint style="info" %}
Flag arguments don't have to be in the same order as shown, but they do need to be below the flag itself.
{% endhint %}

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

# the Reply method will reply in the console from which the command was executed
Reply "Hi, I'm Cheese! Let me guess, your name is:"
Reply $name
```

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

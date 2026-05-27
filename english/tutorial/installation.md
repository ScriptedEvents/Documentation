---
description: How to install SER on your server
icon: bars-progress
---

# Installation

{% hint style="danger" %}
This guide is **NOT** about how to set up your SCP:SL server. This guide is for people who know how servers work and have worked with other plugins before.

Things that are not strictly about this plugin - like granting admin roles and setting up your server - are not covered here. The official SCP:SL discord server provides technical support for things like this.
{% endhint %}

## #1 - Install the `SER.dll` file

You can find the latest releases here:

> [https://github.com/ScriptedEvents/ScriptedEventsReloaded/releases](https://github.com/ScriptedEvents/ScriptedEventsReloaded/releases)

## #2 - Move to the correct folder

You can select one of 2 versions of SER:

### `SER.dll`

This is the default version and will work on every server. It should be moved to either one of these locations:

```
LabAPI -> plugins -> [PORT NUMBER] -> SER.dll
```
```
LabAPI -> plugins -> global -> SER.dll
```

{% hint style="info" %}
`[PORT NUMBER]` is a number like `7777`, which corresponds to a port of your server. It's recommended to put use the `global` directory if you're unsure.
{% endhint %}

### `SER-Exiled.dll`

This is the EXILED version and will work only on a server using EXILED. It should be moved to:
```
EXILED -> Plugins -> SER-Exiled.ser
```

## #3 - Restart the server

When the server finishes loading, you should see a message like this:

```
Thank you for using ### Scripted Events Reloaded ### by Elektryk_Andrzej!
```

This means that SER has loaded successfully.

{% hint style="warning" %}
If you don't see this, check if an error hasn't been thrown.
Issues like that are usually caused by improperly configured servers.
{% endhint %}

## #4 - Verify

After a successful installation, you should see a folder like this:

```
LabAPI -> configs -> Scripted Events Reloaded
```

Every script must live in this folder in order to be found by SER.

# Generate example scripts!

We highly recommend you to take a look at some example scripts that SER comes with!

To generate them, use `serexamples` command in the **server console** - this will create a folder:
```
LabAPI -> configs -> Scripted Events Reloaded -> Example Scripts
```

Inside, there will be plenty of scripts, ranging from simple utilities, to full systems like custom roles, chaos coin, custom events and much more!

If you don't want a given script to be active on your server, prefix its name with `#` (e.g. `#chaosCoin.ser`) or just remove it.

# Download the VS Code extension!

If you are planning on writing scripts on your PC, we highly recommend that you download the [`Scripted Events Reloaded` extension](https://marketplace.visualstudio.com/items?itemName=ElektrykAndrzej.ser) for Visual Studio Code!

This extension adds:
* Theme support for SER scripts
* Basic documentation on hovering
* Custom .ser file extension icon
* and more features coming in the future

# Are you a programmer?

If you understand basic concepts like variables, functions, loops, if statements etc., you can go straight here:
### [SER Syntax Specification](https://github.com/ScriptedEvents/ScriptedEventsReloaded/blob/main/language_specification.md)

This one file covers most of the stuff you need to understand about SER syntax.

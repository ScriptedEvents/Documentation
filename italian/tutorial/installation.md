---
description: How to install SER on your server
icon: bars-progress
metaLinks:
  alternates:
    - /broken/spaces/cuMKPytdZ4h8yad4Mib4/pages/F6E70EEaVVcz1vXTvvbz
---

# Installation

{% hint style="danger" %}
This guide is **NOT** about how to set up your SCP:SL server. This guide is for people who know how servers work and have worked with other plugins before.

Things that are not strictly about this plugin - like granting admin roles and setting up your server - are not covered here. The official SCP:SL discord server provides technical support for things like this.
{% endhint %}

## #1 - Install the `SER.dll` and `NCalc.dll` files

You can find the latest releases here:

> [https://github.com/ScriptedEvents/ScriptedEventsReloaded/releases](https://github.com/ScriptedEvents/ScriptedEventsReloaded/releases)

## #2 - Move them to the correct folders

### `SER.dll`

This is the main plugin. This should be moved to either one of these locations:

* `LabAPI -> plugins -> [PORT NUMBER] -> SER.dll`
* `LabAPI -> plugins -> global -> SER.dll`

{% hint style="info" %}
`[PORT NUMBER]` is a number like `7777`, which corresponds to a port of your server. It's recommended to put use the `global` directory if you're unsure.
{% endhint %}

### `NCalc.dll`&#x20;

This is a dependency for handling logical operations like conditions. This should be moved to either:

* `LabAPI -> dependencies -> [PORT NUMBER] -> NCalc.dll`
* `LabAPI -> dependencies -> global -> NCalc.dll`

## #3 - Restart the server

When the server finishes loading, you should see a message like this:

```
Thank you for using ### Scripted Events Reloaded ### by Elektryk_Andrzej!
```

This means that SER has loaded successfully.

{% hint style="warning" %}
If you don't see this, check if an error hasn't been thrown. The most common issues are:

* Either SER or your server are outdated
* Incorrect installation
{% endhint %}

## #4 - Verify&#x20;

After a successful installation, you should see a folder like this:

```
LabAPI -> configs -> Scripted Events Reloaded
```

Every script must live in this folder in order to be found by SER.

## #5 - Generate example scripts (optional)

If you want to check out some example scripts, you can use the `serexamples` command in the server console.

These will be located in:

```
LabAPI -> configs -> Scripted Events Reloaded -> Example Scripts
```

Be sure to know the generated scripts! These may add features that you do not want to have on your server, and are there purely to show off what SER is capable of.

If you find a script that you do not want to have, just remove the file. You can always bring it back using the `serexamples` command again.

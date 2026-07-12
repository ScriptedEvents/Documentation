---
icon: scroll
---

# Scripts

Scripts are lists of commands the server executes automatically. Instead of you running each command by yourself, you can make a script to store all of the commands, and run just that script!

## Where to make a script?

All scripts are stored in this folder:
```
LabAPI -> configs -> Scripted Events Reloaded
```

You can also make folders with scripts inside the `Scripted Events Reloaded` folder, SER also supports that!
```
LabAPI -> configs -> Scripted Events Reloaded -> my awesome folder
```

## How to make a script?

All scripts are text files. Create a file called `myScript.ser` (or `myScript.txt`), which will be your first script.
Once created, copy the following:
```
Reply "Hello, World!"
```

This is now a valid script!

## How to run a script?

You can either run it through the server or remote admin console using the `serrun` command. Simply do

```
serrun <scriptName>
```

So in our case, we replace `<scriptName>` with `myScript`:

```
serrun myScript
```

{% hint style="info" %}
The `serrun` command only expects **script names, not full file names!**
{% endhint %}

You should now see a message like this:

```
serrun myScript
Hello, World!
Script 'myScript' was requested to run
```

{% hint style="warning" %}
When using remote admin console, you will need the `ser.run` permission, otherwise the sender will not be able to run the script.
{% endhint %}

### [Script flags](script-flags.md)

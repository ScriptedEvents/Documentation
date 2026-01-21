---
icon: scroll
layout:
  width: default
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
metaLinks:
  alternates:
    - /broken/spaces/cuMKPytdZ4h8yad4Mib4/pages/zVeO904nSQtlLW7qmMkd
---

# Practical script - Server advertisement

## Aim of the script

Let's make a script which will send customized broadcasts advertising. This will use the `Broadcast` and `Wait` methods to control the timing and content of advertisements.

Let's make a script called `ad.txt` and get to work!

```
# broadcast 1: thanking for playing on our server
# broadcast 2: "check out our github" or smth
# broadcast 3: "consider donating" ad for the moneys 🤑
# we also want to have a 2s gap between broadcasts for more ✨ finesse ✨
```

It's useful to write down what do we want to achieve with a given script.

## Styling

First broadcast should look something like this:

```
Broadcast * 7s "Thank you for playing on Script Mania! Enjoy your stay!"
```

Which in turn looks something like this:

<figure><img src="../.gitbook/assets/image (5).png" alt="" width="563"><figcaption></figcaption></figure>

But we can do better! Using [https://docs.unity3d.com/Packages/com.unity.textmeshpro@4.0/manual/RichTextSupportedTags.html](https://docs.unity3d.com/Packages/com.unity.textmeshpro@4.0/manual/RichTextSupportedTags.html), we can use custom tags to spice up our broadcast like so:

{% code overflow="wrap" %}
```
Broadcast * 7s "<b><size=30><color=#cfc0fa>Thank you for playing on</color></size><br><size=50><color=#ffdc69>ScriptMania!</color></size><br><size=20>Enjoy your stay!</size></b>"
```
{% endcode %}

<figure><img src="../.gitbook/assets/image (6).png" alt="" width="563"><figcaption></figcaption></figure>

## Composing the rest

For the sake of this tutorial, we will be using [discord.gg/3j54zBnbbD](https://discord.gg/3j54zBnbbD) and[ ko-fi.com/elektrykandrzej](https://ko-fi.com/elektrykandrzej) as placeholders. You should replace the contents of all broadcasts with what you want instead.

Using the same principles, we can add the 2nd:

{% code overflow="wrap" %}
```
Broadcast * 7s "<b><size=30><color=#cfc0fa>Check out our discord server!</color></size><br><size=50><color=#ffdc69>discord.gg/3j54zBnbbD</color></size></b>"
```
{% endcode %}

<figure><img src="../.gitbook/assets/image (7).png" alt="" width="563"><figcaption></figcaption></figure>

And the 3rd broadcast:

{% code overflow="wrap" %}
```
Broadcast * 7s "<b><size=30><color=#cfc0fa>Donate to the SER team!</color></size><br><size=50><color=#ffdc69>ko-fi.com/elektrykandrzej</color></size></b>"
```
{% endcode %}

<figure><img src="../.gitbook/assets/image (8).png" alt="" width="563"><figcaption></figcaption></figure>

## Final result

```
# broadcast 1: thanking for playing on our server
# broadcast 2: "check out our github" or smth
# broadcast 3: "consider donating" ad for the moneys 🤑
# we also want to have a 2s gap between broadcasts for more ✨ finesse ✨

Broadcast * 7s "<b><size=30><color=#cfc0fa>Thank you for playing on</color></size><br><size=50><color=#ffdc69>ScriptMania!</color></size><br><size=20>Enjoy your stay!</size></b>"
Wait 9s

Broadcast * 7s "<b><size=30><color=#cfc0fa>Check out our discord server!</color></size><br><size=50><color=#ffdc69>discord.gg/3j54zBnbbD</color></size></b>"
Wait 9s

Broadcast * 7s "<b><size=30><color=#cfc0fa>Donate to the SER team!</color></size><br><size=50><color=#ffdc69>ko-fi.com/elektrykandrzej</color></size></b>"
```

{% hint style="warning" %}
Notice that the `Wait` method doesn't wait for `2s`, but `9s` instead.

This is because the `Broadcast` method is **not yielding**! This means that in this case, where we want to send another broadcast **2 seconds after the previous** broadcast, we need to wait for **7s + 2s, so 9s**
{% endhint %}

Now you've created a complete advertising script!

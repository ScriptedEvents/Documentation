---
icon: user-pen
metaLinks:
  alternates:
    - /broken/spaces/cuMKPytdZ4h8yad4Mib4/pages/SYPENGhvwwAGf2YqEEjK
---

# Fortgeschrittene Spieler-Variablen

Irgendwann reichen die vorgegebenen Spieler-Variablen einfach nicht mehr aus, um das umzusetzen, was du im Kopf hast. Zum Glück kannst du aber noch viel mehr rausholen!

## Eigene Spieler-Variablen erstellen

Es gibt 3 Wege, eigene Variablen zu erstellen – jeder davon ist ein Stück mächtiger als der vorherige.

### Eine leere Variable erstellen

```
# Erstellt eine leere Spieler-Variable mit dem Namen @myPlayerVariable
@myPlayerVariable = ()
```

Wenn du mal eine komplett leere Variable brauchst, ist das der Weg.

### Eine bestehende Variable kopieren

```
# Erstellt eine Kopie der @scpPlayers Variable
@myVar = @scpPlayers
```

Damit hast du eine Variable erstellt, die exakt die gleichen Spieler enthält, die `@scpPlayers` in diesem Moment hat!

#### Beispiel-Anwendung

Schau dir mal dieses Script hier an:

<pre><code># Wir wollen alle SCPs töten und sie zu CI machen
Kill @scpPlayers
<strong>SetRole @scpPlayers ChaosConscript
</strong></code></pre>

Hier solltest du direkt skeptisch werden. Wir können die `@scpPlayers` nicht zu Chaos Conscripts machen, wenn alle SCPs gerade gestorben sind!

Versuchen wir es stattdessen mal mit `@spectatorPlayers`:

<pre><code># Wir wollen alle SCPs töten und sie zu CI machen
Kill @scpPlayers
<strong>SetRole @spectatorPlayers ChaosConscript
</strong></code></pre>

Das würde zwar funktionieren, aber dann werden auch alle anderen Zuschauer – die vorher gar keine SCPs waren – zu CI. Das ist ein ziemliches Dilemma, aber wir können das Problem lösen, **indem wir einfach eine Kopie von `@scpPlayers` machen!**

<pre><code># Hier erstellen wir eine Kopie von @scpPlayers und benutzen diese
<strong>@scpsToDie = @scpPlayers
</strong>Kill @scpsToDie
SetRole @scpsToDie ChaosConscript
</code></pre>

Warum ist das die richtige Lösung für das Problem?

{% hint style="info" %}
## Eigene Variablen aktualisieren sich nicht von selbst!

Das bedeutet: Es ist völlig egal, ob sich der Wert von `@scpPlayers` später ändert. Der Wert der Variable `@scpsToDie` **ändert sich nicht mit**.

Mit anderen Worten: Der Wert von `@scpsToDie` macht quasi einen "Snapshot" (Schnappschuss) von allen Spielern, die gerade in der `@scpPlayers` Variable drin sind. Was danach mit diesen Spielern passiert, ist der neuen Variable völlig egal.
{% endhint %}

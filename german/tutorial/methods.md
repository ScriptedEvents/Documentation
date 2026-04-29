---
icon: command
metaLinks:
  alternates:
    - /broken/spaces/cuMKPytdZ4h8yad4Mib4/pages/z82x1UopunT8VxmQ9tE8
---

# Methoden

Methoden sind im Grunde wie Befehle. Genau wie Befehle können sie bestimmte Argumente oder Parameter entgegennehmen und damit etwas auslösen. Sie sind quasi die Bausteine deiner Scripts.

## Was gilt als Methode?

Damit das Script etwas als Methode erkennt, müssen folgende Punkte erfüllt sein:

1. Es muss eine existierende Methode sein (du findest sie über `serhelp methods`).

```
🚫 SendMassiveMessage "Hello, World!"
✅ Reply "Hello, World!"
```

2. Es muss das erste Wort in der Zeile sein (es gibt Ausnahmen, die später erklärt werden).

```
🚫 test Reply "Hello, World!"
✅ Reply "Hello, World!"
```

3. Die Groß- und Kleinschreibung muss exakt stimmen.

```
🚫 reply "Hello, World!"
🚫 REPLY "Hello, World!"
✅ Reply "Hello, World!"
```

## Welche Methoden kann ich benutzen?

Der Befehl `serhelp` verrät es dir! Wenn du `serhelp methods` eingibst, bekommst du eine Liste mit allen Methoden, die dir zur Verfügung stehen.

{% hint style="warning" %}
Bis du dieses Tutorial liest, könnte sich der Befehl ein wenig geändert haben. Ich rate dir, selbst kurz zu prüfen, ob der Befehl noch so aussieht wie hier gezeigt.
{% endhint %}

Hier ist ein kleiner Ausschnitt der Ausgabe:

```
...

--- Broadcast methods ---
> ClearCountdown       Entfernt einen aktiven Countdown für Spieler.
> Countdown            Erstellt einen Countdown via Broadcast.
> Broadcast            Sendet einen Broadcast an Spieler.
> ClearBroadcasts      Löscht alle Broadcasts für Spieler.
> Hint                 Sendet einen Hint (Hinweis) an Spieler.

...
```

## Wie bekomme ich Infos zu einer bestimmten Methode?

Du kannst `serhelp <methodenName>` eingeben, um Infos zu einer spezifischen Methode zu erhalten. Schauen wir uns mal an, was passiert, wenn wir `serhelp Broadcast` eingeben:

```
=== Broadcast ===
> Sendet einen Broadcast an Spieler.

Diese Methode erwartet folgende Argumente:
(1) 'players' Argument
 - Erwarteter Wert: Spieler-Variable z.B. @players oder * für alle Spieler

(2) 'duration' Argument (Dauer)
 - Erwarteter Wert: Dauer im Format #ms (Millisekunden), #s (Sekunden), #m (Minuten) etc., z.B. 5s oder 2m

(3) 'message' Argument (Nachricht)
 - Erwarteter Wert: Beliebiger Text z.B. "Hello, World!"
```

## Wie nutze ich diese Informationen?

Sagen wir mal, wir wollen den Broadcast `cool broadcast` für 3 Sekunden an alle Spieler senden. Wie machen wir das?

Wir haben 3 Argumente:

1. **Das `players` Argument** Wenn wir "alle Spieler" meinen, nehmen wir einfach das Sternchen `*`.

```
Broadcast *
```

2. **Das `duration` Argument** In der Hilfe steht, wie es geht: Wir brauchen Sekunden, also nutzen wir das Format `#s`. Wir ersetzen `#` durch unsere Zahl, also `3s`.

```
Broadcast * 3s
```

3. **Das `message` Argument** Das ist der Text, der angezeigt werden soll. Wir schreiben also `"cool broadcast"`.

```
Broadcast * 3s "cool broadcast"
```

{% hint style="danger" %}
## Text in SER angeben
Wenn du Text angibst, MUSST du ihn in Anführungszeichen setzen. Wenn du das nicht machst, wird **jedes Wort** als **eigenes Argument** gewertet, was zu einem Fehler führt.

```
            #1      #2       #3        #4
🚫 Reply Beispiel Nachricht zum Ausgeben

          - - - - -  #1  - - - - -
✅ Reply "Beispiel Nachricht zum Ausgeben"
```
{% endhint %}

Mit diesem Wissen können wir ruckzuck einen Player-Broadcast erstellen! Öffne die Datei `myScript.txt` in deinem `SER`-Ordner und füge folgendes hinzu:

```
Reply "Hello, World!"
Broadcast * 3s "cool broadcast"
```

Wenn du das Script jetzt ausführst, solltest du einen Broadcast wie diesen hier sehen:

<figure><img src="https://github.com/user-attachments/assets/126d0612-4b1d-4d83-b492-78def6ca546b" alt="" width="563"><figcaption></figcaption></figure>

Und das war's auch schon – du weißt jetzt, wie man Methoden benutzt!

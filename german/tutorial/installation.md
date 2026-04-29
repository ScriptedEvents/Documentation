---
description: So installierst du SER auf deinem Server
icon: bars-progress
metaLinks:
  alternates:
    - /broken/spaces/cuMKPytdZ4h8yad4Mib4/pages/F6E70EEaVVcz1vXTvvbz
---

# Installation

{% hint style="danger" %}
In dieser Anleitung geht es **NICHT** darum, wie du deinen SCP:SL Server grundlegend einrichtest. Dieser Guide ist für Leute gedacht, die wissen, wie Server funktionieren und die schon mal mit Plugins gearbeitet haben.

Dinge, die nicht direkt mit diesem Plugin zu tun haben – wie das Zuweisen von Admin-Rollen oder das Aufsetzen des Servers – werden hier nicht behandelt. Der offizielle SCP:SL Discord-Server bietet technischen Support für solche Themen.
{% endhint %}

## #1 - Installiere die `SER.dll` Datei

Die neuesten Versionen (Releases) findest du hier:

> [https://github.com/ScriptedEvents/ScriptedEventsReloaded/releases](https://github.com/ScriptedEvents/ScriptedEventsReloaded/releases)

## #2 - In den richtigen Ordner verschieben

### `SER.dll`

Das ist das Haupt-Plugin. Es sollte in einen dieser beiden Ordner verschoben werden:

* `LabAPI -> plugins -> [PORT NUMMER] -> SER.dll`
* `LabAPI -> plugins -> global -> SER.dll`

{% hint style="info" %}
`[PORT NUMMER]` ist eine Zahl wie `7777`, die dem Port deines Servers entspricht. Wenn du dir unsicher bist, nimm einfach den `global` Ordner.
{% endhint %}

## #3 - Server neu starten

Wenn der Server fertig geladen hat, solltest du eine Nachricht wie diese hier sehen:

```
Thank you for using ### Scripted Events Reloaded ### by Elektryk_Andrzej!
```

Das bedeutet, dass SER erfolgreich geladen wurde.

{% hint style="warning" %}
Falls du das nicht siehst, prüfe, ob eine Fehlermeldung ausgegeben wurde. Die häufigsten Probleme sind:

* Entweder SER oder dein Server sind veraltet
* Falsche Installation
{% endhint %}

## #4 - Überprüfen

Nach einer erfolgreichen Installation solltest du diesen Ordner hier sehen:

```
LabAPI -> configs -> Scripted Events Reloaded
```

Jedes Script muss in diesem Ordner liegen, damit SER es finden kann.

## #5 - Beispiel-Scripts generieren (optional)

Wenn du dir ein paar Beispiel-Scripts ansehen willst, kannst du den Befehl `serexamples` in der Server-Konsole nutzen.

Diese findest du dann hier:

```
LabAPI -> configs -> Scripted Events Reloaded -> Example Scripts
```

Schau dir die generierten Scripts auf jeden Fall an! Sie könnten Funktionen hinzufügen, die du vielleicht gar nicht auf deinem Server haben willst. Sie sind rein dazu da, um zu zeigen, was SER alles drauf hat.

Wenn dir ein Script nicht gefällt, lösch die Datei einfach. Du kannst sie jederzeit mit dem `serexamples` Befehl wieder herholen.

---
description: Wie installierst du SER auf deinem Server
icon: bars-progress
metaLinks:
  alternates:
    - /broken/spaces/cuMKPytdZ4h8yad4Mib4/pages/F6E70EEaVVcz1vXTvvbz
---

# Installation

{% hint style="danger" %}
Diese Anleitung beschreibt **NICHT**, wie du deinen SCP:SL Server erstellst. Diese Anleitung richtet sich an Personen, die mit deren Server vertraut sind und bereits Erfahrung mit anderen Erfahrungen mit anderen Plugins haben.

Dinge, die nicht direkt mit diesem Plugin zusammenhängen - wie die Vergabe von Admin-Rollen oder die Servereinrichtung - werden hier nicht behandelt. Der offizielle SCP:SL Discord bietet dafür den Technischen Support.
{% endhint %}

## #1 - Installiere die `SER.dll` Datei und `NCalc.dll` Dateien

Du kannst die neueste Version hier finden:

> [https://github.com/ScriptedEvents/ScriptedEventsReloaded/releases](https://github.com/ScriptedEvents/ScriptedEventsReloaded/releases)

## #2 - Verschiebe diese in den richtigen Ordner

### `SER.dll`

Dies ist das eigentliche Plugin. Diese sollte in einen dieser Ordner verschoben werden:

* `LabAPI -> plugins -> [PORT NUMBER] -> SER.dll`
* `LabAPI -> plugins -> global -> SER.dll`

{% hint style="info" %}
`[PORT NUMBER]` ist eine Nummer wie `7777`, welche als Port deines Servers gilt. Wir empfehlen den `global` Ordner zu nutzen, wenn du dir unsicher bist.
{% endhint %}

### `NCalc.dll`&#x20;

Dies ist die Dependency des Plugins. Sie wird für die Verarbeitung logischer Operationen wie Bedingungen benötigt. Diese Datei gehört in einer dieser Ordner:

* `LabAPI -> dependencies -> [PORT NUMBER] -> NCalc.dll`
* `LabAPI -> dependencies -> global -> NCalc.dll`

## #3 - Den Server neustarten

Wenn der Server den Neustart abgeschlossen hat, sollte so eine Nachricht in der Konsole auftauchen:

```
Thank you for using ### Scripted Events Reloaded ### by Elektryk_Andrzej!
```

Dies bedeutet, dass SER korrekt geladen wurde.&#x20;

{% hint style="warning" %}
Wenn du das nicht siehst, prüfe, ob ein Fehler aufgetreten ist. Häufige Probleme sind:

* Entweder SER oder der Server sind nicht mehr aktuell
* Falsche Installation
{% endhint %}

## #4 - Verifizierung&#x20;

Nach einer erfolgreichen Installation, solltest du diesen Ordner sehen:

```
LabAPI -> configs -> Scripted Events Reloaded
```

Jedes Skript muss sich in diesem Ordner befinden um geladen zu werden.

## #5 - Generiere Beispiele für Skripts (Optional)

Wenn du dir einige Beipiele für Skripts ansehen willst, kannst du den Befehl `serexamples` in der Konsole eingeben.

Diese befinden sich dann in:

```
LabAPI -> configs -> Scripted Events Reloaded -> Example Scripts
```

Mache dich mit den generierten Skripts vertraut! Diese fügen vielleicht Features zu deinem Server hinzu, die du nicht möchtest und sind hauptsächlich für die demonstrierung der Fähigkeiten von SER da.

Wenn du ein unerwünschtes Skript hast, entferne einfach die Datei. Du kannst diese immer mit dem Befehl `serexamples` wieder generieren.

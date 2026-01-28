---
icon: scroll
metaLinks:
  alternates:
    - /broken/spaces/cuMKPytdZ4h8yad4Mib4/pages/R2VVig28xjUEym0cJuf4
---

# Skripts

Skripte sind Listen von Befehlen, die der Server automatisch ausführt. Anstatt jeden Befehl einzeln auszuführen, kannst du ein Skript erstellen, welches alle Befehle speichert, und nur dieses Skript ausführen!

## Wo machst du ein Skript?

Alle Skripte sind im Ordner `LabAPI -> configs -> Scripted Events Reloaded` gespeichert. Du kannst auch Ordner mit Skripten innerhalb des Ordners `Scripted Events Reloaded` erstellen, SER unterstützt dies!

## Wie machst du ein Skript?

Alle Skripte sind eine Textdatei. Erstelle eine Datei mit dem Namen `meinSkript.txt`, welches dein erstes Skript sein wird. Wenn du es erstellt hast, kopiere folgendes:

```
Reply "Hello, World!"
```

Dies ist nun ein vollständiges Skript!

## Wie starte ich ein Skript?

Du kannst entweder über den Server oder die Remote-Admin Konsole mit den `serrun` Befehl ausführen. Schreibe ganz einfach:

```
serrun <skriptName>
```

In unserem Fall, ersetzen wir `<skriptName>` mit `meinSkript`:

```
serrun meinSkript
```

{% hint style="info" %}
Der `serrun` Befehl erwartet nur den **Skript Name, nicht den vollen Dateiname!**
{% endhint %}

Du solltest nun eine Nachricht wie folgendes sehen:

```
[21:37:69] serrun meinSkript
[21:37:69] Hello, World!
[21:37:69] Script 'meinSkript' was requested to run
```

{% hint style="warning" %}
Wenn du die Remote-Admin Konsole benutzt, brauchst du die `ser.run` Berechtigung, ansonsten kannst du es nicht ausführen.
{% endhint %}

# REDAXO Dokumentation

Die aktuelle Live-Version ist hier ersichtlich: <https://redaxo.org/doku/main>

## Hinweise zur Mitarbeit

Wir freuen uns sehr über Mitarbeit bei der REDAXO-Dokumentation. Ihr könnt gern jederzeit komplette Kapitel übernehmen (bitte mit polarpixel, tbaddade oder skerbis absprechen) oder einfach nur Verbesserungen und Korrekturen einbringen (dann am besten als Pull request)

## Bitte beachten

Bei der Formatierung und dem Markdown-Syntax an vorhandenen Dokumenten orientieren, möglich sind:

* Überschriften
* Sprunganker
* Listen
* Tabellen
* Hinweise (eingerückt mit `> **Hinweis:** ...`)
* Inline-Code und Code-Blöcke (ausgezeichnet mit 3 Backticks)
* Bilder
* ABBR (Erläuterung weiter unten)

> **Tipp:** Der Markdown-Editor eurer Wahl unterstützt möglicherweise Linting und weitere Formatierungshilfen. 

### Inhaltsverzeichnis

Diese Sprunganker-Navigation (Inhaltsverzeichnis des Kapitels) muss direkt am Anfang hinter der ersten Überschrift kommen. Direkt danach muss die zweite Überschrift folgen. Bitte in jedes Kapitel eine Sprunganker-Navigation integrieren:

```
# Seitenüberschrift

- [Überschrift](#anker-zur-ueberschrift)
- [Anker 2](#anker-2)
    - [Anker 2a](#anker2a)
- [Anker 3](#anker-3)
    - [Anker 3a](#anker-3a)
    - [Anker 3b](#anker-3b)
    - [Anker 3c](#anker-3c)
- [Anker 4](#anker-4)

<a name="anker-zur-ueberschrift"></a>

## Überschrift 

[...]
```

### Bearbeitungsstatus

Wenn man sich einen Inhalt vornimmt, bitte mit Namen und Status markieren in der [dokumentation.md](dokumentation.md)

> **Hinweis:** Die Links in der Inhaltsverzeichnis-Datei [dokumentation.md](dokumentation.md) funktionieren nicht innerhalb von GitHub, da sie vorbereitet sind für den automatischen Import in die REDAXO-Website. Ihr müsst daher die gewünschte Datei selbst auswählen und öffnen.

### Schreibstil

- Möglichst ohne direkte Anrede (Du / Sie) auskommen. Falls in Ausnahmefällen nicht möglich, dann "Du" verwenden statt "Sie"

### Schreibweisen häufig vorkommender Begriffe

- REDAXO
- AddOn
- PlugIn

### Coding-Standard

Bei den Code-Beispielen bitte bei den allgemein gültigen REDAXO-Coding-Standard beachten:
[http://symfony.com/doc/current/contributing/code/standards.html](http://symfony.com/doc/current/contributing/code/standards.html)

### Bilder und Screenshots

- Breite 1600 Pixel Breite. Höhe, wie man es braucht.
- Kein Browserfenster soll zu sehen sein.
- Immer den kompletten REDAXO-Inhalt, inklusive Navigation.
- Benennung: v5.2.0-[Kennung-was-das-Bild-zeigt].png
- In den Assets-Ordner.
- Immer Standard-Theme mit aktivierten AddOns aus der Installation verwenden, damit die Navigation gleich aussieht.


### ABBR

Mit ABBR kann beim überfahren mit der Maus zum Beispiel die Langform einer Abkürzung anzeigt werden.

Steht irgendwo im Text z.B. folgendes: **BSI**, kann mit diesem Code der zusätzliche Hinweis angezeigt werden:

```
*[BSI]: Bundesamt für Sicherheit in der Informationstechnik
```
*Beispiel aus der installation.md*

Mehr dazu kann hier nachgelesen werden: [PHP Markdown Extra](https://michelf.ca/projects/php-markdown/extra/#abbr)

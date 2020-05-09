# Console

- [Einführung](#einfuehrung)
- [Aufruf der Console](#aufruf)
- [Hilfe](#hilfe)
- [Entwicklung eigener Consolen-Skripte](#dev)
  - [run.php](#run)
  - [package.yml](#package)

<a name="einfuehrung"></a>

## Einführung

Die Console ermöglicht REDAXO Funktionen direkt über das Commandline Interface (CLI) des Systems auszuführen. Dies kann genutzt werden, um Code unabhängig von einem HTTP Request direkt auf dem Server über die Systemconsole auszuführen.

Console Befehle können unter anderem für folgende Aufgaben eingesetzt werden:

- REDAXO-Installation
- AddOn-Installation / Deinstallation
- Schnittstelle für erweitere/spezielle Funktionen/Vorgänge
- Automatisierung/Skripting von Abläufen mit Zugriff auf das System
- Umgebung um sehr aufwändige prozesse wie migrationen o.ä. Ablaufen zu lassen, ohne timeouts etc.
- Fernwartung des Systems
- Automatisierte Veröffentlichungsprozesse der Entwicklungsstände von Websiten (Deploy-Workflows)
- via AddOns erweiterbar (Kommandos registrierbar, siehe untenstehendes Beispiel)

<a name="aufruf"></a>

## Aufruf der Console

```console
php redaxo/bin/console
```

oder

```console
redaxo/bin/console
```

(Hierbei sollte die Datei `console` ausführbar sein)

Je nach System ist es ggf. erforderlich, die Console unter dem PHP-User bzw. Eigentümer des Webordners auszuführen. In diesem Fall lautet der Befehl:

```console
sudo -u username php redaxo/bin/console
```

Für Docker exec sollte man `-u username` an den Befehl anfügen.  

<a name="hilfe"></a>

## Hilfe

Der einfache Aufruf der Console per `console` ohne Parameter liefert eine Liste aller
aktuell verfügbaren Consolen-Kommandos.

Um mehr Informationen und Optionen zu den einzelnen Befehl zu erhalten fügt man dem Aufruf des Befehls `--help` als Parameter an.

z.B: `console cache:clear --help`

<a name="dev"></a>

## Entwicklung eigener Consolen-Skripte

<a name="run"></a>

### run.php

Die Ausführung eines Console Befehls erfordert eine eigene Klasse, die auf `rex_console_command` aufbaut und den ausführbaren Code selbst enthält bzw. aufruft. In dieser Klasse muss es eine Methode `execute` geben. Die einfachste Form sieht etwa so aus:

```php
class mein_console_befehl extends rex_console_command {
    protected function execute() {
        echo "hallo redaxo"; // beliebiges php hier
    }
}
```

Falls die implementierte Funktionalität sowohl via Weboberfläche als auch REDAXO Console zugreifbar sein sollte, würde es sich anbieten die entsprechende Logik in einer separaten PHP Klasse zu implementieren und diese aus der o.g. Klasse heraus aufzurufen.

<a name="package"></a>

### package.yml

Damit der ausführbare Befehl in der REDAXO Console zugänglich ist, muss er noch in der package.yml eines AddOns als solcher definiert werden.

**Beispiel**

```yml
console_commands:
    meinaufruf:befehl: mein_console_befehl
```

# Console

- [Einführung](#einfuehrung)
- [run.php](#run)
- [package.yml](#package)
- [Aufruf](#console)

<a name="einfuehrung"></a>
## Einführung

Die Console ermöglicht REDAXO Funktionen direkt über das Commandline Interface (CLI) des Systems auszuführen. Dies kann genutzt werden, um Code unabhängig von einem HTTP Request direkt auf dem Server über die Systemconsole auszuführen.

Console Befehle können unter anderem für folgende Aufgaben eingesetzt werden:

	- Schnittstelle für erweitere/spezielle Funktionen/Vorgänge
	- Automatisierung/Skripting von Abläufen mit Zugriff auf das System
	- Umgebung um sehr aufwändige prozesse wie migrationen o.ä. Ablaufen zu lassen, ohne timeouts etc.
	- Fernwartung des Systems
	- Automatisierte Veröffentlichungsprozesse der Entwicklungsstände von Websiten (wird von `ydeploy` eingesetzt)
	- via AddOns erweiterbar (Kommandos registrierbar, siehe ydeploy und untenstehendes Beispiel)

<a name="run"></a>
## run.php

Die Ausführung eines Console Befehls erfordert eine eigene Klasse, die auf `rex_console_commands` aufbaut und den ausführbaren Code selbst enthält bzw. aufruft. In dieser Klasse muss es eine Funktion `execute` geben. Die einfachste Form sieht etwa so aus:

```php
class mein_console_befehl extends rex_console_command {
    protected function execute() {
        echo "hallo redaxo"; // beliebiges php hier
    }
}
```

Falls die implementierte Funktionalität sowohl via Weboberfläche als auch REDAXO Console zugreifbar sein sollte, würde es sich anbieten die entsprechende Logik in einer separaten PHP Klasse zu implementieren und diese aus der o.g. Klasse heraus aufzurufen.

<a name="package"></a>
## package.yml

Damit der ausführbare Befehl in der REDAXO Console zugänglich ist, muss er noch in der package.yml eines AddOns als solcher definiert werden.

**Beispiel**

```yml
console_commands:
    meinaufruf:befehl: mein_console_befehl
```

<a name="console"></a>
## Console Aufruf

Der Console Aufruf muss über PHP erfolgen:

```
/apache/php/php redaxo/bin/console meinaufruf:befehl
```

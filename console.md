# Konsole

- [Einführung](#einfuehrung)
- [Aufruf der Konsole](#aufruf)
- [Hilfe](#hilfe)
- [Anwendungsbeispiele](#beispiele)
  - [Passwort setzen](#passwort-setzen)
  - [Datenbank Backup erzeugen/zurückspielen](#datenbank)
  - [Datenbank Schema als PHP exportieren](#dbschema-export)
  - [package:list](#package-list)
  - [install:list](#install-list)
  - [Core/AddOn/PlugIn Assets synchronisieren](#asset-sync)
- [Entwicklung eigener Konsolen-Skripte](#dev)
  - [run.php](#run)
  - [package.yml](#package)
- [Integration der Konsole in Phpstorm](#phpstorm)
- [Tipps](#tipps)
  - [Autovervollständigung](#tipp-autocomplete)

<a name="einfuehrung"></a>

## Einführung

REDAXO liefert mehrere CLI ("Command-line interface")-Befehle und Dienstprogramme, die über die Konsole (console) ausgeführt werden können. Sie ermöglichen es u.a. REDAXO zu installieren, AddOns zu aktualisieren und den Entwicklungsprozess sowie Wartungsarbeiten zu beschleunigen. AddOns oder PlugIns können den Funktionsumfang der Konsole um weiteren Befehle erweitern.

Mögliche Einsatzzwecke:

- [REDAXO Installation](/{{path}}/{{version}}/installation#console)
- [AddOn-Installation / Deinstallation](/{{path}}/{{version}}/basis-addons#console)
- Schnittstelle für erweitere/spezielle Funktionen/Vorgänge
- Automatisierung/Scripting von Abläufen mit Zugriff auf das System
- Umgebung um sehr aufwändige Prozesse wie Migrationen, Report-Generierung o.ä. ablaufen zu lassen, ohne Timeouts etc.
- Fernwartung des Systems
- automatisierte Veröffentlichungsprozesse der Entwicklungsstände von Websites (Deploy-Workflows)
- via AddOns erweiterbar (Befehle registrierbar, siehe untenstehendes Beispiel)

Im Rahmen einer REDAXOHour ist eine Videoeinführung entstanden, die viele Punkte dieses Kapitels erklärt.

<a class="button-secondary" href="https://www.youtube.com/watch?v=5tU5s7m9-tM">Zum Video bei YouTube</a>

<a name="aufruf"></a>

## Aufruf der Konsole

```console
php redaxo/bin/console
```

oder

```console
redaxo/bin/console
```

(Hierbei sollte die Datei `console` ausführbar sein)

Je nach System ist es ggf. erforderlich, die Konsole unter dem PHP-User bzw. Eigentümer des Webordners auszuführen. In diesem Fall lautet der Befehl:

```console
sudo -u username php redaxo/bin/console
```

Für Docker exec sollte man `-u username` an den Befehl anfügen.  

<a name="hilfe"></a>

## Hilfe

Der einfache Aufruf der Konsole per `console` ohne Parameter liefert eine Liste aller
aktuell verfügbaren Konsolen-Befehle.

Um mehr Informationen und Optionen zum jeweiligen Befehl zu erhalten, fügt man dem Aufruf des Kommandos `--help` als Parameter an.

z. B.: `console cache:clear --help`

<a name="beispiele"></a>

## Anwendungsbeispiele

<a name="passwort-setzen"></a>

### Passwort setzen

Durch den Zugriff via REDAXO Konsole können für Backend-Benutzer neue Passwörter gesetzt werden.
Dies ist insbesondere dann hilfreich, wenn kein Admin-Zugriff via Backend mehr möglich ist.

```console
php redaxo/bin/console user:set-password <username> <passwort>
```

<a name="datenbank"></a>

### Datenbank Backup erzeugen/zurückspielen

Da in der Konsole in der Regel weniger Restriktionen gegeben sind, können umfangreiche Datenbanksicherungen erstellt oder wiederhergestellt werden. Speziell für große Datenbanken ist dies ein effizienter Weg zur Sicherung.

**Erzeugt eine Sicherung in der Datei `dump.sql`**

```console
php redaxo/bin/console db:connection-options | xargs mysqldump > dump.sql
```

**Wiedereinspielen einer vorher erstellten Sicherung** aus der Datei `dump.sql`.
In der Datenbank enthaltene Tabellen und Daten werden dabei überschrieben!

```console
php redaxo/bin/console db:connection-options | xargs sh -c 'mysql "$0" "$@" < dump.sql'
```

<a name="asset-sync"></a>

### Core/AddOn/PlugIn Assets synchronisieren

Um die Entwicklung von AddOns und PlugIns zu erleichtern, ist es möglich Dateien zwischen dem öffentlich zugänglichen `assets/` Ordner und den AddOn/PlugIn Quellen unter `redaxo/src/addons` zu synchronisieren.

```console
php redaxo/bin/console assets:sync
```

<a name="dbschema-export"></a>

### Datenbankschema als PHP exportieren

Bei der Entwicklung von AddOns und PlugIns ist es beim Verwenden von Datenbank-Tabellen notwendig, diese bei der Installation des AddOns/PlugIns anzulegen. Dafür bietet REDAXO eine Schema API, die es erlaubt Tabellen zu erzeugen und zu migrieren.

Der dafür notwendige PHP Code lässt sich mittels Konsolen-Befehl erzeugen, um Ihn anschließend in die `install.php` zu kopieren.

```console
php redaxo/bin/console db:dump-schema <tabellenname>
```

<a name="package-list"></a>

### package:list ###

`package:list`Liefert Informationen über installierte AddOns 

Optionen: 

- search: filtert die Liste nach dem Suchbegriff
- installed-only (-i): zeigt nur installierte Packages an
- activated-only (-a): zeigt nur installierte & aktivierte Packages an
- using-exit-code: gibt je nachdem, ob es zu den ausgewählten Filtern ein Ergebnis gibt, `0` oder `1` als exit-code zurück (hilfreich bei Skripten)
- json: liefert anstelle einer formatierten Tabelle ein JSON mit Packages.

<a name="install-list"></a>

### install:list ###

![Screenshot](/assets/v5.12.0-package_list.png)

`install:list` Listet alle verfügbaren Addons von redaxo.org auf und zeigt die installierte Version dazu an.

Optionen:

- `--search` - Filtert die Liste anhand eines Suchbegriffs (vgl. Filterung/Suche im Backend)
- `--updates-only` - Zeigt nur AddOns an, für die ein Update verfügbar ist
- `--json` - gibt die Ausgabe als JSON (für z.B. Verarbeitung in Skripten)



<a name="dev"></a>

## Entwicklung eigener Konsolen-Skripte

<a name="run"></a>

### run.php

Die Ausführung eines Konsolen-Befehls erfordert eine eigene Klasse, die auf `rex_console_command` aufbaut und den ausführbaren Code selbst enthält bzw. aufruft. In dieser Klasse muss es eine Methode `execute` geben. Die einfachste Form sieht etwa so aus:

```php
class mein_console_befehl extends rex_console_command {
    protected function execute() {
        echo "hallo redaxo"; // beliebiges php hier
    }
}
```

Falls die implementierte Funktionalität sowohl via Weboberfläche als auch REDAXO Konsole zugreifbar sein sollte, würde es sich anbieten, die entsprechende Logik in einer separaten PHP Klasse zu implementieren und diese aus der o.g. Klasse heraus aufzurufen.

<a name="package"></a>

### package.yml

Damit der ausführbare Befehl in der REDAXO Konsole zugänglich ist, muss er noch in der package.yml eines AddOns als solcher definiert werden.

**Beispiel**

```yml
console_commands:
    meinaufruf:befehl: mein_console_befehl
```


<a name="phpstorm"></a>

## Integration der Konsole in Phpstorm

Da die REDAXO Konsole auf der `symfony/console` Bibliothek aufsetzt, kann die [REDAXO Konsole wie eine herkömmliche Symfony-Console](https://www.jetbrains.com/help/phpstorm/symfony-support.html#use_symfony_cli) mit Phpstorm integriert werden.

Dies ist möglich, sobald das REDAXO-Setup abgeschlossen wurde.



<a name="tipps"></a>

## Tipps


<a name="tipp-autocomplete"></a>

### Autovervollständigung

Um die Bedienbarkeit der Konsole zu verbessern, ist es möglich ein [Autovervollständigung-Skript](https://github.com/bamarni/symfony-console-autocomplete) zu verwenden, dass auf der Konsole durch doppeltes Drücken der Tab-Taste ausgelöst wird.

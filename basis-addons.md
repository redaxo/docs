# AddOns

* [Über](#ueber)
* [Im Lieferumfang enthaltene AddOns](#included)
* [AddOn Verwaltung](#addons)
* [Upload](#upload)
  + [Upload per Installer](#upinstaller)
  + [Manueller Upload per (S)FTP](#upftp)
  + [Hinweis zu AddOns aus GitHub](#github)  
* [AddOn-Installation](#install)
* [Update](#update)
* [Reinstallieren / Reparatur](#reinstall)
* [Deinstallation](#uninstall)
* [Konsolen Befehle](#console)
  + [Download per Konsole](#downconsole)
  + [Liste aller verfügbaren AddOns](#conlist)
  + [AddOn-Update](#conupdate)
  + [AddOn löschen](#condelete)

<a name="ueber"></a>

## Über AddOns

AddOns sind Erweiterungen für REDAXO. Sie können zum Beispiel zusätzliche Funktionen liefern, die Benutzeroberfläche erweitern, Bedienelemente hinzufügen oder benötigte Skripte für die Frontendausgabe installieren. AddOns können komplexe Applikationen (Newssystem, Kalender, Bildbearbeitung) sein oder, im einfachsten Fall, zusätzliche PHP-Klassen im System bereitstellen (z. B.: PDF-Umwandlung, E-Mail-Verschlüsselung, URL-Schemata, u.v.m.).

Selbst ein großer Teil der Grundfunktionen von REDAXO wird als AddOns bereitgestellt (Core-AddOns). Dadurch können diese Core-AddOns leicht aktualisiert und ggf. durch individuelle Lösungen ausgetauscht werden.

> AddOns in REDAXO sind vergleichbar mit den in anderen CMSs verfügbaren Plugins oder Extensions.

Einige AddOns liefern eigene PlugIns mit, das sind quasi "Unter-AddOns eines AddOns". Diese können die AddOns modular um weitere Funktionen erweitern. Plugins werden im Normalfall nur mit dem AddOn ausgeliefert.

<a name="included"></a>

## Im Lieferumfang enthaltene AddOns

REDAXO bringt bereits bei der Installation einige AddOns und PlugIns mit:

| AddOn           | PlugIn                                                                  | Beschreibung                                                                               |
|-----------------|-------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|
| backup          |                                                                         | Erstellung und Wiederherstellung von Backups                                               |
| be_style        |                                                                         | AddOn für die Backenddarstellung                                                           |
| redaxo          | Liefert das Default-Design des Backend                                  |                                                                                            |
| customizer      | Liefert Erweiterungen (Code-Higlightning, Link zum Frontend, Einfärbung |                                                                                            |
| cronjob         |                                                                         | Ausführung regelmäßiger, geplanter Aufgaben                                                |
| article_status  | Ändert den Online-Status entsprechend Meta-Angabe                       |                                                                                            |
| optimize_tables | Optimiert die Datenbanktabellen                                         |                                                                                            |
| install         |                                                                         | Veröffentlichung und Download von AddOns                                                   |
| media_manager   |                                                                         | Ausgabe und Manipulation von Medien                                                        |
| mediapool       |                                                                         | Medienverwaltung                                                                           |
| metainfo        |                                                                         | Stellt Metafelder im System zur Vefügung                                                   |
| phpmailer       |                                                                         | Bindet die PHPMailer-Klasse ein für den Versand von E-Mails                                |
| project         |                                                                         | Ein leeres AddOn, um eigene Projekt-spezifische Funktionen zu integrieren (*updatesicher*) |
| structure       |                                                                         | Liefert die Strukturverwaltung für Kategorien und Artikel                                  |
| content         | Stellt die Funktionen zur Inhaltsbearbeitung bereit                     |                                                                                            |
| history         | Versionierung von Artikeln                                              |                                                                                            |
| version         | Ergänzt eine Arbeitsversion der Website                                 |                                                                                            |
| users           |                                                                         | Benutzer- und Rollenverwaltung                                                             |

<a name="addons"></a>

## AddOn-Verwaltung

Die AddOn-Verwaltung, im Hauptmenü unter **AddOns** zu finden, liefert die Funktionen zur Installation, Deinstallation und Aktivierung von AddOns und PlugIns sowie Informationen zum Namen und Links zu Hilfeseiten. Mit Klick auf das Fragezeichen (siehe weiter unten) erhält man oft eine ausführliche Dokumentation des jeweiligen AddOns.

> Die AddOn-Verwaltung **ist kein Download-Katalog**.

<a name="upload"></a>

## Upload

Bevor ein AddOn installiert werden kann, muss dieses hochgeladen werden. Dies kann manuell durch FTP erfolgen; der schnellste und bequemste Weg, neue AddOns in das System zu laden, ist jedoch der Download über den **Installer**.

**Weitere AddOn-Quellen sind:**

* AddOn-Bereich auf [www.redaxo.org](https://redaxo.org/download/addons/) (Identisch mit Installer)
* GitHub-Repositories
* Die Agentur, bzw. Dienstleister der Website

Nachfolgend werden gängige Upload-Methoden aufgelistet:

<a name="upinstaller"></a>

### Upload per Installer

Siehe: [Installer](/{{path}}/{{version}}/installer)

<a name="upftp"></a>

### Manueller Upload per (S)FTP

* Download des AddOns als ZIP
* Entpacken des ZIP
* ggf. README.md beachten, sofern vorhanden
* Upload in den Ordner `/redaxo/src/addons/` 

> Der Ordner-Name des AddOs sollte identisch mit dem AddOn-Key sein, der in der darin befindlichen package.yml hinterlegt ist.

<a name="github"></a>

### AddOns aus GitHub

Soweit möglich, sollte man nicht das aktuelle Github-Repository herunterladen. Hierbei handelt es sich meist um Entwicklungsversionen, die nicht für den produktiven Einsatz gedacht sind. Für den produktiven Einsatz sollte man immer auf ein aktuelles Release zurückgreifen. Vorher empfiehlt es sich, auch die dort hinterlegten Issues beachten. In manchen Fällen kann es jedoch auf Github bereits eine Fehlerbereinigte Version geben, die noch nicht auf www.redaxo.org veröffentlicht ist.

<a name="install"></a>

## AddOn-Installation

Nach dem erfolgten Download über den Installer, bzw. manuellem Upload, können die AddOns in der AddOn-Verwaltung (Menüpunkt: `AddOns` ) installiert werden.

> Neben der Versionsnummer findet man ein Fragezeichen ( `?` ). Hier erhält man meist nützliche Informationen zur Installation und zur Benutzung. Es empfiehlt sich, diese vor der Installation zu lesen.

Durch einen Klick auf `installieren` wird das AddOn installiert. Hierbei werden die nötigen Schritte (z. B. Kopieren von CSS- und JS-Dateien, Anlegen von Datenbanken) durchgeführt, damit das AddOn verwendet werden kann. Nach erfolgter Installation wird das AddOn aktiviert und kann anschließend verwendet werden.

<a name="update"></a>

## Update

Wenn das AddOn im *Installer* gelistet ist, kann es über diesen schnell und unkompliziert aktualisiert werden.
Weitere Informationen im Abschnitt: [Installer](/{{path}}/{{version}}/installer). Möchte man ein Update manuell durchführen, reicht häufig das Ersetzen des AddOn-Ordners durch den neuen Ordner und ein anschließender Aufruf der Reinstall-Funktion in der AddOn-Verwaltung.

> Bei einem Update sollten immer die Hinweise im Installer oder einer evtl. vorhandenen README beachtet werden. Ein vorheriges Backup wird empfohlen.

<a name="reinstall"></a>

## Reinstallieren / Reparatur

Sollte es mal zu einem Problem mit dem AddOn kommen (evtl. nach einem Update), kann man das AddOn reinstallieren. Hierbei wird das AddOn erneut installiert und Einstellungen und Dateien werden ggf. korrigiert.

Konkret werden vom Core die Bedingungen aus der package.yml neu geprüft, `install.php` und anschließend `install.sql` werden geladen und die Assets werden frisch kopiert.

> Bei einem Reinstall sollten keine Daten oder Einstellungen verloren gehen. Da einzelne AddOns aber von dieser Regel abweichen könnten, bitte die Hinweise in der jeweiligen AddOn-Dokumentation beachten.

<a name="uninstall"></a>

## Deinstallation / Löschen

Möchte man ein AddOn deinstallieren, klickt man auf `de-installieren` . Möchte man das AddOn komplett löschen, klickt man auf `löschen` .

Konkret werden vom Core `uninstall.php` und anschließend `uninstall.sql` geladen; die Assets sowie die Einträge aus `rex_config` werden gelöscht.

> Hinweis:

Bei einer Deinstallation sollte das AddOn oder das PlugIn normalerweise seine angelegten Dateien und Tabellen vollständig entfernen. Einige AddOns weichen jedoch bewusst von dieser Regel ab. Zum Beispiel löscht yForm seine eigenen Tabellen, aber nicht die eigentlichen Datentabellen. Auch das Backup-AddOn löscht bewusst nicht die angelegten Backups im data-Ordner. Daher bitte die Hinweise in der jeweiligen AddOn-Dokumentation beachten.

<a name="console"></a>

## Konsolen-Befehle

<a name="downconsole"></a>

### Download per Konsole

AddOns können auch über die Konsole geladen werden. Das Kommando lautet:

`php redaxo/bin/console install:download <addonkey> <version>` 

Beispiel:

``` 
redaxo/bin/console install:download yform
```

> Wird die Version nicht angegeben, wird eine Auswahl bereitgestellt.

<a name="conlist"></a>

### Liste aller verfügbaren AddOns

Command `install:list` .

Listet alle verfügbaren AddOns von redaxo.org auf und zeigt die installierte Version dazu an.

``` 
redaxo/bin/console install:list
```

Options:

* `--search` - Filtert die Liste anhand eines Suchbegriffs (vgl. Filterung/Suche im Backend)
* `--updates-only` - Zeigt nur AddOns an, für die ein Update verfügbar ist.
* `--json` - Gibt die Ausgabe als json string (für z. B. verarbeitung in skripten)

<a name="conupdate"></a>

### AddOn-Update

Command `install:update` updated ein AddOn mit Updates von redaxo.org.

``` 
redaxo/bin/console install:update <addonkey> <version>:
```

* addonkey: z. B. "yform"
* version: z. B. "1.2.3"

Die Versionsangabe ist optional, wenn keine angegeben ist, werden mögliche Versionen zur Auswahl gestellt (gleich wie im Backend auch sind).

<a name="condelete"></a>

### Löschen eines AddOns

`redaxo/bin/console package:delete <package-id>` 

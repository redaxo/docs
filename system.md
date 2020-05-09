# System

* [Einstellungen (und Features)](#settings)
* [Sprachen](#lang)
* [Logdateien](#log)
* [Systembericht](#bericht)
* [Customizer](#custom)
* [Historie](#historie)

<a name="settings"></a>

## Einstellungen

Im Tab Einstellungen werden die grundlegenden Daten zur Konfiguration des Systems und für die Website erfasst.

* URL der Website
* Name der Website
* Backendsprache
* E-Mail-Adresse bei Fehlern
* E-Mail-Benachrichtigung bei Fehlern (wenn PHPMailer-AddOn aktiviert)
* Startartikel
* Fehlerartikel
* Standard-Template
* Editor-Integration

Die Einstellungen werden ggf. von installierten AddOns erweitert und bieten dann weitere Optionen.

Im Panel **Features** stehen folgende Funktionen zur Verfügung:

### Cache Löschen

Templates und Sprachdateien werden erstellt, Artikelcache wird gelöscht. Sobald ein Artikel im Frontend aufgerufen wird, wird der Cache des/der entsprechenden Artikels/Kategorie wieder erstellt. *Sollte nur gestartet werden, wenn ein Problem vorliegt*

### Debug-Modus aktivieren

Mit dem Debug-Modus werden bei PHP-Skriptfehlern im Frontend und Backend zusätzliche Angaben zum Fehler ausgegeben. Außerdem werden keine immutable cache-http-header verwendet. Der Debug-Modus sollte im Live-Betrieb nicht aktiviert werden, da die Fehlermeldungen auch sensible Daten beinhalten können, darüber hinaus wird die Webpräsenz auf noindex gesetzt.  

### Safe mode aktivieren

Im Safe mode werden vorübergehend alle AddOns deaktiviert. Falls bspw. ein AddOn nach der Installation Probleme macht, kann dieses über den Safe mode deaktiviert oder deinstalliert werden.

### Setup

Hier kann das Setup erneut gestartet werden. Es kann dafür verwendet werden eine defekte Installation im **Notfall** zu reparieren, das Passwort des Admins zurückzusetzen oder nötige Konvertierungsaufgaben nach einem größeren Update durchzuführen (z. B. [Aktualisierung der Datenbank auf utf8mb4](/{{path}}/{{version}}/aktualisierung#utf8mb4))  

<a name="lang"></a>

## Sprachen

REDAXO unterstützt mehrere Sprachen. Im Reiter Sprachen können diese angelegt und verwaltet werden. Weitere Informationen zum Thema im Kapitel: [Mehrsprachigkeit](/{{path}}/{{version}}/mehrsprachigkeit).

<a name="log"></a>

## Logdateien

Hier werden zentral die Log-Dateien des Systems und einiger AddOns zur Protokollierung und Fehleranalyse abgelegt.

<a name="bericht"></a>

## Systembericht

Der Systembericht informiert über die aktuelle Serverumgebung und installierte AddOns mit Angabe der Versionsnummer. Er kann als Markdown-Code heruntergeladen werden und so für den Support in GitHub und Slack anderen Nutzern bereitgestellt werden. Die Daten selbst sind so weit bereinigt, dass sie keine Informationen über die Server IP und Datenbanknamen verraten.

<a name="custom"></a>

## Customizer (sofern installiert)

Der Customizer stellt Optionen zur Individualisierung des Backends zur Verfügung. Darüber hinaus stellt er für Entwickler CodeMirror zur komfortablen Darstellung von Code zur Verfügung.

<a name="historie"></a>

## Historie (sofern installiert)

Ist das History-Plugin der Struktur installier, kann die Historie hier gelöscht werden.

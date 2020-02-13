# System

- [Einstellungen (und Features)](#settings)
- [Sprachen](#lang)

<a name="settings"></a>
## Einstellungen

Im Tab Einstellungen werden die grundlegenden Daten zur Konfiguration des Systems erfasst. 

- Url der Website
- Name der Website 
- Backendsprache
- E-Mail-Adresse bei Fehlern
- E-Mail-Benachrichtigung bei Fehlern (wenn PHPMailer Addon aktiviert) 
- Startartikel
- Fehlerartikel
- Standardtemplate
- Editor-Integration

Die Einstellungen werden ggf. von installieren AddOns erweitetert und bieten dann weitere Optionen. 

Im Panel Features stehen folgende Funktionen zur Verfügung

### Cache Löschen

Templates und Sprachdateien werden erstellt, Artikelcache wird gelöscht. Sobald ein Artikel im Frontend aufgerufen wird, wird der Cache des/der entsprechenden Artikels/Kategorie wieder erstellt.

### Debug-Modus aktivieren

Mit dem Debug-Modus werden bei PHP-Skriptfehlern im Frontend und Backend zusätzliche Angaben zum Fehler ausgegeben. Ausserdem werden keine immutable cache-http-header verwendet. Im Live-Betrieb nicht aktivieren, da die Fehlermeldungen auch sensible Daten beinhalten können.

### Safe mode aktivieren

Im Safe mode werden vorübergehend alle AddOns deaktiviert. Falls bspw. ein AddOn nach der Installation Probleme macht, kann dieses über den Safe mode deaktiviert oder deinstalliert werden.

### Setup

Hier kann das Setup erneut gestartet werden. Es kann dafür verwendet werden eine defekte Installation im **Notfall** zu reparieren, das Passwort des Admins zurückzusetzen oder nötige Konvertierungsaufgaben nach einem größeren Update durchzuführen.  

<a name="lang"></a>
## Sprachen

REDAXO unterstützt mehrere Sprachen. Im Reiter Sprachen können diese angelegt und verwaltet werden. Weitere Informationen zum Thema im Kapitel: [Mehrsprachigkeit](/{{path}}/{{version}}/mehrsprachigkeit. 

<a name="log"></a>
## Logdateien

Hier werden zentral die Log-Dateien des Systems und einiger AddOns abgelegt. 

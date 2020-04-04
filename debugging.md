# Fehlerbehebung und Debugging

Auch eine REDAXO-Installation kann einmal „Schluckauf“ haben. Im Folgenden werden Möglichkeiten aufgezeigt, deine REDAXO-Installation zu reparieren.

> **Hinweis:** Wir empfehlen auch vor einem Fehler, regelmäßige Backups zu erstellen. Datenbank-Backups können automatisiert über das Cronjob-Addon erstellt werden.

## Fehleranalyse: Whooops und Oooops

**Hier Screenshots Ooops, Rooaaar einfügen**

Tritt ein Fehler auf, meldet REDAXO sich standardmäßig im Frontend mit einem Oooops und im Backend mit einem Rrrrroar.

**Hier Screenshots Whooops einfügen**

Wenn ein Administrator eingeloggt ist, oder der Administrator den  Debug-Modus aktiviert hat, wird anstelle des Oooops ein Whoooops mit genauerer Fehlerbeschreibung und Stacktrace ausgegeben.

## Fehleranalyse: Die system.log-Datei

**Hier Screenshot einfügen**

In der Datei `redaxo/data/core/system.log` werden Fehler geloggt - möglicherweise ist der Fehler bereits dabei.

## Debugging: Das debug-Addon

**Hier Screenshot einfügen**

Neu in REDAXO 5.11 ist das Debug-Addon, welches im Backend zusätzlich aktiviert werden kann. Es erscheint ein neuer Menüpunkt, in dem Clockwork gestartet wird. Jeder weitere Aufruf im Frontend oder Backend übergibt an Clockwork Debugging-Informationen.


## Debugging: Einstellungen in der `config.yml`

In der Datei `redaxo/data/core/config.yml` können Parameter zum Debugging aktiviert werden. Der Debug-Modus sollte ausschließlich nur dann aktiviert werden, wenn die Website nicht öffentlich erreichbar ist.

## Fehler: Google indexiert die Seite nicht, alle Seiten werden als noindex markiert.

Möglicherweise ist der Debug-Modus aktiviert. Der Debug-Modus sollte ausschließlich nur dann aktiviert werden, wenn die Website nicht öffentlich erreichbar ist.

## Fehler: REDAXO funktioniert nach einem Website-Umzug nicht mehr

* Ist sichergestellt, dass alle Dateien erfolgreich kopiert wurden?
* Stimmt die PHP-Version?
* Wurden die Datenbank-Zugangsdaten angepasst?
* Sind alle Einstellungen am Paket
* Wurde die .htacess-Datei übernommen oder neu gesetzt oder sind Anpassungen dort nötig?

## Fehler: Ich kann mich nicht mehr einloggen

Möglicherweise wurde das Passwort geändert oder der Benutzer existiert nicht mehr. Oder: Möglicherweise wurde ein Backup eingespielt, das die Tabelle `rex_user` nicht beinhaltet hat oder überschrieben hat. 

* Lösung 1: Ggf. das Setup starten, um den Administrator erneut anzulegen.
* Lösung 2: Über die REDAXO-Console einen neuen Benutzer erstellen

Ein Login ist auch nicht mehr möglich, wenn der Speicherplatz des Hosting-Pakets voll ist und die PHP-Session daher nicht gestartet werden kann.

## Weitere Fehler und Lösungen aus der REDAXO-Community

### Fehler: Installer kann keine Addons abrufen

Stelle sicher, dass `https://www.redaxo.org/de/ws/` über eine Socket-Verbindung erreichbar ist.

### Fehler: Pjax-Formulare im Backend speichern nicht

Wird beim Speichern in einem Modul oder Template im Backend ein 403-Fehler gemeldet, ist evtl. `mod_security` beim Webspace aktiviert.

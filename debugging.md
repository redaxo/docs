# Fehlerbehebung und Debugging
- Fehleranalyse
    - [Whooops und Oooops](#ooops)
    - [Die `system.log`-Datei](#systemlog)
- Debugging
    - [Einstellungen in der `config.yml`](#configyml)    
    - [Das debug-Addon](#debugaddon)
    - [Entwicklertools des Browsers](#browser)
- Fehler
    - [Google indexiert die Seite nicht, alle Seiten werden als noindex markiert.](#googleindex)
    - [REDAXO funktioniert nach einem Website-Umzug nicht mehr](#moved)
- Weitere Fehler und Lösungen aus der REDAXO-Community
    - [Installer kann keine Addons abrufen](#installer)
    - [Pjax-Formulare im Backend speichern nicht](#pjax)
    - [Ich kann mich nicht mehr einloggen](#login)


Auch eine REDAXO-Installation kann einmal „Schluckauf“ haben. Im Folgenden werden Möglichkeiten aufgezeigt, deine REDAXO-Installation zu reparieren.

> **Hinweis:** Wir empfehlen auch vor einem Fehler, regelmäßige Backups zu erstellen. Datenbank-Backups können automatisiert über das Cronjob-Addon erstellt werden.

<a name="ooops"></a>
## Fehleranalyse: Whooops und Oooops

![Ooops](/assets/v5.10.0-debug_ooops.png)

Tritt ein Fehler auf, meldet REDAXO sich im Frontend mit einem Oooops und im Backend mit einem Rrrrroar.

![Whoops](/assets/v5.10.0-debug_whooops.png)

Wenn ein Administrator eingeloggt ist, oder der Administrator den  Debug-Modus aktiviert hat, wird anstelle des Oooops ein Whoooops mit genauerer Fehlerbeschreibung und Stacktrace ausgegeben.

<a name="systemlog"></a>
## Fehleranalyse: Die `system.log`-Datei

![Screenshot /System/Logdateien](/assets/v5.10.0-debug_syslog.png)

In der Datei `redaxo/data/core/system.log` werden Fehler geloggt - möglicherweise ist der Fehler bereits dabei. Diese wird auch unter `System > Logdateien` angezeigt.

<a name="configyml"></a>
## Debugging: Einstellungen in der `config.yml`

In der Datei `redaxo/data/core/config.yml` können Parameter zum Debugging aktiviert werden. Der Debug-Modus sollte ausschließlich nur dann aktiviert werden, wenn die Website nicht öffentlich erreichbar ist.

<a name="debugaddon"></a>
## Debugging: Das debug-Addon

![Debug-AddOn ab REDAXO 5.11](/assets/v5.11.0-debug_addon.png)

Das Debug-Addon, welches zusätzlich installiert werden kann. Es erscheint ein neuer Menüpunkt, in dem Clockwork gestartet wird. Jeder weitere Aufruf im Frontend oder Backend übergibt an Clockwork Debugging-Informationen.

<a name="browser"></a>
## Debugging: Entwicklertools des Browsers

![Safari Netzwerk/Serververhalten](/assets/v5.10.0-browser_network.png)

In Desktop-Browsern befindet sich in den Entwickler-Tools ein "Netzwerk"-Reiter, in welchem REDAXO bei aktiviertem Debug-Modus zusätzliche Performance-Informationen ausgibt, die über `rex_timer` gemessen werden.

<a name="googleindex"></a>
## Fehler: Google indexiert die Seite nicht, alle Seiten werden als noindex markiert.

Möglicherweise ist der Debug-Modus aktiviert. Der Debug-Modus sollte ausschließlich nur dann aktiviert werden, wenn die Website nicht öffentlich erreichbar ist.

<a name="moved"></a>
## Fehler: REDAXO funktioniert nach einem Website-Umzug nicht mehr

* Ist sichergestellt, dass alle Dateien erfolgreich kopiert wurden?
* Stimmt die PHP-Version?
* Wurden die Datenbank-Zugangsdaten angepasst?
* Sind alle Einstellungen am Paket korrekt, z.B. Domain, A-Record, Verzeichnispfad, etc.?
* Wurde die .htaccess-Datei übernommen oder neu gesetzt oder sind Anpassungen dort nötig?
* Wurde das Setup erneut ausgeführt oder zumindest der Cache gelöscht?

<a name="login"></a>
## Fehler: Ich kann mich nicht mehr einloggen

Möglicherweise wurde das Passwort geändert oder der Benutzer existiert nicht mehr. Oder: Möglicherweise wurde ein Backup eingespielt, das die Tabelle `rex_user` nicht beinhaltet hat oder überschrieben hat. 

* Lösung 1: Ggf. das Setup starten, um den Administrator erneut anzulegen.
* Lösung 2: [Das Passwort des Administrators zurücksetzen.](https://redaxo.org/doku/master/passwort-vergessen)
* Lösung 3: Über die REDAXO-Console einen neuen Benutzer erstellen oder das Passwort eines bestehenden Benutzers zurücksetzen: `console user:set-password <username> <neues-passwort>`

Ein Login ist auch nicht mehr möglich, wenn der Speicherplatz des Hosting-Pakets voll ist und die PHP-Session daher nicht gestartet werden kann.

<a name="community"></a>
## Weitere Fehler und Lösungen aus der REDAXO-Community

<a name="installer"></a>
### Fehler: Installer kann keine Addons abrufen

Stelle sicher, dass `https://www.redaxo.org/de/ws/` über eine Socket-Verbindung erreichbar ist.

<a name="pjax"></a>
### Fehler: Pjax-Formulare im Backend speichern nicht

Wird beim Speichern in einem Modul oder Template im Backend ein 403-Fehler gemeldet, ist evtl. `mod_security` oder `fail2ban` beim Webspace aktiviert.

Für `mod_security` testweise nur auf "Erkennung und protokollieren" einstellen.

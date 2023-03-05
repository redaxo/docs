# Fehlerbehebung und Debugging

* Fehleranalyse
  + [Whoops und Ooops](#ooops)
  + [Die `system.log` -Datei](#systemlog)
* Debugging
  + [Der Debug-Mode](#debugmode)
  + [Die Funktion `dump()` ](#dump)
  + [Einstellungen in der `config.yml` ](#configyml)
  + [Das debug-AddOn](#debugaddon)
  + [Entwicklertools des Browsers](#browser)
* Fehler
  + [Google indexiert die Seite nicht, alle Seiten werden als noindex markiert.](#googleindex)
  + [REDAXO funktioniert nach einem Website-Umzug nicht mehr](#moved)
* Weitere Fehler und Lösungen aus der REDAXO-Community
  + [Installer kann keine AddOns abrufen](#installer)
  + [Die Bearbeiten-Ansicht eines Artikels führt zu einem Fehler](#cture-edit-error)
  + [Pjax-Formulare im Backend speichern nicht](#pjax)
  + [Ich kann mich nicht mehr einloggen](#login)

Auch eine REDAXO-Installation kann einmal „Schluckauf“ haben. Im Folgenden werden Möglichkeiten aufgezeigt, deine REDAXO-Installation zu reparieren.

Im Rahmen einer REDAXOHour ist eine Video Einführung entstanden, die viele Punkte dieses Kapitels erklärt.

<a class="button-secondary" href="https://www.youtube.com/watch?v=mpiI9ucTUSo">Zum Video bei YouTube</a>

> **Hinweis:** Wir empfehlen auch vor einem Fehler, regelmäßige Backups zu erstellen. Datenbank-Backups können automatisiert über das Cronjob-AddOn erstellt werden.

<a name="ooops"></a>

## Fehleranalyse: Whoops und Ooops

Ein Ooops oder Whoops wird ausgegeben, wenn es zu einem kritischen Fehler gekommen ist, z.B. einem `E_ERROR`. Mit aktiviertem Debug-Modus auch bei `E_WARNING`, `E_NOTICE`.

Wenn ein Administrator eingeloggt ist, oder der Administrator den Debug-Modus aktiviert hat, wird anstelle des Ooops ein Whoops mit genauerer Fehlerbeschreibung und Stacktrace ausgegeben, um die Fehlersuche zu vereinfachen.

![Ooops](/assets/v5.10.0-debug_ooops.png) Allgemeine Ooops-Fehlerseite im Frontend (links) und im Backend (rechts)

> Tritt ein Fehler auf, meldet REDAXO sich im Frontend mit einem Ooops und im Backend mit einem Rrrrroar.

![Whoops](/assets/v5.10.0-debug_whooops.png) Whoops-Fehlerseite mit Debug-Informationen

Die Whoops-Meldung liefert die Codestellen und Fehlermeldungen zum aufgetretnenen Fehler. Die Infos können zudem kopiert werden. 

Mit dem 'Report a bug Button' auf der Whoops Fehlerseite kann, falls erforderlich direkt ein Issue im REDAXO GitHub-Repo angelegt werden. **Bitte nur verwenden, wenn man sich sicher ist, dass es sich um einen Bug im Core handelt**.  


<a name="systemlog"></a>

## Fehleranalyse: Die **system.log**-Datei

![Screenshot /System/Logdateien](/assets/v5.10.0-debug_syslog.png)

In der Datei `redaxo/data/core/system.log` werden Fehler geloggt - möglicherweise ist der Fehler bereits dabei. Diese wird auch unter `System > Logdateien` angezeigt.

<a name="dump"></a>

## Debugging: Die Funktion **dump()**

![Aktivierter Debug-Modus](/assets/v5.10.0_debug_dump.png)

Ergebnis einer dump()-Ausgabe

Anstelle von `var_dump()` kann im REDAXO-Kontext die Funktion `dump()` verwendet werden, um die Ausgabe einer Variablen, eines Objekts oder eines anderen Datentyps im Frontend auszugeben. Der Vorteil besteht darin, dass die Ausgabe HTML-formatiert ist und dadurch schneller erfasst und durchsucht werden kann.

### Suchen in einem Dump: 

Wenn der ausgewertete Inhalt komplex ist, sollte man das lokale Suchfeld verwenden, um nach bestimmten Variablen oder Werten zu suchen. Hierzu klickt man auf eine beliebige Stelle im Dump-Inhalt und drückt dann `Strg. + F` oder `Cmd. + F`, damit das lokale Suchfeld erscheint. Alle gängigen Tastenkombinationen zur Navigation in den Suchergebnissen werden unterstützt (Strg + G oder Cmd + G, F3 usw.) Nach Abschluss der Suche lässt sich das Feld mit Esc wieder ausblenden.


<a name="debugmode"></a>

## Debugging: Der Debug-Modus

![Aktivierter Debug-Modus](/assets/v5.10.0_debug.png)

Woran erkennt man, dass der Debug-Modus eingeschaltet ist?

Im Debug-Modus werden zur Laufzeit weitere Informationen gesammelt und im Fehlerfall ausgegeben. Exceptions werden als Whoops ausgegeben und helfen so dem Entwickler, Fehler zu beseitigen und Probleme zu erkennen.

Der Debug-Modus kann über die config.yml verschärft werden: über die Eigenschaft `throw_always_exception: true` werden auch einfache `Notices` (`E_WARNING`, `E_NOTICE`) als Whoops ausgegeben. Die Vorteile liegen auf der Hand: So wird man bei der Entwicklung von Modulen, Templates oder AddOn-Code u.a. frühzeitig darauf aufmerksam, wenn Methoden und Funktionen in PHP verwendet werden, die bereits als `deprecated` markiert und bei einem Update der PHP-Version zu Fehler führen werden.

Der Debug-Modus darf unter keinen Umständen aktiviert werden, wenn die Website öffentlich zugänglich ist. Denn der Debug-Modus ist öffentlich und nicht nur eingeloggte Administratoren erhalten eine Fehlermeldung und die darin exponierten Informationen.

Wir empfehlen, die Seite vorher durch einen `.htpasswd` -Verzeichnisschutz o.ä. zu schützen oder zumindest in einen Wartungsmodus zu versetzen, bspw. durch das AddOn `maintenance` . Zum Schutz von Entwickler und Betreiber werden im Debug-Modus alle header auf `noindex` gesetzt, um auch Suchmaschinenen daran zu hindern, sensible Daten durch die Debug-Ausgabe in den Suchmaschinen-Index aufzunehmen.

### Konsole

**Aktivieren**

`php redaxo/bin/console config:set debug.enabled true --type bool`

**Deaktivieren**

`php redaxo/bin/console config:set debug.enabled false --type bool`


<a name="configyml"></a>

## Debugging: Einstellungen in der **config.yml**

In der Datei `redaxo/data/core/config.yml` können Parameter zum Debugging aktiviert werden. Der Debug-Modus sollte ausschließlich nur dann aktiviert werden, wenn die Website nicht öffentlich erreichbar ist.

<a name="debugaddon"></a>

## Debugging: Das debug-AddOn (ab REDAXO 5.11)

Das Debug-AddOn kann zusätzlich installiert werden kann und anschließend im Frontend und Backend verwendet werden. Es erscheint ein neuer Menüpunkt, in dem Clockwork gestartet wird. Jeder weitere Aufruf im Frontend oder Backend übergibt an Clockwork Debugging-Informationen.

> Das Debug-AddOn sollte nicht in Produktivumgebungen eingesetzt werden, weil hierfür der Debug-Modus im System aktiviert sein muss. Bei Multidomain-Umgebungen sollte man sich mit der gewünschten Domain im Backend einloggen, damit es unter der jeweiligen Domain eingesetzt werden kann.

![Debug-AddOn ab REDAXO 5.11](/assets/v5.11.0-debug_addon.png) Serverseitige Abläufe visualisiert durch Clockwork

Um eigene Messungen vornehmen zu können, kann die rex_timer-Klasse verwendet werden und den eigenen Code dazwischen einfügen:

```php
rex_timer::measure('Bezeichnung für Clockwork', function() {
    // lange und aufwändige Arbeit eines eigenen Code-Abschnittes einfügen und messen lassen.
});
```

[Weiterführende Infos zu rex_timer in den API Docs](https://friendsofredaxo.github.io/phpdoc/classes/rex-timer.html)

[REDAXOHours Vortrag zum Thema Whoops in REDAXO, und dem Neuen Debug Addon](https://www.youtube.com/watch?v=yYhXgTMuEf0)


<a name="browser"></a>

## Debugging: Entwicklertools des Browsers

![Safari Netzwerk/Serververhalten](/assets/v5.10.0-browser_network.png)

In Desktop-Browsern befindet sich in den Entwickler-Tools ein "Netzwerk"-Reiter, in welchem REDAXO bei aktiviertem Debug-Modus zusätzliche Performance-Informationen ausgibt, die über `rex_timer` gemessen werden.

<a name="googleindex"></a>

## Fehler: Google indexiert die Seite nicht, alle Seiten werden als noindex markiert

Möglicherweise ist der Debug-Modus aktiviert. Der Debug-Modus sollte ausschließlich nur dann aktiviert werden, wenn die Website nicht öffentlich erreichbar ist.

<a name="moved"></a>

## Fehler: REDAXO funktioniert nach einem Website-Umzug nicht mehr

* Ist sichergestellt, dass alle Dateien erfolgreich kopiert wurden?
* Stimmt die PHP-Version? Siehe [Systemanforderungen](https://redaxo.org/download/core/).
* Wurden die Datenbank-Zugangsdaten angepasst?
* Sind alle Einstellungen am Webspace-Paket und der Domain korrekt, z. B. Domain, A-Record, Verzeichnispfad, etc.?
* Wurde die .htaccess-Datei übernommen oder neu gesetzt oder sind Anpassungen dort nötig?
* Wurde das Setup erneut ausgeführt oder zumindest der Cache gelöscht?

<a name="login"></a>

## Fehler: Ich kann mich nicht mehr einloggen

Möglicherweise wurde das Passwort geändert oder der Benutzer existiert nicht mehr. Oder: Möglicherweise wurde ein Backup eingespielt, das die Tabelle `rex_user` nicht beinhaltet hat oder überschrieben hat.

* Lösung 1: Ggf. das Setup starten, um den Administrator erneut anzulegen.
* Lösung 2: [Das Passwort des Administrators zurücksetzen.](https://redaxo.org/doku/main/passwort-vergessen)
* Lösung 3: Über die REDAXO-Konsole einen neuen Benutzer erstellen oder das Passwort eines bestehenden Benutzers zurücksetzen: `console user:set-password <username> <neues-passwort>` 

Ein Login ist auch nicht mehr möglich, wenn der Speicherplatz des Hosting-Pakets voll ist und die PHP-Session daher nicht gestartet werden kann.

<a name="community"></a>

## Weitere Fehler und Lösungen aus der REDAXO-Community

<a name="installer"></a>

### Fehler: Installer kann keine AddOns abrufen

Stelle sicher, dass `https://www.redaxo.org/de/ws/` über eine Socket-Verbindung erreichbar ist. Möglicherweise hat der Hoster ausgehende Socket-Verbindungen blockiert, oder verwendet keinen aktuellen Zertifikatsspeicher. Dies kann auch im Zuge einer PHP-Versionsumstellung passieren.

<a name="structure-edit-error"></a>

### Fehler: Die Bearbeiten-Ansicht eines Artikels führt zu einem Fehler

Möglicherweise ist ein Modul oder der Inhalt eines Blocks defekt und löst einen Fehler aus. Mögliche Lösungsansätze:

* Den betroffenen Modulcode im Menü `Module` auf Fehler überprüfen oder
* Im Zweifel über die Datenbank den betroffenen Block in der Tabelle `rex_article_slice` entfernen und den REDAXO-Cache löschen.

<a name="pjax"></a>

### Fehler: Pjax-Formulare im Backend speichern nicht

Wird beim Speichern in einem Modul oder Template im Backend ein 403-Fehler gemeldet, ist evtl. `mod_security` oder `fail2ban` beim Webspace aktiviert.

Für `mod_security` testweise nur auf "Erkennung und protokollieren" einstellen.

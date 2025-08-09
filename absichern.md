# REDAXO absichern

* [Live-Mode](#livemode)
* [Security-AddOn](#securityaddon)

<a name="livemode"></a>

## Live-Mode
Dieser Modus ist dafür konzipiert, die Sicherheit von Live-Systemen zu erhöhen, indem er die Möglichkeiten zur Ausführung von PHP-Code und bestimmten Systemänderungen durch Backend-Admins einschränkt. Der Live-Mode kann durch eine Einstellung in der `config.yml` manuell aktiviert werden.

> Bei Nutzung einer Deployment-Lösung oder alternativer lokaler Entwicklung sollte dies als obligatorisch angesehen werden. 

### Aktivierung des Live-Modes

Der Live-Mode kann in der `config.yml` aktiviert werden. Der Default-Wert ist: `false` 

```yaml
live_mode: true
```

Alternativ ist auch eine Änderung des Modus per PHP möglich. 

```php
if (rex::isBackend())
{ 
    rex_extension::register('PACKAGES_INCLUDED', static function (rex_extension_point $ep) {
        rex::setProperty('live_mode', true);
    }, rex_extension::EARLY);  
}
```

Nach der Aktivierung des Live-Modes werden verschiedene Sicherheitsmaßnahmen wirksam, die dazu beitragen, das System gegen Missbrauch zu sichern, insbesondere wenn ein Backend-Admin-Account kompromittiert wurde.

### Auswirkungen des Live-Modes

Im Live-Mode werden folgende Änderungen wirksam:

- **Safe-Mode und Debug-Mode**: Diese Modi sind immer deaktiviert, um die Ausführung unsicherer oder für die Fehlersuche gedachter Operationen zu verhindern.
- **System-Page Anpassungen**: Buttons für den Debug-Modus, Safe-Mode und das Setup verschwinden, um die Möglichkeit zur Systemkonfiguration zu limitieren.
- **Error-Handling**: Statt des detaillierten Whoops-Fehlerbildschirms erhalten Administratoren die allgemeinere Ooops-Seite.
- **Eingeschränkte Backend-Funktionen**: Die Seiten für Backup-Import, Addonverwaltung, Installer, Metainfoverwaltung, MediaManager-Verwaltung, Debugging, Module- und Template-Verwaltung werden ausgeblendet.
- **PHP-Code Ausführung**: Die Ausführung von PHP-Code über `REX_VALUE[id=X output=php]` wird unterbunden, und es wird eine Warnmeldung im Backend angezeigt.
- **Cronjob-Typen**: Die Ausführung und Anzeige von Cronjobs des Typs PHP-Code und PHP-Callback ist deaktiviert. Bestehende Jobs dieser Typen werden nicht mehr ausgeführt.
- **Metainfo-Callbacks**: Die Ausführung von Metainfo-Callbacks ist nicht möglich.

### Empfehlungen für Entwickler

Wer REDAXO-Websites im Live-Mode betreibt, sollte alternative Methoden für die Implementierung von Funktionalitäten, die PHP-Code erfordern, in Erwägung ziehen. Eigene Addons oder Plugins können für spezifische Anforderungen entwickelt werden, anstelle von direkter Eingabe von PHP-Code über das Backend.

<a name="securityaddon"></a>

## Security AddOn für REDAXO CMS

[Security-AddOn](https://github.com/FriendsOfREDAXO/Security) auf GitHub

Das AddOn ist nicht Teil der Grundinstallation. Es kann über den Installer installiert werden. 
Es bietet Wege das REDAXO-Backend mit verschiedenen Methoden zu sichern.

* Frontend-Passwort für Staging- oder Entwicklersysteme
* Fehlerberichterstattung per E-Mail. Direkt oder als gesammelte Pakete
* IP-Zugangskontrolle: IPs und IP-Bereiche zum Blockieren und Zulassen von Frontend und Backend
* BackendSession-Konfiguration: Sitzungsdauer, KeepAlivePing, maximale Sitzungsdauer
* Backend-Benutzerprotokoll: Protokollierung aller Aktionen der Backend-Benutzer
* Header-Sicherheit: Strict-Transport-security, X-Frame-Options, X-XSS-Protection ... (in Bearbeitung)
* Checkliste: Überprüfung der REDAXO-Installation auf Sicherheitsprobleme mit externen Tools.
* Linkliste mit nützlichen Seiten zum Prüfen der Website und des Backends.


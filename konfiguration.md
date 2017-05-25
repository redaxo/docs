# Konfiguration
- [rex_config](#rex_config)
- [Paketkonfiguration package_yml](#package_yml)
- [Konfiguration des Core](#core)
- [AddOn Konfiguration](#addon_config)


AddOn Entwickler können die Konfiguration der AddOns in der Tabelle `rex_config` ablegen und auslesen. Dateien im AddOn-, bzw. PlugIn-Ordner sollten nicht verändert werden, um automatische Updates zu ermöglichen. Konfigurationswerte können über die Klasse rex_config in der Datenbank gespeichert werden. Die Werte werden gecached:

<a name="rex_config"></a>
## rex_config

Hierbei gilt folgende Konvention:

namespace |key |value
------------- | ------------- | -------------
AddOn Key |Schlüssel |Wert

```
rex_config::set($addon, $key, $value);
$value = rex_config::get($addon, $key);

// alternativ über das Package-Objekt:
rex_addon::get($addon)->setConfig($key, $value);
$value = rex_addon::get($addon)->getConfig($key);

// oder falls das Package-Objekt über $this erreichbar ist (boot.php etc.):
$this->setConfig($key, $value);
$value = $this->getConfig($key);
``` 

<a name="package_yml"></a>
## package.yml

AddOn Entwickler haben die Möglichkeit, Konfigurationsparameter in der Datei `package.yml` abzulegen. Eine typische package.yml sieht z.B. so aus:

```
package: project
version: dev
author: Name des Autors
supportpage: www.redaxo.org/de/forum/

page:
    title: translate:titel des addons
    perm: media/hasMyPerm
    prio: 21
    icon: rex-icon rex-icon-[icon]
    subpages:
        subpage1:  { title: translate:subpage1_title }
        subpage2:  { title: translate:subpage2_title }

requires:
    redaxo: ^5.3.0

configvars:
    message_text1: translate:wert wird übersetzt
    meinevar: meinwert
    nocheinevar: nocheinwert
    nullwert:        
    einleererwert: ''
```

Die Syntax der yml-Datei ist recht einfach. Vor dem Doppelpunkt steht der Name der Config-Variablen, dahinter der Wert. Soll eine Config Variable als Array abgelegt werden, sind die einzelnen Arrayelemente eingerückt.

Die einzelnen Werte können über `rex_addon::get('addonname')->getProperty('varname'))` ausgelesen werden.

`rex_addon::get('project')->getProperty('author'))` gibt `Name des Autors`.


<a name="core"></a>
## Config core

Die Basiskonfiguration des Core ist im Verzeichnis src/data/core/config.yml abgelegt. Die Datei enthält unter anderem die Einstellungen zur Datenbank und Einstellungen, die im Bereich `System` im REDAXO Backend vorgenommen werden.

Ein Zugriff auf Einstellungen des Core ist über die Klasse `rex` möglich.

Funktion | Beschreibung | Beispiel
------------- | ------------- | -------------
rex::getServer() |Basis URL des Webservers für die Seite |https://www.example.com/
rex::getServerName() |Name der Website bzw. des Servers |Meine REDAXO Website
rex::getTablePrefix() |Tabellenprefix für Datentabellen |Standard: rex_
rex::getTempPrefix() |Prefix für temporäre Tabellen |Standard: tmp_
rex::getErrorEmail() |Error E-Mail Adresse |webmaster@example.com
rex::getDirPerm() |Wert für Zugriffsrechte, der beim Anlegen neuer Verzeichnisse durch das System verwendet wird |Standard: 0775
rex::getFilePerm() |Wert für Zugriffsrechte, der beim Anlegen neuer Dateien durch das System verwendet wird |Standard: 0664

Funktion | Beschreibung | Beispiel
------------- | ------------- | -------------
rex::getProperty('timezone') |Wert für die eingestellte Zeitzone |Standard: Europe/Berlin
rex::getProperty('lang') |Standardsprache des Backends |Standard: de_de
rex::getProperty('setup') |Setupmodus. true, wenn sich REDAXO im Setup Modus befindet |Standard: false
rex::getProperty('debug') |Debugmodus. true, wenn sich REDAXO im Debug Modus befindet |Standard: false
rex::getProperty('db') |Array der Datenbankparameter |
rex::getProperty('use_gzip') | |Standard: true
rex::getProperty('use_etag') | |Standard: true
rex::getProperty('use_last_modified') | |Standard: false
rex::getProperty('start_page') | |Standard: structure
rex::getProperty('socket_proxy') | |Standard: null
rex::getProperty('setup_addons') | |Standard: Array
rex::getProperty('system_addons') | |Standard: Array
rex::getProperty('use_accesskeys') | |Standard: true
rex::getProperty('accesskeys') | |Standard: Array

> **Hinweis:** auch die Werte der ersten Tabelle können über `getProperty` ermittelt werden. Z.B. `rex::getProperty('server')` entspricht `rex::getServer()`

<a name="addon_config"></a>
## AddOn Konfiguration

Über `dump(rex::getConfig())` kann man sich eine Übersicht ausgeben der aktuellen AddOn Konfiguration ausgeben lassen.
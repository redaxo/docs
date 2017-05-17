# Konfiguration

AddOn Entwickler können die Konfiguration der AddOns in der Tabelle `rex_config` ablegen und auslesen. Dateien im AddOn-, bzw. PlugIn-Ordner sollten nicht verändert werden, um automatische Updates zu ermöglichen. Konfigurationswerte können über die Klasse rex_config in der Datenbank gespeichert werden (werden gecached):

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


## Config core - rex



Konfig Addons

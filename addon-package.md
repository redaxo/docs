# package.yml

## Die package.yml definiert das AddOn oder PlugIn. 

Hier werden alle nötigen Einstellungen und Informationen hinterlegt, damit das AddOn oder PlugIn korrekt von REDAXO gefunden und ausgeführt werden kann. 
Die Verwendete Sprache ist das auf Markup verzichtende YAML.

> Es ist zu beachten, dass in YAML keine Tabs unterstützt werden. Die Einrückungen werden mit Leerzeichen realisiert. 

Die Definition erfolgt in Schlüssel-Wert-Paaren (key value pairs). Das Trennzeichen zwischen Schlüssel und Wert ist der Doppelpunkt. Die Zugehörigkeit zu Oberpunkten wird durch Einrückungen (per Leerzeichen) definiert.

## Pflichtfelder

Die nachfolgenden Felder sind die einzigen Pflichtfelder in der package.yml. Diese reichen aus um ein funktionsloses Addon zu erstellen. 

```yml
package: meinaddon 
version: '1.0.0' 
```
**package:** Hier wird der AddOnkey hinterlegt. Dieser sollte eindeutige und unverwechselbar sein. Damit es nicht zu Konflikten mit anderen AddOns gleicher Bezeichnung kommt, sollte der Key in MyREDAXO registriert sein. 

**version:** Hier wird die Version des AddOns hinterlegt. Damit der Installer die Versionen korrekt zuordnen kann, sollten die Vorgaben für [Semver](http://semver.org/lang/de/) eingehalten werden. 

Alle hier gesetzten Werte können über `$addon->getProperty($key)` abgefragt werden

```yml

package: demo_addon # Pflichtfeld
version: '1.0.0' # Pflichtfeld
title: Maintenance
author: Friends Of REDAXO
supportpage: https://github.com/FriendsOfREDAXO/demo_addon

# Seiten
page:
    title: 'translate:title' # Werte die mit `translate:` beginnen, werden anhand der Sprachdatei übersetzt. Der Addon-Präfix (hier `demo_addon_`) kann weggelassen werden.
    perm: admin # Seite ist nur für Admins erreichbar
    # Unterseiten
    subpages:
        main:
            title: 'translate:main'
            perm: demo_addon[] # Das AddOn stellt ein Benutzerrecht bereit, das aktiviert sein muss, um diese Unterseite zu erreichen. Admins haben alle Rechte.
        config:
            title: 'translate:config'
            perm: demo_addon[config] # Das noch spezifischer AddOn-Benutzerrecht 'config' ist für diese Unterseite erforderlich. Admins haben alle Rechte.
            icon: rex-icon fa-wrench # Icon von Font Awesome

# Abhängigkeiten
# Anforderungen ans System oder anderere AddOns, um dieses AddOn installieren oder update zu können
requires:
    redaxo: '^5.1' # benötigt mindestens REDAXO 5.1
    packages:
        media_manager: '^2.0.1' # benötigt mindestens das Addon Media Manager 2.0.1
    php:
        version: '>=5.6' # benötigt mindestens PHP 5.6
        extensions: [gd, xml] # benötigt die PHP-Extensions GDlib und XML

# Konflikte
# Verhindert die Installation und Updates, wenn AddOns die genannten Anforderungen erfüllen
# Siehe auch https://github.com/FriendsOfREDAXO/cache_warmup/pull/55#issuecomment-280906737
conflicts:
    packages:
        media_manager: '>=3' # Ist Media Manager in Version 3 vorhanden, führt das zum Konflikt mit diesem AddOn

```



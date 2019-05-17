# Package (package.yml) 

- [Beispiel einer package.yml](#beispiel)
- [Die package.yml definiert das AddOn oder PlugIn](#ueber)
- [Pflichtangaben](#pflicht)
- [Empfohlene Angaben](#empfohlen)
- [Abhängigkeiten (requires:)](#requires)
- [Konflikte (conflicts:)](#conflicts)
- [Dateien/Ordner ignorieren](#ignore)
- [Seiten (page: / subpages:)](#seiten)
  - [Seiten verstecken](#hidden)
  - [Seiten ohne Layout ausgeben](#haslayout)
- [Rechte (perm:)](#rechte)
- [Übersetzung](#uebersetzung)
- [Eigene Properties](#eigene)
- [PJAX deaktivieren](#pjax)
- [PlugIn](#plugin)

<a name="beispiel"></a>
## Beispiel einer package.yml

```yml
package: meinaddon 
version: '1.0.0' 
author: Rex Red
supportpage: https://meinesupportseite.tld
page:
    title: 'translate:Mein Addon'
    perm: meinaddon[]
    pjax: false
    icon: rex-icon fa-television
    subpages:
        main:  
             title: 'translate:main'
             icon: rex-icon fa-television
             eigener: extra
        help:  
             title: 'translate:help'
             icon: rex-icon fa-help
             eigener: default
        module: 
             title: 'translate:module' 
             perm: admin
requires:
    redaxo: '^5.1'
    packages:
        media_manager: '^2.0.1'
        addonname/pluginname: '^2.4.6'
conflicts:
    packages:
        irgendein_addon: '>=1.0.0'
```
<a name="ueber"></a>
## Die package.yml definiert das AddOn oder PlugIn 

In der package.yml werden alle nötigen Einstellungen und Informationen hinterlegt (das Package), damit das AddOn oder PlugIn korrekt von REDAXO gefunden und ausgeführt werden kann. 
Die verwendete Sprache ist das auf Markup verzichtende YAML.

> In YAML werden keine Tabs unterstützt. Die Einrückungen müssen mit Leerzeichen realisiert werden.

Die Definition erfolgt in Schlüssel-Wert-Paaren (key value pairs). Das Trennzeichen zwischen Schlüssel und Wert ist der Doppelpunkt. Die Zugehörigkeit zu Oberpunkten wird durch Einrückungen (per Leerzeichen) definiert. 

Diese Definitionen heißen in REDAXO *Properties* und können innerhalb des AddOns mit `$this->getProperty($key)` abgefragt werden. 

Die Properties eines anderen AddOns erhält man durch: `rex_addon::get('addonkey')->getProperty('author')`.  

<a name="pflicht"></a>
## Pflichtangaben

Die nachfolgenden Felder sind die einzigen Pflichtfelder in der package.yml. Diese reichen aus, um ein (funktionsloses) Addon zu erstellen.

```yml
package: meinaddon 
version: '1.0.0' 
```
**package:** Hier wird der AddOnkey hinterlegt. Dieser sollte eindeutig und unverwechselbar sein, darf nur aus Buchstaben, _ (Unterstrich) und Zahlen bestehen. Damit es nicht zu Konflikten mit anderen AddOns gleicher Bezeichnung kommt, sollte man den AddOn-Key in [MyREDAXO](https://redaxo.org/myredaxo/login/) registrieren.

**version:** Hier wird die Version des AddOns hinterlegt. Damit der Installer die Versionen korrekt zuordnen kann, müssen die folgenden Vorgaben entsprechend [Composer](https://getcomposer.org/doc/articles/versions.md) eingehalten werden. 

<a name="empfohlen"></a>
## Empfohlene Angaben

Damit die Nutzer erfahren, wer das AddOn geschrieben hat und wo man Support erhält, sollte man die Informationen zu Author und Supportseite hinterlegen. 

```yml
author: Rex Red
supportpage: https://meinesupportseite.tld
```
<a name="requires"></a>
## Abhängigkeiten (requires:)

Im AddOn sollte man festgelegen, welche Umgebung es erwartet oder gar benötigt. Hierzu zählen:

- die erforderliche REDAXO-Version
- erforderliche AddOns und PlugIns, auf denen das AddOn ggf. aufbaut oder deren Funktionen es nutzt.
- die erwartete PHP-Version
- erforderliche PHP-Extensions

Werden diese Bedingungen nicht erfüllt, ist eine Installation nicht möglich. 

**Beispiel:**

```yml
requires:
    redaxo: '^5.1'
    packages:
        media_manager: '^2.0.1'
        addonname/pluginname: '^2.4.6'
    php:
        version: '>=5.6' 
        extensions: [gd, xml]
```
Abhängigkeiten werden eingeleitet mit `requires:`.

Darunter eingerückt werden die Subkeys, hier: `redaxo`, `packages`, `php`; `packages` und `php` haben wiederum eigene Subkeys.

Hier wird *mindestens REDAXO 5.1* vorausgesetzt. `^` drückt aus, dass es sich auf das aktuelle Major-Release bezieht. Das heißt, eine Installation in einem REDAXO 6 wäre nicht möglich. Dies gilt ebenso für den Media Manager, der mindestens in Version 2.0.1 vorliegen muss. PHP dagegen muss nur höher oder gleich 5.6 sein. Hier gilt nicht die Begrenzung auf die Major-Release, sodass eine Installation unter PHP 7 möglich ist. "`addonname/pluginname: '^2.4'`" prüft ob ein bestimmtes PlugIn vorhanden ist. 

<a name="conflicts"></a>
## Konflikte (conflicts:)

Manchmal vertragen sich einige AddOns nicht miteinander, weil sie die gleichen Bibliotheken mitbringen – oder es liegt einfach eine Umgebung vor, die zu Problemen führen kann. Dann sollte vor der Installation geprüft werden, ob ein Konflikt vorliegt. Die Definition ist identisch mit `requires:`, wird jedoch durch `conflicts:` eingeleitet.

```yml 
conflicts:
    packages:
        irgendein_addon: '>=1.0.0'
```
Wird die Version größer/gleich 1.0.0 des genannten AddOns gefunden, bricht die Installation ab. 

<a name="ignore"></a>
## Dateien/Ordner ignorieren

Bei der Erstellung des Installationspaketes können ausgwählte Dateien und Ordner ignoriert werden 

```yml
installer_ignore:
    - node_modules
    - .env
```

> Das ignore-Pattern greift nur auf der Root-Ebene des AddOns und arbeitet nicht rekursiv. Dementsprechend sind auch keine Patterns möglich wie assets/css/* oder source/js.

<a name="seiten"></a>
## Seiten (page: / subpages:) 
 
Die Hauptseite wird über die Property `page` definiert. Diese wird aufgerufen, wenn man auf den Menüpunkt des AddOns klickt. 

Jede Seite erhält einen Titel mit dem Key `title`. 

```yml
page:
    title: 'translate:title' 
```
Der in der Hauptseite hinterlegte Titel ist zugleich die Bezeichnung für den Menüpunkt. 

Für den Menüpunkt des AddOns kann ein Icon aus Font-Awsome festgelegt werden. Für die korrekte Darstellung sollte die CSS-Klasse des Icons immer in Kombination mit `rex-icon` angegeben werden:

```yml
page:
    title: 'translate:title' 
    icon: rex-icon fa-television 
```

Will die Hauptseite in **Unterseiten** unterteilen, werden diese mit Hilfe des Keys `subpages` eingeleitet. Danach folgen eingerückt frei wählbare Properties für die einzelnen Unterseiten. 

```yml
subpages:
    main:  
        title: 'translate:main'
        icon: rex-icon fa-television
    help:  
        title: 'translate:help'
        icon: rex-icon fa-help
    module: 
        title: 'translate:module' 
        perm: admin
``` 
Die einzelnen Tabs der Seiten können auch mit Icons versehen werden.

**Die Seiten müssen im Ordner `/pages` als php-Dateien vorliegen.** (hier: `main.php`, `help.php`, `module.php`).
Die Hauptseite ist die `index.php` im /pages-Ordner.

<a name="hidden"></a>
### Seiten verstecken

Manchmal benötigt man Seiten, die nicht über die Navigation erreichbar sind. Hierzu steht der Parameter `hidden` zur Verfügung; mit `true` oder `false` wird die Sichtbarkeit gesteuert:

```yml
seitenkey: { title: 'translate:seitenname', hidden: true}
```
Auch der eigentliche Menüpunkt des AddOns kann so versteckt werden. 

<a name="haslayout"></a>
### Seiten nicht im REDAXO-Layout ausgeben

Möchte man die Seite im eigenen Design ausgeben (z.B. in einem Popup) oder man benötigt eine Ausgabe nicht im HTML-Format (z.B. für JSON,TXT,YML) hilft folgender Code in der Seiten-Definiton. 

`hasLayout: false`


<a name="rechte"></a>
## Rechte (perm:)

In der package.yml können auch Rechte für Benutzer festgelegt und abgefragt werden. 

Möchte man z.B. nur Admins die Nutzung des AddOns gestatten, so fügt man der `page`-Definition `perm: admin` hinzu.
Möchte man das nur auf eine Unterseite beziehen, legt man den Key in der Definition der entsprechenden Unterseite ab. 

Oftmals reicht die Festlegung auf den Admin nicht und man möchte eine ausgefeiltere Rechte-Vergabe definieren. (Beispiel: der Redakteur darf Daten einpflegen, aber nicht löschen.) 

Daher legt man am besten ein eigenes Recht an. 
Hierzu bietet sich der Hauptbereich der package.yml an. 

Damit die Rechte später leicht identifiziert werden können, sollten diese den AddOnkey wiederspiegeln.

z.B.: `perm: meinaddon[]`

Wird dieser Key angelegt, ist das Recht in der Benutzerverwaltung auswählbar. Weitere, davon abgeleitete Rechte können durch einen zusätzlichen key in den Klammern definiert werden. 

z.B: `perm: meinaddon[delete]`

Die Rechte können dann im AddOn per PHP abgefragt werden:

```php
rex::getUser()->hasPerm('meinaddon[delete]')
```
<a name="uebersetzung"></a>
## Übersetzung

Mit `translate:` beginnende Werte werden anhand der Sprachdatei übersetzt. Der Addon-Präfix (hier z.B. `meinaddon_`) kann in den Lang-Files (den Sprachdateien) des AddOns weggelassen werden.

<a name="eigene"></a>
## Eigene Properties

Die package.yml ist sehr offen gestaltet. Daher kann man auch eigene Properties in ihr ablegen. 
Der Abruf erfolgt wie oben gezeigt per `$this->getProperty($eigenerkey)`.


<a name="pjax"></a>
## PJAX deaktivieren

Möchte man PJAX auf den Seiten des AddOns nutzen, kann man dies per `pjax: true` erreichen.

```yml
page:
    title: 'translate:Mein Addon'
    perm: meinaddon[]
    pjax: true
    icon: rex-icon fa-television
```

<a name="plugin"></a>
## PlugIn

PlugIns unterscheiden sich von AddOns nur durch ihre Definition im Value des Keys `package` in der Datei `package.yml`. 

```yml
package: meinaddon/meinplugin
```

Die Seiten eines PlugIns werden dem AddOn automatisch hinzugefügt. 


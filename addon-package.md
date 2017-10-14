# package.yml 

- [Beispiel einer package.yml](#beispiel)
- [Die package.yml definiert das AddOn oder PlugIn](#ueber)
- [Pflichtangaben](#pflicht)
- [Empfohlene Angaben](#empfohlen)
- [Abhängigkeiten (requires:)](#requires)
- [Konflikte (conflicts:)](#conflicts)
- [Seiten (page: / subpages:)](#seiten)
- [Rechte](#rechte)
- [Übersetzung](#uebersetzung)
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
        help:  
             title: 'translate:help' 
        module: 
             title: 'translate:module' 
             perm: admin
requires:
    redaxo: '^5.1'
    packages:
        media_manager: '^2.0.1'
conflicts:
    packages:
        irgendein_addon: '>=1.0.0'
```
<a name="ueber"></a>
## Die package.yml definiert das AddOn oder PlugIn 

In der package.yml werden alle nötigen Einstellungen und Informationen hinterlegt, damit das AddOn oder PlugIn korrekt von REDAXO gefunden und ausgeführt werden kann. 
Die Verwendete Sprache ist das auf Markup verzichtende YAML.

> Es ist zu beachten, dass in YAML keine Tabs unterstützt werden. Die Einrückungen werden mit Leerzeichen realisiert. 

Die Definition erfolgt in Schlüssel-Wert-Paaren (key value pairs). Das Trennzeichen zwischen Schlüssel und Wert ist der Doppelpunkt. Die Zugehörigkeit zu Oberpunkten wird durch Einrückungen (per Leerzeichen) definiert. 

Diese Definitionen heißen in REDAXO Properties und können innerhalb des AddOns mit `$this->getProperty($key)` abgefragt werden. 

Die Properties eines anderen AddOns erhält man durch: `rex_addon::get('addonkey')->getProperty('author')`.  

<a name="pflicht"></a>
## Pflichtangaben

Die nachfolgenden Felder sind die einzigen Pflichtfelder in der package.yml. Diese reichen aus um ein funktionsloses Addon zu erstellen. 

```yml
package: meinaddon 
version: '1.0.0' 
```
**package:** Hier wird der AddOnkey hinterlegt. Dieser sollte eindeutige und unverwechselbar sein. Damit es nicht zu Konflikten mit anderen AddOns gleicher Bezeichnung kommt, sollte der Key in MyREDAXO registriert sein. 

**version:** Hier wird die Version des AddOns hinterlegt. Damit der Installer die Versionen korrekt zuordnen kann, sollten die folgenden Vorgaben entsprechend [Composer](https://getcomposer.org/doc/articles/versions.md) eingehalten werden. 

<a name="empfohlen"></a>
## Empfohlene Angaben

Damit die Nutzer erfahren wer das AddOn geschrieben hat und wo er Support erhält sollten die Informationen zu Author und Supportseite hinterlegt werden. 

```yml
author: Rex Red
supportpage: https://meinesupportseite.tld
```
<a name="requires"></a>
## Abhängigkeiten (requires:)

Es sollte im AddOn festgelegt werden, welche Umgebung es erwartet. Hierzu zählen:

- die erforderliche REDAXO-Version
- erforderliche AddOns auf denen das AddOn ggf. aufbaut oder deren Funktionen nutzt.
- die erwartete PHP-Version 
- erforderliche PHP-Extensions

Werden diese  Bedingungen nicht erfüllt, ist eine Installation nicht möglich. 

**Beispiel:**

```yml
requires:
    redaxo: '^5.1'
    packages:
        media_manager: '^2.0.1'
    php:
        version: '>=5.6' 
        extensions: [gd, xml]
```
Abhängigkeiten werden eingeleitet mit `requires:`.

Darunter eingerückt werden die Subkeys, hier. redaxo, packages, php. packages und php haben wiederum eigene Subkeys.

Hier wird *mindesten REDAXO 5.1* vorausgesetzt. `^` drückt aus, dass es sich auf die aktuelle Major Release bezieht. D.h. Eine Installation in einem REDAXO 6 wäre nicht möglich. Dies gilt ebenso für den Media Manager, der mindestens in Version 2.0.1 vorliegen muss. PHP dagegen muss nur höher oder gleich 5.6 sein. Hier gilt nicht die Begrenzung auf die Major-Release, so dass eine Installation z.B. unter PHP 7 möglich ist. 

<a name="conflicts"></a>
## Konflikte (conflicts:)

Manchmal vertragen einige AddOns nicht oder es liegt einfach eine Umgebung vor die zu Problemen führen kann, dann sollte vor der Installation geprüft werden ob ein Konflikt vorliegt. Die Definition ist identisch mit `requires:`, wird jedoch durch `conflicts:` eingeleitet.

```yml 
conflicts:
    packages:
        irgendein_addon: '>=1.0.0'
```
Wird die Version 1.0.0 des genannten AddOns gefunden, bricht die Installation ab. 

<a name="seiten"></a>
## Seiten (page: / subpages:) 
 
Die Hauptseite wird über den Key `page` definiert. Diese wird aufgerufen, wenn man auf den Menüpunkt des AddOns klickt. 

Jede Seite erhält einen Titel durch den Key `title`. 

```yml
page:
    title: 'translate:title' 
```
Der in der Hauptseite hinterlegte Titel ist zugleich die Bezeichnung für den Menüpunkt. 

Für den Menüpunkt des AddOns kann ein Icon aus Font-Awsome festgelegt werden. Für die korrekte Darstellung sollte es immer in Kombination mit der CSS-Class `rex-icon` angegeben werden.  

```yml
page:
    title: 'translate:title' 
    icon: rex-icon fa-television 
```

Soll die Hauptseite in **Unterseiten** unterteilt werden, werden diese mit Hilfe des Keys `subpages` definiert. Danach folgen frei wählbare Keys für die einzelnen Unterseiten. 

```yml
subpages:
    main:  
      title: 'translate:main'    
    help:  
     title: 'translate:help' 
    module: 
      title: 'translate:module' 
      perm: admin
``` 
Die einzelnen Tabs der Seiten können auch mit Icons versehen werden.

**Die Seiten müssen im Ordner `/pages` als php-Dateien vorliegen.** (hier: main.php, config.php). 
Die Hauptseite ist die **index.php im /pages-Ordner**. 

<a name="rechte"></a>
## Rechte

In der package.yml können auch Rechte für Benutzer festgelegt und abgefragt werden. 

Möchte man z.B. dass nur Admins das AddOn nutzen dürfen, fügt man im Kopfbereich, z.B. nach Author `perm: admin` hinzu.
Möchte man das nur auf eine Unterseite beziehen, legt man den Key in der Definition der entsprechenden Unterseite ab. 

Gut, manchmal reicht die Festlegung auf den Admin nicht, man braucht evtl. eine ausgefeiltere Rechte-Vergabe. (Beispiel: Redakteur darf Daten einpflegen, aber evtl. nicht löschen) 

Daher legt man am besten ein eigenes Recht an. 
Hierzu bietet sich der Hauptbereich der package.yml an. 

Damit die Rechte später leicht identifiziert werden können sollten diese den addonkey wiederspiegeln.

z.B.: `perm: meinaddon[]`

Wird dieser Key angelegt, ist das Recht bereits in der Benutzerverwaltung auswählbar. Weitere davon abgeleitete Rechte können durch einen zusätzlichen key in den Klammern definiert werden. 

z.B: meinaddon[delete]

Die Rechte können im AddOn per PHP abgefragt werden:


```php
rex::getUser()->hasPerm('meinaddon[delete]')
```
<a name="uebersetzung"></a>
## Übersetzung

Werte die mit `translate:` beginnen, werden anhand der Sprachdatei übersetzt. Der Addon-Präfix (hier z.B: `meinaddon_`) kann in den Lang-Files des AddOns weggelassen werden.

<a name="pjax"></a>
## PJAX deaktivieren

Möchte man auf PJAX auf den Seiten des AddOns verzichten kann man dies per `pjax: false` REDAXO mitteilen. 

```yml
page:
    title: 'translate:Mein Addon'
    perm: meinaddon[]
    pjax: false
    icon: rex-icon fa-television
```

<a name="plugin"></a>
## PlugIn



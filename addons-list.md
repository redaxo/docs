# Liste einiger AddOns

- [Einführung](#einfuehrung)
- [Systemerweiterungen](#systemerweiterungen)
- [Backend](#backend)
- [Applikationen](#applikationen)
- [Development](#development)
  - [Adminer](#adminer)
  - [Cheatsheat für Extensionpoints](#cheatsheet)
  - [Demo-AddOn](#demo)
  - [Developer - Module, Templates und Aktionen syncen](#developer)
  - [Project - Schnell mal eine PHP-Class einbinden](#project)
  - [Strukturierte Daten - HilfsAddOn für Jason-LD](#strucdata)
  - [Theme - Verwalten aller Projektdateien für Frontend und Backend](#theme)
  - [YConverter - Migration REDAXO 4.x zu 5.x](#yconverter)
  - [YTraduko - Übersetzungshelfer](#ytraduko)
  - [ZIP-Install](#zip)
- [Workflows](#workflows)
  - [REDAXO mit Bimmelbam](#bimmelbam)
  - [REDAXO mit Docker](#docker)



<a name="einfuehrung"></a>
## Einführung

Erst die zu einem Projekt passenden AddOns machen REDAXO zu dem mächtigen Werkzeug was es wirklich ist. In der Vielzahl der AddOns ist es manchmal schwierig das passende zu finden. Daher gibt es hier eine redaktionelle Vorstellung einiger AddOns.

AddOns sind über die REDAXO-Website als Downloads verfügbar (https://redaxo.org/download/addons/) oder können über den Installer direkt in eine Installation eingebaut werden.

Der Natur der Sache ist geschuldet, dass diese Aufstellung immer unvollständig sein wird. Denn es kommen stets neue AddOns dazu. Der Bereich ist derzeit auch noch im Aufbau. Wenn also hier ein wichtiges AddOn fehlt ... - ran an die Tasten und einen entsprechenden Artikel schreiben.

<a name="systemerweiterungen"></a>
## Systemerweiterungen

### YRewrite - sprechende Urls

Eine multidomainfähige Lösung für schöne Urls und Seo-Optimierung

### YForm - der Datenbankmanager

Mit yform lassen sich Datentabellen anlegen und verwalten, Formulare aufbauen und verarbeiten, E-Mail Templates erstellen und einiges mehr.

<a name="backend"></a>
## Backend AddOns

AddOns, die für die Programmierung, und die Verwaltung im Backend hilfreich sind.

### MBlock - Elemente Gruppieren

Mit MBlock lassen sich Module erstellen, die mehrere gleichartige Inhaltselemente enthalten. Ideal für Galerien, Teamseiten, Akkordeons usw.

### Quick Navigation

Das AddOn ermöglicht den schnellen Zugriff auf die ganze Struktur im Backend. Es sollte in keinem Projekt fehlen mit einem Umfang von mehr als zwei Seiten.

<a name="applikationen"></a>
## Applikationen, thematische AddOns

AddOns, die Erweiterungen für Branchen und spezielle Aufgaben bereitstellen.

### Sked Kalender

ist ein mächtiges AddOn, mit dem sich die meisten Aufgaben zur Terminverwaltung und -anzeige umsetzen lassen.

https://github.com/FriendsOfREDAXO/sked

[mehr lesen ...](https://redaxo.org/cms/addons/sked-der-kalender/)


### Aufgaben

Ein Aufgaben Manager, der nicht nur beim Aufbau einer REDAXO Präsentation den Todo Workflow abbilden kann sondern auch für andere Zwecke verwendbar ist.

**Installation per Installer**
[**Github-Repo**](https://github.com/FriendsOfREDAXO/aufgaben)


<a name="development"></a>
## AddOns

<a name="adminer"></a>
### Adminer

Adminer für REDAXO. Seit Version 1.3.0 kann der rex_sql_table code für die ausgewählte Tabelle in der Tabellenstruktur angezeigt werden. Sehr hilfreich bei der AddOn-Erstellung für die install.php. 

**Installation per Installer**

[**Github-Repo**](https://github.com/FriendsOfREDAXO/adminer)

<a name="cheatsheet"></a>
### Cheatsheet

Das Cheatsheet-AddOn scant die REDAXO-Installation nach Extension-Points im Core und den installierten AddOns und listet deren Position im Quellcode auf. 

[**Installation aus Github-Repo:**](https://github.com/tbaddade/redaxo_cheatsheet)

<a name="demo"></a>
### Demo-AddOn

Das Demo-AddOn zeigt wie AddOns entwickelt und dokumentiert werden. Gut kommentierter Quellcode, Hilfe und Hints im AddOn selbst helfen beim Verständnis der AddOn-Programmierung und der Dokumentation. Es liefert auch ein Doku-Plugin, das den Aufbau einer Hilfe für das eigne AddOn ermöglicht.   

**Installation per Installer**

[**Github-Repo:**](https://github.com/FriendsOfREDAXO/demo_addon)


<a name="developer"></a>
### Developer

Developer kopiert und synct Module, Templates und Aktionen zwischen Dateisystem und Datenbank, so werden diese leicht für externe Editoren und per FTP zugänglich.

**Installation per Installer**

[**Github-Repo**](https://github.com/FriendsOfREDAXO/developer)

<a name="project"></a>
### Project

In REDAXO bereits vorhanden, ist das Project-AddOn. Hier können einfach eigene PHP-Classes und Assets eingebunden werden, die nach einem Update nicht gelöscht werden. Man erspart sich so also die Entwicklung eines eigenen AddOns, wenn man das System einfach nur mit einer PHP-Class bereichern möchte. 

**Installation in der AddOn-Verwaltungr**


<a name="strucdata"></a>
### Strukturierte Daten (JSON-LD)

Gerne vergessen, von Google aber gern gesehen. JSON-LD - Informationen auf der Website. Dieses AddOn hilft bei der Erstellung. 

[**Github-Repo**](https://github.com/eaCe/strucdata)



<a name="theme"></a>
### Theme

Das Theme-AddOn erleichtert die Verwaltung aller für das Projekt erforderlichen Prajektdateien in einem zusätzlichen /theme-Ordner im Web-Root. Theme erlaubt es auch das System oder die Website mit zusätzlichen CSS, JS und PHP-Classes zu breichern. Ist das Developer-AddOn installiert, synct es sich mit diesem um die Modul- und Template-Dateien an einer zugänglicheren Stelle bereitzustellen. 

**Installation per Installer**

[**Github-Repo**](https://github.com/FriendsOfREDAXO/theme)

<a name="yconverter"></a>
### YConverter

Eine REDAXO 4.x - Datenbank kann mit Hilfe dieses AddOns für REDAXO 5.x vorbereitet werden und migriert werden. Hierbei werden bekannte Class- und Methodenaufrufe, REX_VARS für REDAXO 5.x vorbereitet und sogar xform-Tabellen nach yform konvertiert. 

[**Github-Repo**](https://github.com/yakamara/yconverter)

<a name="ytraduko"></a>
### YTraduko - Übersetzungshelfer 

Ytraduko hilft bei der Übersetzung der eigenen AddOns. Anstelle selbst für die weiteren Sprachen neue .lang - Dateien anzulegen, erledigt dieses AddOn es selbst. Die Übersetzungen können übersichtlich und schnell eingepflegt werden. 

[**Installation aus Github-Repo**](https://github.com/yakamara/ytraduko)

<a name="zip"></a>
### ZIP-Install 

Das ZIP-Install ermöglicht es gezippte AddOns ohne Umweg per FTP auf den Server zu laden und zu entpacken. Ganz praktisch vor allem, wenn es sich um AddOns handelt, die es nur als GitHub-Repo gibt und nicht im Installer zur Vefügung stehen.  

**Installation per Installer**

[**GitHub-Repo**](https://github.com/FriendsOfREDAXO/zip_install)


<a name="workflows"></a>
## Workflows für Developer

<a name="bimmelbam"></a>
### REDAXO mit Gulp, Browserify, PostCSS und Bimmelbam

Ein Frontend-Workflow auch für REDAXO

Frontendentwicklung wird immer aufwändiger, SCSS wollen kompiliert werden, Bilder komprimiert werden, JS schöner werden, HTML-Prototypen wollen erzeugt werden. ***REDAXO mit Bimmelbam*** zeigt hierfür einen ausbaufähigen Weg. 

[**GitHub-Repo**](https://github.com/FriendsOfREDAXO/redaxo-mit-bimmelbam)


<a name="docker"></a>
### REDAXO mit Docker

***MAMP und XAMPP waren gestern!*** REDAXO kann leicht, systemunabhängig mit Docker verwendet werden. Die Vorteile: Möglichkeit der zentralen Installation und Bearbeitung, Versionierbarkeit, Ausbaufähigkeit. REDAXO-mit-Docker liefert alle Ressourcen und eine einsteigergeignete Anleitung. Und damit man nicht bei Null anfangen muss, kann eine Demo gleich automatisiert installiert werden. ***REDAXO mit Docker und Bimmelbam*** sind übrigens leicht miteinander kombinierbar. Weitere Infos in den jeweiligen REPOS. 

[**GitHub-Repo**](https://github.com/FriendsOfREDAXO/redaxo-mit-docker)

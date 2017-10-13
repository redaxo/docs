# AddOns

- [Über](#ueber)
- [Im Lieferumfang enthaltene AddOns](#included)
- [AddOnverwaltung](#addons)
- [Upload](#upload)
 - [Upload per Installer](#upinstaller)
 - [Upload per (S)FTP](#upftp) 
 - [Hinweis zu AddOns aus GitHub](#github)  
- [AddOn-Installation](#install)
- [Update](#update)
- [Reinstallieren / Reparatur](#reinstall)
- [Deinstallation](#uninstall)

<a name="ueber"></a>
## Über

AddOns sind Erweiterungen für REDAXO. Sie liefern zusätzliche Funktionen, verbessern oder erweitern die Benutzeroberfläche und Bedienung oder liefern die nötigen Skripte für die Frontendausgabe. AddOns können auch komplexe Applikationen (Newssystem, Kalender, Bildbearbeitung) sein oder im einfachsten Fall nur zusätzliche PHP-Classes im System bereitstellen (PDF-Umwandlung, E-Mail-Verschlüsselung, URL-Schemen). 

Ein großer Teil der Grundfunktionen von REDAXO wird als AddOns bereitgestellt (Core-AddOns). Diese Core-AddOns können so leicht aktualisiert und ggf. durch individuelle Lösungen ausgetauscht werden. 

Einige AddOns liefern eigene PlugIns mit. Diese erweitern das AddOn um weitere Funktionalitäten.

<a name="included"></a>
## Im Lieferumfang enthaltene AddOns

REDAXO liefert bereits bei der Installation einige AddOns und PlugIns mit:

AddOn | PlugIn | Beschreibung
------------- | ------------- | -------------
backup | |Erstellung und Wiederherstellung von Backups
be_style | | Addon für die Backenddarstellung
|| redaxo | Liefert das Default-Design des Backend
|| customizer | Liefert Erweiterungen (Code-Higlightning, Link zum Frontend, Einfärbung
cronjob | | Ausführung Regelmäßiger, geplanter Aufgaben
|| article_status | Ändert den Online-Status entsprechend Meta-Angabe
|| optimize_tables | Optimiert die Datenbanktabellen
install | | Veröffentlichung und Download von AddOns
media_manager | | Ausgabe und Manipulation von Medien
mediapool | | Medienverwaltung
metainfo | | Stellt Metafelder im System zur Vefügung
phpmailer | | Bindet die PHPMailer Class ein zum Versand von E-Mails
project | | Ein leeres AddOn um eigene Funktionen zu integrieren (*updatesicher*)
structure | | Liefert die Strukturverwaltung für Kategorien und Artikel
|| content | Stellt die Funktionen zur Inhaltsbearbeitung bereit
|| history | Versionierung von Artikeln
|| version | Pflege von Arbeitsversionen
users | |Benutzer- und Rollenverwaltung

<a name="addons"></a>
## AddOn-Verwaltung 
In der AddOn-Verwaltung, die im Hauptmenü unter **AddOns** zu finden ist, werden die verfügbaren AddOns gelistet und verwaltet sowie neue AddOns installiert bzw. aktiviert. Die AddOn-Verwaltung ist kein Katalog, sie listet nur die auf das System bereits hochgeladenen AddOns.

Die AddOn-Verwaltung listet die AddOns und deren Plugins, deren Versionsnummer, einen Link zu einer Hilfsdatei und die entsprechenden Funktionen zur Verwaltung. 

Der schnellste Weg neue AddOns in das System zu laden ist der Download über den **Installer**. 

**Weitere AddOnquellen sind: **

- AddOn-Bereich auf [www.redaxo.org](https://redaxo.org/download/addons/) (Identisch mit Installer) 
- GitHub-Repos
- Ihre Agentur / Ihr Dienstleister

   
<a name="upload"></a>
## Upload 
Bevor ein AddOn installiert werden kann muss dieses hochgeladen werden. Nachfolgend zeigen wir hier gängige Upload-Methoden. 

<a name="upinstaller"></a>
### Upload per Installer
Siehe: [Installer](/{{path}}/{{version}}/installer)

<a name="upftp"></a>
### Manueller Upload per (S)FTP
- Download des AddOns als ZIP
- Entpacken des ZIP
- ggf. README.md beachten, sofern vorhanden
- Upload in den Ordner `/redaxo/core/addons/`


<a name="github"></a> 
### Hinweis zu AddOns aus GitHub. 
Soweit möglich sollte man nicht das aktuelle Repository herunterladen, hierbei handelt es sich meist um Entwicklungsversionen, die nicht für den produktiven Einsatz gedacht sind. Hier sollte man immer auf eine aktuelle Release zurückgreifen. Vorher bitte auch, die dort hinterlegten Issues beachten. 

<a name="install"></a> 
## AddOn-Installation

Nach dem erfolgten Upload können die AddOns in der AddOn-Verwaltung (Menüpunkt: `AddOns`) installiert werden. 

> Neben der Versionsnummer findet man ein Fragezeichen (`?`). Hier findet man meist nützliche Informationen zur Installation und zur Benutzung. Es empfiehlt sich, diese vor der Installation zu lesen. 

Klickt man auf `installieren`, wird das AddOn installiert. Hierbei werden die nötigen Schritte (z.B. kopieren von CSS- und JS-Dateien, Anlage von Datenbanken) durchgeführt, damit das AddOn verwendet werden kann. Nach erfolgter Installation kann das AddOn aktiviert und anschließend verwendet werden. 

<a name="update"></a>
## Update

Wenn das AddOn im Installer gelistet ist, kann es über diesen schnell und unkompliziert aktualisiert werden.. 
Weitere Informationen im Abschnitt: [Installer](/{{path}}/{{version}}/installer) 

<a name="reinstall"></a>
## Reinstallieren / Reparatur

Sollte es mal zu einem Problem mit dem AddOn kommen (evtl. nach einem Update), kann man das AddOn reinstallieren. Hierbei wird das AddOn wieder installiert und ggf. Einstellungen und Dateien korrigiert. 

> Bei einem Reinstall werden keine Daten entfernt   

<a name="uninstall"></a>
## Deinstallation / Löschen

Möchte man ein AddOn deinstallieren, klickt man auf  `de-installieren`. Möchte man das AddOn komplett löschen, klickt man auf `löschen`. 

> Einige AddOns löschen beim Deinstallieren nicht die angelegten Datenbank-Tabellen und die darin erfassten Daten. Hierzu bitte zu zugehörige Dokumentation beachten.
`



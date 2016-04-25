# Installation

- [Systemanforderungen](#systemanforderungen)
- [Download](#download)
- [Upload](#upload)
- [Installation](#installation)

<a name="systemanforderungen"></a>
## Systemanforderungen

Folgende Voraussetzungen müssen zur einwandfreien Nutzung und Installation von REDAXO 4.x von Webspace, Webserver und Datenbank erfüllt werden:

* PHP >= 4.3.2
* MySQL (3,) 4, 5
* FTP Zugangsdaten (Host, Login, Passwort)
* MySQL Zugangsdaten (Host, Datenbank, Login, Passwort)

<a name="download"></a>
## Download

Sie können auf der offiziellen REDAXO-Webseite die aktuelle Basisversion des Systems erhalten. Diese sowie Updates oder ältere Versionen sollten Sie im Download-Bereich finden können. Laden Sie zur Installation die aktuelle REDAXO 4.x Version in einem Zip-Archiv gepackt herunter. Die entpackte Ordnerstruktur sollte dann wie folgt vorliegen:

	/files
	/redaxo
	.htaccess
	_htaccess
	_lastchanges.txt
	_lizenz.txt
	index.php

**Wichtiger Hinweis:**

> Die komplette Ordnerstruktur sollte für die Installation nicht verändert werden. Einen detaillierten Überblick über die Ordnerstruktur und Rechtevergabe erhalten Sie im Kapitel Upload.

**Kurzbeschreibung der Ordnerstruktur**

Im Ordner files werden alle Dateien abgelegt, welche durch den Medienpool hochgeladen werden. Der Ordner redaxo enthält alle Systemkomponenten, durch Aufrufen des Ordners im Browser http://domain.de/redaxo gelangt man zur Loginseite des Backends. Die Datei index.php dient zu Darstellung aller Artikel/Seiten der Webseite. Durch sie wird das Frontend ausgegeben. Den txt-Dateien kommt keine tragende Bedeutung zu, sie erfüllen lediglich informative Zwecke.

Die in der Ordnerstruktur älterer Versionen 2.x und 3.x enthaltenen Ordner css, js und pics sind in der Ordnerstruktur von REDAXO 4.x nicht mehr enthalten.

<a name="upload"></a>
## Upload

Laden Sie den Ordnerinhalt des entpackten Zip-Archivs der aktuellen REDAXO-Version auf Ihren Webspace. Für die notwendigen Einstellungen zum Upload auf Ihren Webserver schlagen Sie in der Hilfe Ihres FTP-Programms nach.

Es empfiehlt sich ein Upload in das Root-Verzeichnis Ihres Webspaces, es ist aber auch möglich, REDAXO in ein Unterverzeichnis zu laden, jedoch muss dies dann im Weiteren gesondert berücksichtigt werden.

Sobald die Ordnerstruktur samt enthaltener Dateien erfolgreich auf Ihren Webspace geladen ist, können Sie, nachdem alle Berechtigungen korrekt gesetzt sind, mit der Installationsroutine beginnen.

Eine der ersten Überprüfungen gilt den Rechten mehrerer Ordner und Dateien.
Sie können die Installation starten und auf die mögliche Fehlerliste warten oder gleich die notwendigen Einstellungen über Ihr FTP-Programm überprüfen und anpassen.

**Ordnerstruktur**

	/files
	/redaxo
	.htaccess
	_htaccess
	_lastchanges.txt
	_lizenz.txt
	index.php

**Folgende Dateien und Ordner benötigen genannte Rechte**

	755 /files
	755 /redaxo/include/addons/import_export/backup
	755 /redaxo/include/generated
	755 /redaxo/include/generated/articles
	755 /redaxo/include/generated/files
	755 /redaxo/include/generated/templates
	755 /redaxo/include/install
	755 /redaxo/include/clang.inc.php
	755 /redaxo/include/addons.inc.php
	755 /redaxo/include/functions.inc.php
	755 /redaxo/include/master.inc.php

<a name="installation"></a>
## Installation

Sobald Sie REDAXO auf Ihren Webspace übertragen haben und alle Rechte korrekt gesetzt sind, können Sie mit der Installation beginnen. Die Rechte werden in der Installations-Routine überprüft. Rufen Sie dazu in Ihrem Browser die URL Ihres Webspaces auf und fügen Sie an den Pfad

	/redaxo oder
	/redaxo/index.php

Ihre eingegebene URL sollte dann so aussehen: “http://meineurl.de/redaxo/index.php”. Hier sollte “meineurl” selbstverständlich durch Ihre Domain ersetzt sein.

**Sprachversion und Lizenzvereinbarung**

Vor Beginn des eigentlichen Setups wählen Sie bitte eine Sprache und bestätigen sie, dass Sie die Lizenzvereinbarungen gelesen haben.

Aktuell können Sie zwischen Deutsch, Englisch, Deutsch (utf-8) & Englisch (utf-8) wählen. Weitere Sprachen finden Sie im Downloadbereich unter dem Punkt Sprachpakete.

**Installationsroutine**

Nach diesen beiden Masken beginnt die eigentliche Installationsroutine, die insgesamt aus fünf Schritten besteht. Dabei werden die Ordnerrechte und die PHP-Version überprüft, die Datenbank angesteuert, Daten zu Ihrer Webseite erfasst, die Datenbank entsprechend eingerichtet und der Administrations-Benutzeraccount angelegt.

--


**1. Setup Schritt 1: Check der Ordnerrechte und der PHP-Version**

Im ersten Schritt des Setups wird die PHP-Version gecheckt und die Rechteüberprüfung der für die Nutzung von REDAXO benötigten Ordner und Dateien durchgeführt. Passen Sie ggf. mit Ihrem FTP-Programm die Rechte wie angegeben an. Erweiterte Informationen zum korrekten Upload und der nötigen Rechtevergabe können sie dem Kapitel Upload entnehmen.

--

**Setup Schritt 2: Allgemeine REDAXO-Einstellungen**

Im diesem Schritt können Sie Angaben zu Ihrer Webseite eintragen (diese lassen sich in den Systemeinstellungen im Backend des Systems nachträglich überarbeiten).

Entscheidend sind die Datenbankinformationen SQL-Host, Name der Datenbank, Login und Passwort. Diese müssen korrekt angegeben werden, um auf die Datenbank zugreifen zu können. Diese Angaben sollten sie von Ihrem Provider zur Verfügung gestellt bekommen.

Die Einstellungen werden vom Setup in die Datei include/master.inc.php geschrieben.

**Sicherheitshinweis**

> Die Passwortverschlüsselung sollten Sie unbedingt nutzen. Diese erweitert die Sicherheit für Ihr REDAXO-System und Ihren Server. Wählen Sie dazu “mit Verschlüsselung (sha1).”

**Tipp**

> Ihre Serverdomain muss nicht mit der Serverbezeichnung übereinstimmen. Es könnte die Serverdomain beispielsweise so aussehen: “meinedomain.de”, hingegen die Serverbezeichnung so lauten: “Meine Webseite”. Es bietet sich an, die genannte Serverbezeichnung im Title-tag des Templates einzubinden.

--

**Setup Schritt 3: Anlegen der Datenbank**

Im dritten Schritt der Installationsroutine wird die Datenbank für REDAXO eingerichtet. Dabei bestehen verschiedene Möglichkeiten, dies vom Setup ausführen zu lassen.

Für den ersten Start von REDAXO nutzen Sie die Option “Datenbank einrichten”. Es werden alle relevanten Tabellen und Datensätze, die Redaxo benötigt, in der Datenbank angelegt.

Setup - Vorhandenen Export einspielen
Möchten Sie REDAXO kennenlernen, empfehlen wir Ihnen, sich die REDAXO-Demo anzuschauen. Diese können Sie auch schon direkt bei der Installation einspielen lassen. Wählen Sie dazu “Vorhandenen Export einspielen” und wählen Sie den entsprechenden Export rex_4.3_demo.

Sie können die Datenbank-Struktur, sofern Sie phpMyAdmin oder ein ähnliches Tool zur Verfügung haben, überprüfen. Die folgenden Tabellen sollten nach der Basis-Installation angelegt worden sein:

	rex_62_params
	rex_62_type
	rex_679_types
	rex_679_type_effects
	rex_action
	rex_article
	rex_article_slice
	rex_clang
	rex_file
	rex_file_category
	rex_module
	rex_module_action
	rex_template
	rex_user

Beachten Sie, dass bei der Wahl “Datenbank einrichten und alte Überschreiben” alle Einträge aus der Datenbank entfernt werden.

REDAXO 4.x bietet bei seiner Installation die Option der Aktuallisierung einer Datenbank von REDAXO 3.x (3.0, 3.1, 3.2) an. Sie sollten jedoch unbedingt die Datenbank vor dem Update sichern.

**Hinweis zum Update**

> Es wird durch die Aktualisierung der Datenbank lediglich die Datenbank aktualisiert. Einträge in die Templates und Module werden nicht vorgenommen. So kann es zu Fehlern in der Ausgabe kommen, da REDAXO 4.x im Core (Systemkern) erheblich erneuert wurde und so zum Beispiel modernere Include-Verfahren nutzt.

--

**Setup Schritt 4: Administrator anlegen**

Hier legen Sie den ersten Benutzer für das REDAXO-Backend fest. Dieser wird mit Administratoren-Rechten angelegt. 
Sie können als Administrator diesen Account zu einem späteren Zeitpunkt modifizieren.

--

**Setup Schritt 5: Installation abgeschlossen**

Sind Sie bei diesem Schritt der Installation angekommen, haben Sie es geschafft. Die Installation war erfolgreich. Ihre Datenbank und REDAXO sind zum ersten Login bereit und eingerichtet.

Klicken Sie den Link oder geben Sie in Ihrem Browser die URL zu REDAXO ein (Siehe Hinweis oben “Start des Setups”). Sie gelangen genau wie in das Setup auch in die Administration.

--

**Erneute Durchführung des Setups**

Sie können im Nachhinein die gesamte Installationsroutine erneut starten. Dazu müssen Sie im Backend eingeloggt sein und unter System den Setup Button klicken.

Bestätigen Sie anschließend den Klick durch den “OK”-Button und darauf folgend mit “weiter” um das Setup erneut zu starten.

Ein erneuter Start des Setups ist jedoch in der Regel nicht nötig.

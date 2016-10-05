# Installation

In den folgenden Abschnitten erfährst du, wie du Redaxo auf deinem Server oder Webspace installieren kannst. 

- [Schnellanleitung](#schnell)
- [Datenbank](#datenbank)
- [Download](#download)
- [Upload](#upload)
- [Installationsvorgang](#install)

<a name="schnell"></a>
## Schnellanleitung
- Erstelle eine MySQL-Datenbank und notiere dir die Zugangsdaten. 
- Lade die neuste Version unter http://redaxo.org/de/download/ herunter.
- Entpacke die ZIP-Datei auf deinem Rechner.
- Lade die Dateien in dein Webverzeichnis.
- Führe die Installation unter der Adresse der Website mit angehängtem /redaxo/ (http://deinedomain.tld/redaxo/) aus.
- Gehe alle [Installationschritte](#install) durch.

<a name="datenbank"></a>
## Datenbank
Erstellle eine leere MySQL-Datenbank. Bei einigen Hostern ist bereits eine Datenbank angelegt, hierzu solltest Du Zugangsdaten erhalten haben. Für die Installation benötigst du die Zugangsdaten (Datenbank-Name, Adresse des Servers, Datenbank-Benutzer und Passwort) für diese Datenbank. 

<a name="download"></a>
## Download

Lade dir als erstes die aktuelle Version von Redaxo unter http://redaxo.org/de/download/ herunter. Informationen zum aktuellen Release findest du auch unter https://github.com/redaxo/redaxo/releases.
<a name="upload"></a>
## Upload 

Entpacke das heruntergeladene Zip-File und verschiebe den Inhalt in den Webordner deines lokalen Servers oder via FTP,SFTP, WebDAV auf deinen öffentlichen Webserver. Meist lautet der Webpordner httpdocs , htdocs oder html. 
Ausführliche Informationen zum Upload und zu deinen Zugangsdaten erhälst du von deinem Hostingpartner.

> **Tipp:** Einige Hoster bieten zur Verwaltung auch Oberflächen wie PLESK oder CPANEL zur Verwaltung des Webspaces an. Hier enthalten ist auch ein Dateimanager mit dem Du die Zip-Datei direkt hochladen und auf dem Server entpacken kannst. 


> **Hinweis für MAC und Linux-User:** Stelle sicher, dass die versteckten .htaccess-Dateien mit übertragen werden. In einigen FTP-Programmen müssen diese erst eingeblendet werden. 

Sollte der Server es beim Upload nicht selbst erledigt haben, stelle die Ordner- und Dateirechte auf 755.
<a name="install"></a>
## Installationsvorgang

Nachdem du Redaxo hochgeladen hast, kannst du die Installation mit http://deinedomain.tld/redaxo/ aufrufen. 
Die folgenden 7 Schritte führen dich durch die Installation. 

### Schritt 1 - Sprachauswahl

Im  ersten Schritt legst du die Sprache für den Installationsvorgang und für das Backend fest. 

![Sprachwahl](/assets/v5.2.0-installation-01-language.png)

> **Hinweis :** Die Sprache kann später im Setup oder User geändert werden. 

### Schritt 2 - Lizenz
Redaxo ist ein Open Source Projekt und kostenfrei. Allerdings gibt es Lizenzbedingungen die akzeptiert werden müssen.

![Lizenz](/assets/v5.2.0-installation-02-license.png)
Schritt 2 -  Lizenz 

### Schritt 3 - Systemcheck
An dieser Stelle führ die Installationsroutine einen Systemcheck durch und gibt ggf. Warnungen aus. Wenn was nicht stimmt, überprüfe eventuell auch die Systemvoraussetzungen.  

![Systemcheck](/assets/v5.2.0-installation-03-systemcheck.png)
Schritt 3 -  Systemcheck

### Schritt 4 - Konfiguration
An dieser Stelle wird die grundlegende Konfiguration durchgeführt. 
   
- URL der Website mit abschließendem /
- Name der Website  
- E-Mail-Adressse bei Fehlern
- Zeitzone
- Datenbankverbindung

Befindet sich die Datenbank auf dem lokalen Server, kannst Du hier localhost stehen lassen. Bei einigen Hostern sind der Webspace und die Datenbank voneinander getrennt. In diesem Fall musst Du hier die Adresse des Datenbankservers eingeben. 
Hat dein Benutzer das Recht auch neue Datenbanken zu erstellen, kannst du hier direkt eine neue Datenbank mit der oben agegebenen Bezeichnung anlegen lassen. 

![Config](/assets/v5.2.0-installation-04-config.png)
Schritt 4 -  Systemcheck

### Schritt 5 - Datenbank
Bitte wähle eine der drei Optionen.  
> **Hinweis :** Eine Aktualisierung von Redaxo-Versionen kleiner als 5 sind aktuell nicht vorgesehen.

![Datenbank](/assets/v5.2.0-installation-05-database.png)
Schritt 5 -  Datenbank

### Schritt 6 - Administrator
Definiere einen Namen und ein sicheres Passwort für den Administrator deiner Redaxo-Installation. Sichere Passwörter haben mehr als sechs Zeichen und beinhalten Groß- wie Kleinbuchstaben und Sonderzeichen. Auch ist es sinnvoll nicht unbedingt Admin oder Administrator als Benutzername anzulegen. Diese sind leicht zu erraten.  

![Datenbank](/assets/v5.2.0-installation-06-1stuser.png)
Schritt 6 -  Administrator

### Schritt 7 - Geschafft - Heureka - Hurra
Die Installation ist erfolgreich. Bitte beachte die Hinweise auf der Seite oder melden dich direkt über den Button unter der Seite an. Alternativ kannst du auch /redaxo/ hinter die URL im Browser schreiben, um in das Backend zu gelangen.

![Datenbank](/assets/v5.2.0-installation-07-1stlogin.png)
Schritt 7 -  Ende


# Installation

In den folgenden Bereichen erfährst Du wie Du Redaxo auf deinem Server installieren kannst. 

## Download

Lade dir als erstes die aktuelle Version von Redaxo unter http://redaxo.org/de/download/ herunter. 

## Upload 

Entpacke das heruntergeladene Zip-File und verschiebe den Inhalt in den Webordner deines lokalen Servers oder via FTP,SFTP, WebDAV auf deinen öffenltichen Webserver. 
Meist lautet der Webpordner httpdocs , htdocs oder html. 
Ausführliche Informationen zum Upload und zu deinen Zugangsdaten erhälst Du von Deinem Hostingpartner

Einige Hoster bieten zur Verwaltung auch Oberflächen wie PLESK oder CPANEL zur Verwaltung des Webspaces an. Hier enthalten ist auch ein Dateimanager mit dem Du die Zip-Datei direkt hochladen und auf dem Server entpacken kannst. 

> **Hinweis für MAC und Linux-User:** Stelle sicher, dass die versteckten .htaccess-Dateien mit übertragen werden. In einigen FTP-Programmen müssen diese erst eingeblendet werden. 

Sollte der Server es beim Upload nicht selbst erledigt haben, stelle die Ordner- und Dateirechte auf 755.

## Installationsvorgang

Nachdem Du Redaxo hochgeladen hat, kannst Du die Installation mit http://deinedomain.tld/redaxo/ aufrufen. 
Die folgenden 7 Schritte führen Dich durch die Installation. 

### Schritt 1 - Sprachauswahl

Im  ersten Schritt legst Du die Sprache für den Installationsvorgang und für das Backend fest. 

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
   
- URL Der Website mit abschließendem /
- Name der Website  
- E-Mail-Adressse bei Fehlern
- Zeitzone
- Datenbankverbindung

Hat Dein Benutzer das Recht auch neue Datenbanken zu erstellen, kannst du hier direkt eine neue Datenbank mit der oben agegebenen Bezeichnung anlegen lassen. 
Befindet sich die Datenbank auf dem lokalen Server, kannst Du hier localhost stehen lassen. Bei einigen Hostern sind der Webspace und die Datenbank voneinander getrennt. In diesem Fall musst Du hier die Adresse des Datenbankservers eingeben. 

![Config](/assets/v5.2.0-installation-04-config.png)
Schritt 4 -  Systemcheck

### Schritt 5 - Datenbank
Bitte wähle eine der drei Optionen.  
> **Hinweis :** Eine Aktualisierung von Redaxo-Versionen kleiner als 5 sind aktuell nicht vorgesehen.

![Datenbank](/assets/v5.2.0-installation-05-database.png)
Schritt 5 -  Datenbank

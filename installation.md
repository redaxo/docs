# Installation

- [Schnellanleitung](#schnell)
- [Datenbank](#datenbank)
- [Download](#download)
- [Upload](#upload)
- [Installationsvorgang](#install)

<a name="schnell"></a>
## Schnellanleitung

Die folgenden Abschnitte erläutern, wie man REDAXO auf einem Server oder Webspace installiert. 

- Eine MySQL-Datenbank erstellen und die Zugangsdaten notieren. 
- Die neueste Version unter http://redaxo.org/de/download/ herunterladen.
- Die ZIP-Datei auf deinem Rechner entpacken.
- Die Dateien in das Webverzeichnis hochladen.
Die Installation unter der Adresse der Website mit angehängtem /redaxo/ (http://deinedomain.tld/redaxo/) ausführen.
- Alle [Installationschritte](#install) durchgehen.

<a name="datenbank"></a>
## Datenbank

Zunächst erstellt man eine leere MySQL-Datenbank. Bei einigen Hostern ist bereits eine Datenbank angelegt, hierzu sollte man die Zugangsdaten erhalten haben. Für die Installation werden die Zugangsdaten (Datenbank-Name, Adresse des Servers, Datenbank-Benutzer und Passwort) für diese Datenbank benötigt. 

<a name="download"></a>
## Download

Als Erstes sollte man die aktuelle Version von REDAXO unter http://redaxo.org/de/download/ herunterladen. Informationen zum aktuellen Release gibt es unter https://github.com/redaxo/redaxo/releases.

<a name="upload"></a>
## Upload 

Das heruntergeladene Zip-File wird entpackt und der Inhalt in den Webordner deines lokalen Servers oder via FTP,SFTP, WebDAV auf deinen öffentlichen Webserver verschoben. Meist lautet der Webordner `httpdocs` , `htdocs` oder `html`. 
Ausführliche Informationen zum Upload und zu denZugangsdaten liefert der Hostingpartner.

> **Tipp:** Einige Hoster bieten zur Verwaltung des Webspaces auch Oberflächen wie PLESK oder CPANEL an. Hier enthalten ist auch einen Dateimanager, mit dem man die Zip-Datei direkt hochladen und auf dem Server entpacken kann. 


> **Hinweis für MAC und Linux-User:** Die versteckten .htaccess-Dateien müssen unbedingt mit übertragen werden. In einigen FTP-Programmen muss man diese erst einblenden. 

Die Ordner- und Dateirechte müssen auf `755` gestellt werden, falls der Server dies beim Upload nicht selbst erledigt haben sollte.

<a name="install"></a>
## Installationsvorgang

Nachdem REDAXO hochgeladen wurde, kann die Installation mit http://deinedomain.tld/redaxo/ aufgerufen werden. 
Die folgenden sieben Schritte führen durch die Installation. 

### Schritt 1: Sprachauswahl

Im  ersten Schritt wird die Sprache für den Installationsvorgang und für das Backend festgelegt. 

![Sprachwahl](/assets/v5.2.0-installation-01-language.png)

> **Hinweis :** Die Sprache kann später im Setup oder für den User geändert werden. 

### Schritt 2: Lizenz
REDAXO ist ein Open Source Projekt und kostenfrei. Allerdings gibt es Lizenzbedingungen, die akzeptiert werden müssen.

![Lizenz](/assets/v5.2.0-installation-02-license.png)
Schritt 2: Lizenz 

### Schritt 3: Systemcheck
An dieser Stelle führt die Installationsroutine einen Systemcheck durch und gibt ggf. Warnungen aus. Wenn etwas nicht stimmt, müssen eventuell auch die Systemvoraussetzungen überprüft werden.  

![Systemcheck](/assets/v5.2.0-installation-03-systemcheck.png)
Schritt 3: Systemcheck

**Hinweis für NGINX-Nutzer**
> Nutzer des NGINX-Webservers erhalten eine Fehlermeldung über nicht geschützte Ordner. REDAXO liefert für Apache die nötigen htaccess-Dateien selber mit. Für NGINX müssen die Direktiven selbst angelegt werden.

Direktiven für NGINX:
```
 location ^~ /redaxo/src { deny  all; }
 location ^~ /redaxo/data { deny  all; }
 location ^~ /redaxo/cache { deny  all; }
```
> Bei der Verwendung eines Rewriter-Addons bitte die Dokumentation des Addons beachten.


### Schritt 4: Konfiguration
An dieser Stelle wird die grundlegende Konfiguration durchgeführt. 
   
- URL der Website mit abschließendem /
- Name der Website  
- E-Mail-Adressse bei Fehlern
- Zeitzone
- Datenbankverbindung

Befindet sich die Datenbank auf dem lokalen Server, kann man hier `localhost` stehen lassen. Bei einigen Hostern sind der Webspace und die Datenbank voneinander getrennt. In diesem Fall muss man hier die Adresse des Datenbankservers eingeben. 
Besitzt der Datenbank-User das Recht, auch neue Datenbanken zu erstellen, so kann man hier direkt eine neue Datenbank mit der oben angegebenen Bezeichnung anlegen lassen. 

![Config](/assets/v5.2.0-installation-04-config.png)
Schritt 4: Systemcheck

### Schritt 5: Datenbank
Es muss eine der drei Optionen gewählt werden. 
> **Hinweis :** Eine Aktualisierung von REDAXO-Versionen kleiner als 5 ist aktuell nicht vorgesehen.

![Datenbank](/assets/v5.2.0-installation-05-database.png)
Schritt 5: Datenbank

### Schritt 6: Administrator
Nun muss ein Username und ein sicheres Passwort für den Administrator REDAXO-Installation definiert werden. Sichere Passwörter haben mehr als sechs Zeichen und beinhalten Groß- wie Kleinbuchstaben sowie Sonderzeichen. Auch sollte man nicht unbedingt `Admin` oder `Administrator` als Benutzername anlegen; diese sind leicht zu erraten.  

![Datenbank](/assets/v5.2.0-installation-06-1stuser.png)
Schritt 6: Administrator

### Schritt 7: Geschafft, Heureka, Hurra
Die Installation ist erfolgreich. Man sollte die weiteren Hinweise auf der Seite beachten und sich am besten direkt über den Button `Zum Login` anmelden. Alternativ kann man auch `/redaxo/` hinter die URL der Installation im Browser eingeben, um in das Backend zu gelangen. (Zum Beispiel *www.domain.xy/redaxo*)

![Datenbank](/assets/v5.2.0-installation-07-1stlogin.png)
Schritt 7: Ende


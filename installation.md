# Installation

- [Systemanforderungen](#system)
- [Schnellanleitung](#schnell)
- [Datenbank](#datenbank)
- [Download](#download)
- [Upload](#upload)
- [Installationsvorgang](#install)

<a name="system"></a>
## Systemanforderungen

Für die Version 5.3 wird folgende Umgebung benötigt:
- PHP ab Version: 5.5.9
- MySQL ab Version 5.5 oder MariaDB ab Version 10.0
- Apache2, Nginx oder vergleichbarer Webserver

<a name="schnell"></a>
## Schnellanleitung

Die folgenden Abschnitte erläutern das Vorgehen zur Installation von REDAXO auf einem Server oder Webspace.

- Eine MySQL-Datenbank erstellen und die Zugangsdaten notieren. 
- Die neueste Version unter https://redaxo.org/download/core/ herunterladen.
- Die ZIP-Datei auf dem eigenen Rechner entpacken.
- Die entpackten Dateien in das Webverzeichnis hochladen und die Installation unter der Adresse der Website mit angehängtem /redaxo/ (http://deinedomain.tld/redaxo/) ausführen.
- Alle [Installationschritte](#install) durchgehen.

<a name="datenbank"></a>
## Datenbank

Zunächst wird eine leere MySQL-Datenbank erstellt. Bei einigen Hostern ist bereits eine Datenbank angelegt, hierzu sollten die Zugangsdaten vorhanden sein. Für die Installation werden die Zugangsdaten (Datenbank-Name, Adresse des Servers, Datenbank-Benutzer und Passwort) für diese Datenbank benötigt.

<a name="download"></a>
## Download

Als Erstes die aktuelle Version von REDAXO unter https://redaxo.org/download/core/ herunterladen. Informationen zum aktuellen Release gibt es unter https://github.com/redaxo/redaxo/releases.

<a name="upload"></a>
## Upload 

Das heruntergeladene Zip-File wird entpackt und der Inhalt in den Webordner des lokalen Servers oder via FTP, SFTP, WebDAV auf einen öffentlichen Webserver kopiert. Meist lautet der Webordner `httpdocs` , `htdocs` oder `html`. 
Ausführliche Informationen zum Upload und zu den Zugangsdaten liefert der Hostingpartner.

> **Tipp:** Einige Hoster bieten zur Verwaltung des Webspaces auch Oberflächen wie PLESK oder CPANEL an. Hier enthalten ist auch ein Dateimanager, mit dem die Zip-Datei direkt hochgeladen und auf dem Server entpackt werden kann. 


> **Hinweis für MAC und Linux-User:** Die versteckten .htaccess-Dateien müssen unbedingt mit übertragen werden. In einigen FTP-Programmen müssen diese erst eingeblendet werden. 

Die Ordner- und Dateirechte müssen auf `755` gestellt werden, falls der Server dies beim Upload nicht selbst erledigt haben sollte.

<a name="install"></a>
## Installationsvorgang

Nachdem REDAXO hochgeladen wurde, kann die Installation mit http://deinedomain.tld/redaxo/ aufgerufen werden. 
Die folgenden sieben Schritte führen durch die Installation. 

### Schritt 1: Sprachauswahl

Im ersten Schritt wird die Sprache für den Installationsvorgang und für das Backend festgelegt. 

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
> Bei der Verwendung eines Rewriter-AddOns bitte die Dokumentation des Addons beachten.


### Schritt 4: Konfiguration
An dieser Stelle wird die grundlegende Konfiguration durchgeführt. 
   
- URL der Website mit abschließendem / (Slash)
- Name der Website  
- E-Mail-Adressse bei Fehlern
- Zeitzone
- Datenbankverbindung

Befindet sich die Datenbank auf dem lokalen Server, kann hier `localhost` stehen gelassen werden. Bei einigen Hostern sind der Webspace und die Datenbank voneinander getrennt. In diesem Fall muss hier die Adresse des Datenbankservers eingeben werden. 
Besitzt der Datenbank-User das Recht auch neue Datenbanken zu erstellen, so kann hier direkt eine neue Datenbank mit der oben angegebenen Bezeichnung anlegt werden.

![Config](/assets/v5.2.0-installation-04-config.png)
Schritt 4: Systemcheck

### Schritt 5: Datenbank
Es muss eine der drei Optionen gewählt werden. 
> **Hinweis :** Eine Aktualisierung von REDAXO-Versionen kleiner als 5 ist aktuell nicht vorgesehen.

![Datenbank](/assets/v5.2.0-installation-05-database.png)
Schritt 5: Datenbank

### Schritt 6: Administrator
Nun muss ein Username und ein sicheres Passwort für den Administrator der REDAXO-Installation definiert werden. Sichere Passwörter haben mehr als sechs Zeichen und beinhalten Groß- und Kleinbuchstaben sowie Sonderzeichen. Auch sollte nicht unbedingt `Admin` oder `Administrator` als Benutzername anlegt werden; diese sind zu leicht zu erraten.

![Datenbank](/assets/v5.2.0-installation-06-1stuser.png)
Schritt 6: Administrator

### Schritt 7: Heureka
Die Installation ist erfolgreich. Beachte die weiteren Hinweise auf der Seite. Die Erste Anmeldung kann nun direkt über den Button `Zum Login` erfolgen. Alternativ kann auch `/redaxo/` hinter die URL der Installation im Browser eingeben werden, um in das Backend zu gelangen. (Zum Beispiel *www.domain.xy/redaxo*)

![Datenbank](/assets/v5.2.0-installation-07-1stlogin.png)
Schritt 7: Ende

> ***Nach der Installation:*** Es ist durchaus möglich, dass nach einem Release noch Updates nachgereicht werden. Daher sollte nach der Installation im Installer geprüft werden, ob Aktualisierungen vorliegen.

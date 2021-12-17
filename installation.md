# Installation

* [Vorbereitung](#vorbereitung)
  * [Betrieb unter Apache](#apache)
  * [Betrieb unter Nginx](#nginx)
* [Installation per Zip-File](#zip)
  * [Schnellanleitung](#schnell)
  * [Datenbank](#datenbank)
  * [Download](#download)
  * [Upload](#upload)
* [Installation per REDAXO Loader](#loader)
* [Installationsvorgang](#install)
* [Installation per Kommandozeile](#console)
* [Docker](#docker)

<a name="vorbereitung"></a>

## Vorbereitung

Die Systemanforderungen zum aktuellen Release und vorheriger Releases sind unter <https://redaxo.org/download/core/> einsehbar. 

Einige Ordner müssen vor dem Zugriff von außen geschützt sein. 
Diese lauten: '/redaxo/src', '/redaxo/data', '/redaxo/cache', '/redaxo/bin'.
Das Vorgehen unterscheidet sich je Webserver-Typ und wird nachfolgend erklärt.


<a name="apache"></a>

### Betrieb unter Apache

Für Apache liefert REDAXO in die zuvor genannten Ordner `.htaccess`-Dateien aus. Damit diese greifen, sollte Apache die Verwendung der .htaccess-Dateien in den Einstellungen des Webspaces erlauben (`AllowOverride All`). 


<a name="nginx"></a>

### Betrieb unter Nginx

Wird REDAXO unter Nginx betrieben ist es erforderlich die Ornderrechte korrekt zu setzen, da hier die mitglieferten .htaccess-files nicht greifen. 

Folgende Direktiven sorgen für eine Sperrung der Ordner (Stand REDAXO 5.13): 

```
location ^~ /redaxo/src { deny  all; }
location ^~ /redaxo/data { deny  all; }
location ^~ /redaxo/cache { deny  all; }
location ^~ /redaxo/bin { deny  all; }
```

<a name="zip"></a>
<a name="schnell"></a>
## Installation per Zip-File

* Eine MySQL-Datenbank erstellen und die Zugangsdaten notieren.
* Die neueste Version unter <https://redaxo.org/download/core/> herunterladen.
* Die ZIP-Datei auf dem eigenen Rechner entpacken.
* Die entpackten Dateien in das Webverzeichnis hochladen und die Installation unter der Adresse der Website mit angehängtem /redaxo/ (<http://deinedomain.tld/redaxo/)> ausführen. 
* Alle [Installationschritte](#install) durchgehen.

<a name="datenbank"></a>

### Datenbank

Zunächst wird eine leere MySQL-Datenbank erstellt. Bei einigen Hostern ist bereits eine Datenbank angelegt, hierzu sollten die Zugangsdaten vorhanden sein. Für die Installation werden die Zugangsdaten (Datenbank-Name, Adresse des Servers, Datenbank-Benutzer und Passwort) für diese Datenbank benötigt.

<a name="download"></a>

### Download

Als Erstes die aktuelle Version von REDAXO unter <https://redaxo.org/download/core/> herunterladen. 
Informationen zum aktuellen Release gibt es unter <https://github.com/redaxo/redaxo/releases.>

<a name="upload"></a>

### Upload

Das heruntergeladene Zip-File wird entpackt und der Inhalt in den Webordner des lokalen Servers oder via FTP, SFTP, WebDAV auf einen öffentlichen Webserver kopiert. Meist lautet der Webordner `httpdocs` , `htdocs` oder `html`.

> Bei Upload per FTP/SFTP: Die Transfer-Einstellungen des FTP-Programms sollten auf binary/binär eingestellt sein.

Ausführliche Informationen zum Upload und zu den Zugangsdaten liefert der Hostingpartner.

> **Tipp:** Einige Hoster bieten zur Verwaltung des Webspaces auch Oberflächen wie Plesk oder cPanel an. Hier enthalten ist auch ein Dateimanager, mit dem die Zip-Datei direkt hochgeladen und auf dem Server entpackt werden kann.
> **Hinweis für Mac und Linux-User:** Die versteckten .htaccess-Dateien müssen unbedingt mit übertragen werden. In einigen FTP-Programmen müssen diese erst eingeblendet werden.

Jetzt kann man den [Installationsvorgang/Setup](#install) starten. 

<a name="loader"></a>
## Installation per REDAXO Loader

![Screenshot](/assets/v5.12.0-loader.png)

Der REDAXO-Loader bitetet einen vereinfachten Weg REDAXO auf einen Webspace zu kopieren.  Nach Auswahl der gewünschten REDAXO-Version wird diese bei GitHub heruntergeladen, entpackt und der [Installationsvorgang](#install) gestartet. 

> Der Loader wird bei Erfolg automatisch vom Server gelöscht.  

### Abruf über der Kommandozeile

```console
curl -JLO https://redaxo.org/loader
```

### Download des Loader per Browser

[redaxo-loader.php](https://redaxo.org/loader)


### Anwendung
- redaxo_loader.php in den Webspace laden
- redaxo_loader.php im Browser aufrufen
- REDAXO Version auswählen

Die erforderlichen Dateien werden auf den Server gespielt und der Installationsvorgang gestartet. 



<a name="install"></a>

## Installationsvorgang

Nachdem REDAXO hochgeladen wurde, kann die Installation mit <http://deinedomain.tld/redaxo/> aufgerufen werden.
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

**Hinweis bei Fehlermeldung zu nicht geschützte Ordnern**

Bitte den Abschnitt Vorbereitung beachten und die Rechte entsprechend setzen. 


### Schritt 4: Konfiguration

An dieser Stelle wird die grundlegende Konfiguration durchgeführt.

* URL der Website mit abschließendem / (Slash)
* Name der Website  
* E-Mail-Adressse bei Fehlern
* Zeitzone
* Datenbankverbindung

Befindet sich die Datenbank auf dem lokalen Server, kann hier `localhost` stehen gelassen werden. Bei einigen Hostern sind der Webspace und die Datenbank voneinander getrennt. In diesem Fall muss hier die Adresse des Datenbankservers eingeben werden.
Besitzt der Datenbank-User das Recht auch neue Datenbanken zu erstellen, so kann hier direkt eine neue Datenbank mit der oben angegebenen Bezeichnung anlegt werden.

![Config](/assets/v5.2.0-installation-04-config.png)

Schritt 4: Systemcheck

### Schritt 5: Datenbank

Es muss eine der vier Optionen gewählt werden.
Unterstützt der Datenbankserver utf8mb4, wird eine entsprechende Option zur Auswahl angeboten.

> **Hinweis :** Eine Aktualisierung von REDAXO-Versionen kleiner als 5 ist aktuell nicht vorgesehen.

![Datenbank](/assets/v5.9.0-installation-05-database.png)

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

<a name="console"></a>

## Installation über die Kommandozeile

REDAXO kann über die Konsole `redaxo/bin/console` installiert werdern. 

### Download und Entpacken

Beispiel für REDAXO 5.12. Download per Curl. 

**Download**
```console
curl -JLO  https://redaxo.org/download/redaxo/5.12.0.zip
```

**Entpacken**
```console
unzip redaxo_5.12.0.zip
```

### Setup starten

Die Konsole befindet sich im Ordner `redaxo/bin`

Der Befehl lautet `php console setup:run` für den interaktiven Modus.
Die Hilfe per `php console setup:run --help` liefert mögliche Optionen und Modi.

![Console Screenshot](/assets/v5.12.0-installation_console.png)

u.a.:

* `--quiet` für eine Unterdrückung aller Ausgaben
* `--no-interaction` für keine Interaktion

Die Options können kombiniert werden und so automatische Installationen realisiert werden. 

[Siehe: Konsole](/{{path}}/{{version}}/console)

> Mit der REDAXO Konsole können viele gängige Operationen durchführt werden, wie z. B. Installation, setzen von Config-Settings, Installation / Deinstallation von AddOns (packages)

<a name="docker"></a>

## Docker

![Docker Demos](/assets/v5.12.0-installation_docker.png)

REDAXO lässt sich auch über Docker installieren und testen. Im Docker Hub werden von Friends Of REDAXO (FOR) verschiedene Images angeboten:

Das REDAXO-Image liefert ein fertig installiertes CMS, ganz frisch und ohne Inhalte. Es steht in drei Varianten (Apache, FPM, Alpine) und für mehrere PHP-Versionen bereit. Eine Anleitung zur Installation ist enthalten.  
**REDAXO im Docker Hub:** [https://hub.docker.com/r/friendsofredaxo/redaxo](https://hub.docker.com/r/friendsofredaxo/redaxo)

Wer REDAXO nicht leer, sondern mit Beispiel-Inhalten installieren möchte, greift zu den drei beliebten Website-Demos, die innerhalb der Community entwickelt worden sind, um typische Anwendungsfälle für REDAXO aufzuzeigen: Die Basis-Demo für Einsteiger, die Community-Demo zur Einrichtung geschützter Nutzerbereiche und die Onepage-Demo mit drei Ansätzen zur Erstellung einer Website.  
**Website-Demos im Docker Hub:** [https://hub.docker.com/r/friendsofredaxo/demo](https://hub.docker.com/r/friendsofredaxo/demo)

Zur Einrichtung einer kompletten Entwicklungsumgebung für REDAXO bieten wir bei GitHub das Projekt »REDAXO mit Docker« an. Es führt Schritt für Schritt durch die Installation und liefert dabei nützliche Informationen. Deshalb eignet es sich hervorragend auch für den Einstieg ins Thema Docker.  
**Anleitung bei GitHub:** [REDAXO mit Docker](https://github.com/FriendsOfREDAXO/redaxo-mit-docker)

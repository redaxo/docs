# Socket Verbindung

* [Einleitung](#einleitung)
* [Beispiel](#beispiel)
* [Klassen](#klassen)
  * [rex_socket](#socket)
  * [rex_socket_proxy](#socketproxy)
  * [rex_socket_response](#socketresponse)
* [Methoden (rex_socket)](#methoden)
  * [factory](#factory)
  * [factoryUrl](#factoryurl)
  * [setPath](#setpath)
  * [setOptions](#setoptions)
  * [setTimeout](#settimeout)
  * [addBasicAuthorization](#addbasicauthorization)
  * [addHeader](#addheader)
  * [doRequest](#dorequest)
  * [doGet](#doget)
  * [followRedirects](#followredirects)
  * [doPost](#dopost)
  * [doDelete](#dodelete)
* [Methoden (rex_socket_proxy)](#methoden_socket_proxy)
  * [setDestination (nur mit rex_socket_proxy)](#setdestination)
  * [setDestinationUrl (nur mit rex_socket_proxy)](#setdestinationurl)
* [Methoden (rex_socket_response)](#methoden_socket_response)
  * [getBody (nur mit rex_socket_response)](#getbody)
  * [getBufferedBody (nur mit rex_socket_response)](#getbufferedbody)
  * [getHeader (nur mit rex_socket_response)](#getHeader)
  * [getStatusCode (nur mit rex_socket_response)](#getstatuscode)
  * [getStatusMessage (nur mit rex_socket_response)](#getstatusmessage)
  * [isClientError (nur mit rex_socket_response)](#isclienterror)
  * [isInformational (nur mit rex_socket_response)](#isinformational)
  * [isInvalid (nur mit rex_socket_response)](#isinvalid)
  * [isOK (nur mit rex_socket_response)](#isok)
  * [isRedirection (nur mit rex_socket_response)](#isredirection)
  * [isServerError (nur mit rex_socket_response)](#isservererror)
  * [isSuccessful (nur mit rex_socket_response)](#issuccessful)
  * [writeBodyTo (nur mit rex_socket_response)](#writebodyto)

<a name="einleitung"></a>
## Einleitung
`rex_socket` baut eine http- bzw. https-Verbindung zu einer Url oder Datei auf. Für Verbindungen über einen Proxy Server steht die Klasse `rex_socket_proxy` zur Verfügung. `rex_socket_response` ist nicht zur direkten Nutzung vorgesehen. Es wird von rex_socket aufgerufen, sobald ein Response abgesetzt wird (siehe [Klassen-](#klassen) und [Methodenbeschreibung](#methoden))


<a name="beispiel"></a>
## Beispiel
```php
try {
    //Baut die Verbindung auf. (Host, Port, SSL)
    $socket = rex_socket::factory('www.example.com',443, true);
    //Übergibt den Pfad an rex_socket
    $socket->setPath('/url/to/my/resource?param=1');
    //Übergib PHP Kontext-Optionen
    $socket->setOptions([
        'ssl' => [
            'verify_peer' => false,
            'verify_peer_name' => false
        ]
    ]);
    //Setzt einen Request ab und bekommt ein rex_socket_request-Objekt zurück
    $response = $socket->doGet();
    //Prüft, ob die Antwort 200 ist
    if($response->isOk()) {
        //liest die Informationen aus der Datei
        $body = $response->getBody();
    }
    //Gibt im Falle einer fehlerhaften Verbindung einen Fehler zurück
} catch(rex_socket_exception $e) {
    //error message: $e->getMessage()
}
```

<a name="klassen"></a>
## Klassen

<a name="socket"></a>
### rex_socket
Mit `rex_socket` wird eine klassische Socket-Verbindung hergestellt. Die zur Verfügung stehenden [Methoden](#methoden) sind weiter unten aufgeführt.

<a name="socketproxy"></a>
### rex_socket_proxy
Mit `rex_socket_proxy` kann man einzelne Verbindungen über einen ProxyServer herstellen. Diese Klasse erweitert `rex_socket` um die Methoden [setDestination](#setdestination) und [setDestinationUrl](#setdestinationurl).
> ### Tipp: Proxyserver für alle Verbindungen
> Sollen **alle Verbindungen** der gesamten Installation über einen Proxyserver übertragen werden ersetzt man in der config.yml `redaxo/data/core/config.yml` unter 'socket_proxy' den Value `null` mit dem gewünschten Proxyserver. Danach werden alle Verbindungen automatisch (auch Verbindungen über `rex_socket`) über diesen Proxy transferiert und der Einsatz von `rex_socket_proxy` ist nicht mehr nötig

<a name="socketresponse"></a>
### rex_socket_response
Immer wenn über `rex_socket` oder `rex_socket_proxy` ein Request abgesetzt wird ([doRequest](#dorequest), [doGet](#doget), [doPost](#dopost), [doDelete](#dodelete)) bekommt man ein rex_socket_response-Objekt zurück. Hier stehen weitere [Methoden](#methoden) zur Verfügung.


<a name="methoden"></a>
## Methoden

<a name="factory"></a>
### factory
`factory($host, $port, $ssl)`
Baut eine Socket-Instanz auf, die URL wird anschließend über 'setPath()' übergeben.
> ### Hinweis: Kein Protokoll angeben (http/https)
> Die Nutzung von SSL (HTTPS) wird über den 2. (Port) und 3. (SSL) Parameter gesteuert.
`rex_socket::factory('www.example.com',443, true)`



<a name="factoryurl"></a>
### factoryUrl
`factoryUrl($url)`
Baut eine Socket-Instanz direkt mit einer URL auf.


<a name="setpath"></a>
### setPath
`setPath($path)`
Übergibt den kompletten Pfad bei der Verbindung über `rex_socket::factory()` (beginnend mit /)

<a name="setoptions"></a>
### setOptions
`setOptions(array $options)`
Es können alle Kontextoptionen aus PHP (z.B. bindto, backlog, ipv6_v6only, so_reuseport, so_broadcast, tcp_nodelay) werden ([https://www.php.net/manual/de/context.php](https://www.php.net/manual/de/context.php))

<a name="settimeout"></a>
### setTimeout
`setTimeout($timeout)`
Übergibt die gewünschte Timeout-Zeit in s oder ms

<a name="addbasicauthorization"></a>
### addBasicAuthorization
`addBasicAuthorization($user, $password)`
Setzt einen Header mit Benutzername und Passwort zur Authentifizierung an einem geschützten Server

<a name="addheader"></a>
### addHeader
`addHeader($key, $value)`
Setzt die gewünschten Header im `$key, $value` Format. Zum Beispiel `addHeader('User-Agent', 'Mozilla/5.0 (Macintosh; Intel Mac OS X 12.4; rv:101.0) Gecko/20100101 Firefox/101.0') `

<a name="dorequest"></a>
### doRequest
`doRequest($method, $data)`
Setzt den Request ab. Für `get`, `post` und `delete`gibt es alternativ eigene Methoden.

<a name="doget"></a>
### doGet
`doGet()`
Setzt einen Get-Request ab.

<a name="followredirects"></a>
### followredirects (nur für Get-Requests)
`followRedirects($redirects)`
Übergibt die Anzahl der Redirects der gefolgt werden soll bevor die Verbindung abgebrochen wird.

<a name="dopost"></a>
### doPost
`doPost($data, array $files)`
Setzt einen Post-Request ab. Der Inhalt des Bodys kann als string, array oder callback übergeben werden. Dateien (mit Dateityp) können als Array übergeben werden.

<a name="dodelete"></a>
### doDelete
`doDelete()`
Setzt ein Delete-Request ab.

<a name="methoden_socket_proxy"></a>
## Methoden von rex_socket_proxy
Bei der Nutzung von `rex_socket_proxy` stehen zusätzlich zu den oben genannten Methoden zusätzlich folgende Methoden zur Verfügung.

<a name="setdestination"></a>
### setDestination
Wird die Verbindung über `rex_socket_proxy` aufgebaut, übergibt man mit `factory()` bzw. `factoryURL()` den Proxyserver. Die eigentliche Ziel-Url wird mit `setDestination()` übergeben.
`rex_socket_proxy::factoryUrl($proxyServer)->setDestination($host, $port, $ssl)`

<a name="setdestinationurl"></a>
### setDestinationUrl
Wird die Verbindung über `rex_socket_proxy` aufgebaut, übergibt man mit `factory()` bzw. `factoryURL()` den Proxyserver. Die eigentliche Ziel-Url wird mit `setDestinationUrl()` übergeben.
`rex_socket_proxy::factoryUrl($proxyServer)->setDestinationUrl($url)`

<a name="methoden_socket_response"></a>
## Methoden von rex_socket_response
Immer wenn ein Request abgesetzt wird ([doRequest](#dorequest), [doGet](#doget), [doPost](#dopost), [doDelete](#dodelete)) bekommt man ein rex_socket_response-Objekt zurück. Hier stehen weitere Methoden zur Verfügung mit denen die Serverantwort und der Inhalt der Datei verarbeitet werden kann.
<a name="getbody"></a>
### getBody
Die bevorzugte Methode um den Inhalt der Datei aufzurufen und zu verarbeiten. Im Hintergrund wird `getBufferedBody()` (siehe nächste Methode und die einzelnen Chunks in eine Variable geschrieben. Somit erhält man den kompletten Inhalt einer Datei ohen sich Gedanken über Speicher Probleme machen zu müssen. 

<a name="getbufferedbody"></a>
### getBufferedBody
Diese Methode wird von `getBody()` genutzt und ruft den Inhalt einer Datei in kleinen Teilen (Chunks) zu 1024 Zeichen ab um einen Speicherüberlauf zu vermeiden. Möchte man die Methode manuell nutzen muss man sie so oft aufrufen bis das Ergebnis `false` ist. Die Größe der Chunks lässt sich als Parameter mit übergeben `getBufferedBody(256)`

<a name="getHeader"></a>
### getHeader
`getHeader()` gibt den gesamten Header der geöffneten Datei zurück. Die einzelnen Values lassen sich durch Mitgeben des jeweiligen keys ausgeben. Zum Beispiel `getHeader('Date')

<a name="getstatuscode"></a>
### getStatusCode
`getStatusCode()` gibt ausschließlich den Statuscode der geöffneten Datei zurück.

<a name="getstatusmessage"></a>
### getStatusMessage
`geteStatusMessage()` gibt ausschließlich die StatusMessage der geöffneten Datei zurück.

<a name="isclineterror"></a>
### isClientError
Antwortet der Server mit einem StatusCode zwischen 400 und 500 wird `true` zurückgegeben, andernfalls `false`

<a name="isinformational"></a>
### isInformational
Antwortet der Server mit einem StatusCode zwischen 100 und 200 wird `true` zurückgegeben, andernfalls `false`

<a name="isinvalid"></a>
### isInvalid
Antwortet der Server mit einem StatusCode kleiner 100 oder größer 600 wird `true` zurückgegeben, andernfalls `false`


<a name="isok"></a>
### isOK
Antwortet der Server mit dem StatusCode 200 wird `true` zurückgegeben, andernfalls `false`


<a name="isredirection"></a>
### isRedirection
Antwortet der Server mit einem StatusCode zwischen 300 und 400 wird `true` zurückgegeben, andernfalls `false`


<a name="isservererror"></a>
### isServerError
Antwortet der Server mit einem StatusCode zwischen 500 und 600 wird `true` zurückgegeben, andernfalls `false`


<a name="issuccessful"></a>
### isSuccessful
Antwortet der Server mit einem StatusCode zwischen 200 und 300 wird `true` zurückgegeben, andernfalls `false`


<a name="writebodyto"></a>
### writeBodyTo
Schreibt den aberufenen Body in eine Datei `writeBodyTo($filname)` auf dem Server

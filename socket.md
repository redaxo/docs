# Socket Verbindung

* [Einleitung](#einleitung)
* [Beipsiel](#beispiel)
* [Klassen](#klassen)
  * [rex_socket](#socket)
  * [rex_socket_proxy](#socketproxy)
* [Methoden](#methoden)
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
  * [setDestination (nur mit rex_socket_proxy)](#setdestination)
  * [setDestinationUrl (nur mit rex_socket_proxy)](#setdestinationurl)

<a name="einleitung"></a>
## Einleitung
rex_socket baut eine http- bzw. https-Verbindung zu einer Url oder Datei auf. Für Verbindungen über einen Proxy Server steht die Klasse `rex_socket_proxy` zur Verfügung
> ### Tip: Proxy-Server für alle Verbindungen
> Sollen alle Verbindungen der gesamten Installation über einen Proxy-Server übertragen werden sollte man in derconfig.yml `redaxo/data/core/config.yml` unter 'socket_proxy' den Value `null`mit dem Proxy-Server ersetzen. Danach werden alle Verbindungen (auch Verbindungen über `rex_request` über diesen Proxy transferiert und der Einsatz von `rex_socket_proxy` ist nicht mehr nötig


<a name="beispiel"></a>
## Beispiel
```php
try {
    $socket = rex_socket::factory('www.example.com');
    $socket->setPath('/url/to/my/resource?param=1');
    $socket->setOptions([
        'ssl' => [
            'verify_peer' => false,
            'verify_peer_name' => false
        ]
    ]);
    $response = $socket->doGet();
    if($response->isOk()) {
        $body = $response->getBody();
    }
} catch(rex_socket_exception $e) {
    //error message: $e->getMessage()
}
```

<a name="klassen"></a>
## Klassen

<a name="socket"></a>
### rex_socket
Mit `rex_socket` wird eine klassische Verbindung zu einer Url hergestellt. Die zur Verfügung stehenden Methoden sind weiter unten aufgeführt.

<a name="socketproxy"></a>
### rex_socket_proxy
`rex_socket_proxy` eignet sich für die Verbindung über einen ProxyServer. Diese Klasse erweitert  `rex_socket` um die Methoden [setDestination](#setdestination) und [setDestinationUrl](#setdestinationurl).

<a name="methoden"></a>
## Methoden

<a name="factory"></a>
### factory
`factory($host, $port, $ssl)`
Baut eine Socket-Instanz auf, die URL wird anschließend über 'setUrl()' übergeben

<a name="factoryurl"></a>
### factoryUrl
`factoryUrl($url)`
Baut eine Socket-Instanz direkt mit einer URL auf.


<a name="setpath"></a>
### setPath
`setPath($path)`
Übergibt den kompletten Pfad bei der Verbindung über `rex_socket::factory()`

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

<a name="setdestination"></a>
### setDestination
Wird die Verbindung über `rex_socket_proxy` aufgebaut, übergibt man mit `factory()` bzw. `factoryURL()` den Proxyserver. Die eigentliche Ziel-Url wird mit `setDestination()` übergeben.
`rex_socket_proxy::factoryUrl($proxyServer)->setDestination($host, $port, $ssl)`


<a name="setdestinationurl"></a>
### setDestinationUrl (Pendant zu factoryUrl() )
Wird die Verbindung über `rex_socket_proxy` aufgebaut, übergibt man mit `factory()` bzw. `factoryURL()` den Proxyserver. Die eigentliche Ziel-Url wird mit `setDestinationUrl()` übergeben.
`rex_socket_proxy::factoryUrl($proxyServer)->setDestinationUrl($url)`


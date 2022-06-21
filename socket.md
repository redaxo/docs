# Socket Verbindung

* [Einleitung](#einleitung)
* [Beipsiel](#beispiel)
* [Beschreibung der Methoden](#methoden)
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


<a name="einleitung"></a>
## Einleitung
rex_socket baut eine http bzw. https Verbindung zu einer Url bzw. Datei auf. Die Verbindung wird über `rex_socket` hergestellt. Des Weiteren sind die Klassen `rex_socket_proxy`und rex_socket_response` verfügbar.


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
<a name="methoden"></a>
## Beschreibung der Methoden

<a name="factory"></a>
### factory
`factory($host, $port, $ssl)`
Baut eine Socket Instanz auf, die URL wird anschließend über 'setUrl()' übergeben

<a name="factoryurl"></a>
### factoryUrl
`factoryUrl($url)`
Baut eine Socket Instanz direkt mit einer kompletten URL auf.


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
Übergibt die gewünschte Timeout Zeit in s oder ms

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
# Requests

Die Request Funktionen werden in REDAXO verwendet, um mit den superglobalen Variablen `$_GET`, `$_POST`, `$_REQUEST`, `$_SERVER`, `$_COOKIE`, `$_ENV`, `$_SESSION` und `$_FILES` zu arbeiten. Die REDAXO Funktionen sollten bevorzugt verwendet werden, um die superglobalen Variablen abzufragen bzw. anzusprechen.

### Parameter der Funktionen rex_get, rex_post, rex_request, rex_files, rex_env, rex_cookie

Die Funktionen rex_get, rex_post, rex_request, rex_files, rex_env und rex_cookie können mit folgenden Parametern aufgerufen werden (Beispiel für rex_get):

```php
rex_get('var_name','var_type','default')
```

#### Für **var_type** sind folgende Werte gültig:

- string
- int
- integer
- bool
- boolean
- double
- float
- real-
- object
- array

Das Ergebnis wird dann in den entsprechenden Typ umgewandelt.

> **Hinweis:** Die Daten sollten in der weiteren Verarbeitung „gesäubert“ werden. Zum Beispiel sollten mit  `rex_get()`, `rex_post()` und `rex_request()` übernommene Strings vor der Ausgabe auf der Website mit `rex_escape($string)` bearbeitet werden, um mögliches HTML umzuwandeln. Damit wird Cross-Site-Scripting (XSS) verhindert.

Funktion | Beispiel | Erklärung
------------- | ------------- | -------------
rex_get  | `rex_get('meinevar','int',0)` | <http://example.com/meineseite?meinevar=456> => 456
rex_post  | `rex_post('meinevar','string','')` | liest aus $_POST['meinevar'] und gibt das Ergebnis als String zurück
rex_request  | `rex_request('meinevar','array',[])` | liest aus $_REQUEST['meinevar'][] und gibt das Ergebnis als Array zurück
rex_server | `rex_server('SERVER_NAME','string','')` | <http://example.com/meineseite> => example.com
rex_session | `rex_session('meine_var','string','')` | Liefert den zuvor mit rex_set_session in der Variablen meine_var gespeicherten Wert
rex_set_session | `rex_set_session('meine_var', $meine_var)` | Sichert den Inhalt von $meine_var als meine_var in der Session
rex_unset_session | `rex_unset_session('meine_var')` | Löscht meine_var aus der Session
rex_cookie  | `rex_cookie('meinevar','string','')` | liest aus $_COOKIE['meinevar'] und gibt das Ergebnis als String zurück
rex_files  | `rex_files('meinedatei','array',[])` | liest aus $_FILES['meinedatei'] und gibt das Ergebnis als Array zurück
rex_env  | `rex_env('meinevar','string','')` | liest aus $_ENV['meinevar'] und gibt das Ergebnis als String zurück
rex_request_method | `rex_request_method()` | liefert den Wert aus $_SERVER['REQUEST_METHOD'] falls gesetzt, Standard ist get
rex_request::isXmlHttpRequest | `rex_request::isXmlHttpRequest()` | Liefert true, wenn es sich um einen XMLHttpRequest handelt, andernfalls false. Der Wert wird bei Ajax Aufrufen aus den Frameworks Prototype, Mootools, jQuery (evtl. auch weitere) korrekt gesetzt.
rex_request::isPJAXRequest | `rex_request::isPJAXRequest()` | Liefert true, wenn $_SERVER['HTTP_X_PJAX'] true ist, ansonsten false
rex_request::isPJAXContainer | `rex_request::isPJAXContainer($containerId)` | Liefert true, wenn $_SERVER['HTTP_X_PJAX_CONTAINER'] gleich wie $containerId ist, ansonsten false.

Wird im Frontend eine Session benötigt, so muss diese explizit gestartet werden. Hierzu genügt in der Datei boot.php eines AddOns folgender Code:

```php
if (rex::isFrontend()) {
    rex_login::startSession();
}
```

alternativ

```php
if (!rex::isBackend()) {
    rex_login::startSession();
}
```

Beispiel: Code nur ein einziges Mal ausführen, wenn die Website aufgerufen wird.

```php
<?php
//Beim ersten Aufruf der Website wird die Session gestartet. Sie bleibt so lange aktiv, bis der Browser beendet wird.
rex_login::startSession();
if (rex_session('MeineVariable')) {
    //Code der ausgeführt ist, wenn die Variable gesetzt ist (direkt NACH dem ersten Aufruf der Website bis zum beenden des Browsers
} else {
    //Code der beim ersten Aufruf der Website ausgeführt wird bis die Variable 'MeineVariable' gesetzt ist
}
//Variable wird gesetzt
rex_set_session('MeineVariable', 'MeinWert');
```

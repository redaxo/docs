# Api

Über `rex_api_function` können AddOns eine zentrale API zur Verfügung stellen. Die Funktionen dieser API lassen sich jeweils über eine URL aufrufen. Sie dienen dazu, bestimmte Vorgaben, wie z.B. Nutzerrechte oder System-Einstellungen zu prüfen und den Aufruf bei Bedarf an einen dahinterliegenden Service (PHP-Klasse zur Verarbeitung) weiterzureichen. Rückmeldungen der Services können geprüft und als ausführliche Fehler- oder Erfolgsmeldung zurückgegeben werden, die dann von der aufrufenden Stelle ausgegeben werden können.

Da API-Funktionen über einen URL-Request aufgerufen werden, ist es möglich, sie über AJAX-Requests anzusprechen. Mit jedem Request kann nur eine API-Funktion aufgerufen werden.

## Aufruf

Der Aufruf einer API-Funktion kann auf jeder beliebigen Seite erfolgen. Um den Aufruf zu kennzeichnen, ist der Parameter `rex-api-function` nötig, über den der Name der aufzurufenden API-Funktion übergeben wird: `index.php?...&rex-api-call=function_name`. Der übergebene Name entspricht dabei dem Klassennamen ohne das vorangestellte `rex_api_`. Mit dem Aufruf können beliebige weitere Parameter zur Verarbeitung übergeben werden.

## Implementierung

- Jede API-Funktion wird durch eine PHP-Klasse repräsentiert. Der Klassenname muss mit `rex_api_` beginnen und die abstrakte Basisklasse `rex_api_function` erweitern. Es muss mindestens die Methode execute() definiert sein.
- Für die Fehlerausgabe gibt es die Exception-Klasse `rex_api_exception`.
- Für Rückmeldungen dient die Klasse `rex_api_result`.

```php
/**
 * Beispiel einer einfachen rex_api_function Implementierung
 *
 * Über diese API-Funktion kann der Name einer Kategorie ausgegeben werden, deren ID mit übergeben wird.
 * Falls die Kategorie nicht existiert, wird eine Fehlermeldung erzeugt.
 * Aufruf: index.php?rex-api-call=demo&category_id=XX
 */
class rex_api_demo extends rex_api_function
{
    public function execute()
    {
        // Hier wird die Kategorie anhand einer übergebenen ID ausgelesen
        $category_id = rex_request('category_id', 'int');
        $category = rex_category::get($category_id);

        // Falls die Kategorie nicht existiert, wird eine Fehlermeldung ausgelöst
        if (!$category instanceof rex_category) {
          throw new rex_api_exception('Kategorie existiert nicht!');
        }

        // Existiert die Kategorie, wird eine Meldung mit dem Namen der Kategorie zurückgegeben
        return new rex_api_result(true, 'Der Kategorie-Name lautet: '.$category->getName());
    }
}
```

### Explizite Registrierung von API-Funktionen

Seit REDAXO 5.17 können API-Funktionen auch explizit registriert werden. Dies ermöglicht die Verwendung von Namespaces und eine flexiblere Benennung:

```php
// Explizite Registrierung einer API-Funktion
rex_api_function::register('my-api', MyNamespace\MyApiClass::class);

// Aufruf über die registrierte Bezeichnung
// index.php?rex-api-call=my-api
```

**Vorteile der expliziten Registrierung:**

- **Namespaces**: API-Klassen können in Namespaces organisiert werden
- **Flexible Benennung**: Der API-Name muss nicht dem Klassennamen entsprechen
- **Bessere Organisation**: Strukturiertere Verwaltung von API-Funktionen

**Beispiel mit Namespace:**

```php
<?php
namespace MyAddon\Api;

class UserManager extends \rex_api_function
{
    public function execute()
    {
        $action = rex_request('action', 'string');
        
        switch ($action) {
            case 'activate':
                return $this->activateUser();
            case 'deactivate':
                return $this->deactivateUser();
            default:
                throw new \rex_api_exception('Invalid action');
        }
    }
    
    private function activateUser()
    {
        // Benutzer aktivieren
        return new \rex_api_result(true, 'User activated');
    }
    
    private function deactivateUser()
    {
        // Benutzer deaktivieren
        return new \rex_api_result(true, 'User deactivated');
    }
}

// Registrierung in der boot.php
rex_api_function::register('user-manager', MyAddon\Api\UserManager::class);
```

**Aufruf der registrierten API-Funktion:**

```
index.php?rex-api-call=user-manager&action=activate&user_id=5
```

> **Hinweis:** Bei der expliziten Registrierung wird die automatische Erkennung über den `rex_api_`-Präfix umgangen. Die Klassen können daher frei benannt werden.

## Die Methoden der Klassen

### rex_api_function

#### Methoden zur Verwendung innerhalb von rex_api_function

```php
// Funktioniert nur innerhalb von rex_api_function
// Gibt Namen der Funktion und ein CSRF Token zurück  
$url_params = rex_api_function::getUrlParams();

// Funktioniert nur innerhalb von rex_api_function
// Gibt den Namen der Funktion und ein CSRF-Token als verstecktes <input> feld zurück
echo rex_api_function::getHiddenFields();
```

### rex_api_result

Diese Klasse repräsentiert das Ergebnis einer API-Funktion. Sie stellt mehrere Methoden zur Definition des Ergebnisses bereit.
Das Ergebnis kann von der API-Funktion per `return` Statement zurückgegeben werden. Ein Ergebnis kann positiv (Ausführung erfolgreich) oder negativ (Ausführung fehlgeschlagen) sein.

#### Ergebnis erzeugen

```php
$result = new rex_api_result($status, $message);
```

Parameter | Beschreibung  
$status | Status des Ergebnisses. `true` = Ausführung erfolgreich, `false` = Ausführung fehlgeschlagen.
$message | _optional:_ Ausführlicher Nachricht. Z.B. zur Ausgabe für den Nutzer.

#### Status des Ergebnisses abfragen

```php
// Der Status ist bei Erfolg 'true'
$status = $result->isSuccessfull()
```

#### Nachricht ausgeben

```php
// Gibt die Nachricht ohne zusätzliche Formatierung aus
echo $result->getMessage();

// Gibt die Nachricht anhand des Parameters $status formatiert aus
// Erfolgsmeldungen werden mit rex_view::success() formatiert,
// Fehlschläge werden mit rex_view::error() formatiert
echo $result->getFormattedMessage();
```

#### Vor der Rückmeldung einen erneuten Request ausführen

```php
// Falls die Rückmeldung einen zusätzlichen Request erfordert, um z.B. Low-Level-Änderungen zu übernehmen, kann ein
// Flag gesetzt werden:
$result->setRequiresReboot($requires_reboot);

// Der Flag kann so abgefragt werden:
$result->requiresReboot();
```

Parameter | Beschreibung  
$requires_reboot | `false` = keinen neuen Request vor Rückgabe ausführen (Standard). `true` = einen neuen Request vor Rückgabe ausführen. Der zusätzliche Request wird automatisch von rex_api_function ausgeführt.

#### Ergebnis JSON kodieren

```php
// Ergebnis kodieren
// Wandelt die Daten eines rex_api_result Objektes in einen JSON-String
$json = $result->toJSON();

// Ergebnis dekodieren
// Wandelt ein JSON kodiertes Ergebnis zurück in ein rex_api_result Objekt.
$result = rex_api_result::fromJSON($json);
```

### rex_api_exception

Diese Exception kann abgefangen werden. Im Normalfall wird sie von REDAXO als Whoops-Meldung ausgeben.

## rex_article_slice

Die Klasse `rex_article_slice` stellt Methoden zum Arbeiten mit Artikel-Slices zur Verfügung.

### Slice-Status abfragen

Mit der Methode `getStatus()` kann der Status (online/offline) eines Slices abgefragt werden:

```php
$slice = rex_article_slice::getArticleSliceById($slice_id);
if ($slice) {
    $status = $slice->getStatus();
    // Status: 1 = online, 0 = offline
}
```

### Offline-Slices ignorieren

Viele Methoden der `rex_article_slice` Klasse unterstützen einen zusätzlichen Parameter `$ignoreOfflines`, um offline geschaltete Slices zu ignorieren:

```php
// Nur online Slices eines Artikels abrufen
$slices = rex_article_slice::getSlicesForArticle($article_id, $clang, $revision, true);

// Nur online Slices eines bestimmten Modultyps abrufen
$slices = rex_article_slice::getSlicesForArticleOfType($article_id, $module_id, $clang, $revision, true);

// Erstes online Slice für einen Artikel finden
$slice = rex_article_slice::getFirstSliceForArticle($article_id, $clang, $revision, true);

// Erstes online Slice für einen Ctype finden
$slice = rex_article_slice::getFirstSliceForCtype($ctype, $article_id, $clang, $revision, true);

// Nächstes/Vorheriges online Slice abrufen
$nextSlice = $slice->getNextSlice(true);
$prevSlice = $slice->getPreviousSlice(true);
```

**Parameter:**
- `$ignoreOfflines` (boolean): `true` = nur online Slices berücksichtigen, `false` = alle Slices (Standard)

# Queries - rex_sql

- [Queries - rex_sql](#queries_rex_sql)
- [Überschriften](#ueberschriften)
- [Links](#links)
- [Listen](#listen)
- [Tabellen](#tabellen)
- [Code](#code)
- [Hinweise](#hinweise)
- [Anker 3](#anker-3)
    - [Anker 3a](#anker-3a)
    - [Anker 3b](#anker-3b)
    - [Anker 3c](#anker-3c)
- [Anker 4](#anker-4)

<a name="queries_rex_sql"></a>
## Queries - rex_sql

Die Klasse `rex_sql` ist der Datenbankwrapper, über den REDAXO alle Datenbankzugriffe erzeugt und verwaltet. Die Klasse steht dem Entwickler für eigene Datenbankzugriffe zur Verfügung. Es wird empfohlen alle Datenbankzugriffe über diese Klasse vorzunehmen. Sowohl im Frontend als auch im Backend besteht eine aktive Datenbankverbindung, die für die Zugriffe genutzt werden kann.

### Syntax

In der rex_sql Klasse werden häufig Parameter in der Form `function($query, $params)` verwendet. Es wird empfohlen die Werte an den Query über die params zu übergeben.

Beispiel:
```
$sql = rex_sql::factory();
$sql->setQuery('SELECT name, id FROM rex_article WHERE parent_id = :pid', ['pid'=>5]);
```


<a name="getquerytype"></a>
## getQueryType

`getQueryType($qry)`

Gibt den Typ der Abfrage $sql zurück oder `false` wenn die Abfrage keinen Typ enthält.

Mögliche Rückgabewerte sind SELECT, SHOW, UPDATE, INSERT, DELETE, REPLACE, CREATE, CALL, OPTIMIZE oder false. Die Syntax wird nicht geprüft.

<a name="datetime"></a>
## datetime

`datetime($timestamp = null)`

Gibt einen Datumsstring im SQL Datetime Format (Y-m-d H:i:s) aus dem übergebenen Timestamp zurück. Standard ist die aktuelle Zeit.

<a name="setdbquery"></a>
## setDBQuery

`setDBQuery($query, array $params = [], array $options = [])`

Setzt eine Abfrage ($query) ab, wechselt die DBID falls vorhanden und stellt sie anschließ

Beispiel:
```
$sql = rex_sql::factory();
$sql->setDBQuery('SELECT id, name FROM rex_article WHERE id > :id',['id'=>5]);
```

<a name="setdebug"></a>
## setDebug

`setDebug($debug = true)`

Schaltet die Debug Funktion von rex_sql ein. Damit wird das rex_sql Objekt bei ausgeführter Query per dump() ausgegeben.

<a name="preparequery"></a>
## prepareQuery

`prepareQuery($qry)`

Erstellt aus einer übergebenen SQL Abfrage ein PDO Statement.

<a name="execute"></a>
## execute

`execute(array $params = [], array $options = [])`

Führt das vorbereitete Statement aus. Im Fehlerfall wird eine Exception vom Typ rex_sql_exception erzeugt. Mit dem Parameter `$options` kann das Pufferverhalten beeinflusst werden.

```
$sql = rex_sql::factory();
$sql->prepareQuery('SELECT id, name FROM rex_article WHERE id > :id');
$sql->execute(['id'=>10]);
```

Das Beispiel setzt eine Abfrage mit Platzhaltern. Die Werte für die Platzhalter werden mit `execute` übergeben. Damit lässt sich dann beispielsweise eine Abfrage mehrfach verwenden, indem die Parameter verändert werden.

<a name="setquery"></a>
## setQuery

`setQuery($query, array $params = [], array $options = [])`

Setzt die SQL Query, übernimmt die Parameter, setzt das Objekt mit `flush` zurück und führt das Statement aus.

```
$res = $sql->setQuery('SELECT id, name FROM rex_article WHERE id > :id',['id'=>10]);
```

<a name="settable"></a>
## setTable

`setTable($table)`

Setzt den Tabellennamen und gibt das rex_sql Objekt zurück.

<a name="setrawvalue"></a>
## setRawValue

`setRawValue($colName, $value)`

Setzt den Raw Wert einer Tabelle und gibt das rex_sql Objekt zurück.

<a name="setvalue"></a>
## setValue

`setValue($colName, $value)`

Setzt einen einzelnen Wert `value` für eine Spalte `colName` und gibt das rex_sql Objekt zurück.

<a name="setarrayvalue"></a>
## setArrayValue

`setArrayValue($colName, array $value)`

Setzt den Inhalt eines Arrays `value` für eine Spalte `colName`. Der Wert wird per `json_encode` codiert.

<a name="setdatetimevalue"></a>
## setDateTimeValue

`setDateTimeValue($colName, $timestamp)`

Formatiert einen `timestamp` in das SQL Datumsformat und setzt ihn für die Spalte `columnName`. Das rex_sql Objekt wird zurückgegeben.

<a name="setvalues"></a>
## setValues

`setValues(array $valueArray)`

Setzt ein Array als Inhalt. Der Schlüssel des Arrays muss dem passenden Feldnamen der Tabelle entsprechen.



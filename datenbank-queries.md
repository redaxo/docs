# Queries - rex_sql

- [Queries - rex_sql](#queries_rex_sql)
  - [Syntax](#syntax)
  - [Rückgabewerte](#rueckgabewerte)
- [getQueryType](#getquerytype)
- [datetime](#datetime)
- [setDBQuery](#setdbquery)
- [setDebug](#setdebug)
- [prepareQuery](#preparequery)
- [execute](#execute)
- [setQuery](#setquery)
- [setTable](#settable)
- [setRawValue](#setrawvalue)
- [setValue](#setvalue)
- [setArrayValue](#setarrayvalue)
- [setDateTimeValue](#setdatetimevalue)
- [setValues](#setvalues)
- [setArrayValue](#setarrayvalue)
- [setDateTimeValue](#setdatetimevalue)
- [setValues](#setvalues)
- [hasValues](#hasvalues)
- [isValueOf](#isvalueof)
- [setWhere](#setwhere)
- [getValue](#getvalue)
- [getArrayValue](#getarrayvalue)
- [getDateTimeValue](#getdatetimevalue)
- [getRow](#getrow)
- [getTables](#gettables)
- [getTablesAndViews](#gettablesandviews)
- [hasValue](#hasvalue)
- [in](#in)
- [isNull](#isnull)
- [getRows](#getrows)
- [getFields](#getfields)
- [getWhere](#getwhere)
- [select](#select)
- [update](#update)
- [insert](#insert)
- [replace](#replace)
- [delete](#delete)
- [flush](#flush)
- [flushValues](#flushvalues)
- [hasNext](#hasnext)
- [reset](#reset)
- [getLastId](#getlastid)
- [getDBArray](#getdbarray)
- [getArray](#getarray)
- [getErrno](#geterrno)
- [getMysqlErrno](#getmysqlerrno)
- [getError](#geterror)
- [hasError](#haserror)
- [setNewId](#setnewid)
- [getFieldnames](#getfieldnames)
- [getTablenames](#gettablenames)
- [escape](#escape)
- [escapeIdentifier](#escapeidentifier)
- [addGlobalUpdateFields](#addglobalupdatefields)
- [addGlobalCreateFields](#addglobalcreatefields)
- [rewind](#rewind)
- [current](#current)
- [key](#key)
- [next](#next)
- [valid](#valid)
- [showCreateTable](#showcreatetable)
- [showTables (deprecated)](#showtables)
- [showColumns](#showcolumns)
- [getServerVersion](#getserverversion)
- [factory](#factory)
- [checkDbConnection](#checkdbconnection)

<a name="queries_rex_sql"></a>

## Queries - rex_sql

Die Klasse `rex_sql` ist der Datenbankwrapper, über den REDAXO alle Datenbankzugriffe erzeugt und verwaltet. Die Klasse steht dem Entwickler für eigene Datenbankzugriffe zur Verfügung. Es wird empfohlen alle Datenbankzugriffe über diese Klasse vorzunehmen. Sowohl im Frontend als auch im Backend besteht eine aktive Datenbankverbindung, die für die Zugriffe genutzt werden kann.

### Syntax

In der rex_sql Klasse werden häufig Parameter in der Form `function($query, $params)` verwendet. Es wird empfohlen die Werte an den Query über die params zu übergeben.

Beispiel:

```php
$sql = rex_sql::factory();
$sql->setQuery('SELECT name, id FROM rex_article WHERE parent_id = :pid', ['pid'=>5]);
```

### Rückgabewerte

Die meisten Funktionen geben das aktuelle rex_sql Objekt zurück.

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

Setzt eine Abfrage ($query) ab und wechselt die DBID falls vorhanden.

Beispiel:

```php
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

```php
$sql = rex_sql::factory();
$sql->prepareQuery('SELECT id, name FROM rex_article WHERE id > :id');
$sql->execute(['id'=>10]);
```

Das Beispiel setzt eine Abfrage mit Platzhaltern. Die Werte für die Platzhalter werden mit `execute` übergeben. Damit lässt sich dann beispielsweise eine Abfrage mehrfach verwenden, indem die Parameter verändert werden.

<a name="setquery"></a>

## setQuery

`setQuery($query, array $params = [], array $options = [])`

Setzt die SQL Query, übernimmt die Parameter, setzt das Objekt mit `flush` zurück und führt das Statement aus.

```php
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

<a name="setarrayvalue"></a>

## setArrayValue

`setArrayValue($colName, array $value)`

Ein Array in der Datenbank ablegen. Der Wert von array wird per `json_encode` codiert. Siehe auch `getArrayValue`

<a name="setdatetimevalue"></a>

## setDateTimeValue

`setDateTimeValue($colName, $timestamp)`

Legt in der Spalte `$colName` einen Timestamp im Format `Y-m-d H:i:s` ab. Wird in `$timestamp` kein Wert übergeben, wird der aktuelle Unix Timestamp verwendet.

<a name="setvalues"></a>

## setValues

`setValues(array $valueArray)`

Ein assoziatives Array ablegen, wobei die `keys` den Feldnamen entsprechen, die `values` den Werten.

`$sql->setValues(['vorname'=>'Rupert','nachname'=>'Neudeck']);`

<a name="hasvalues"></a>

## hasValues

`hasValues()`

Gibt `true` zurück, wenn das rex_sql Objekt Werte enthält, ansonsten `false`. Es sind keine Parameter erlaubt.

<a name="isvalueof"></a>

## isValueOf

`isValueOf($feld, $prop)`

Prüft den Wert einer Spalte der aktuellen Zeile ob ein Wert enthalten ist. Wenn für `$prop = ""` übergeben wird, wird stets `true` zurückgegeben.

<a name="setwhere"></a>

## setWhere

`setWhere($where, $whereParams = null)`

Setzt die `WHERE`-Bedingung der Abfrage.

`$sql->setWhere(['id' => 3, 'field' => '']);` ergibt `id = 3 AND field = ''`
`$sql->setWhere([['id' => 3, 'field' => '']]);` ergibt `id = 3 OR field = ''`

mit Parameter:
`$sql->setWhere('myid = :id OR anotherfield = :field', ['id' => 3, 'field' => '']);` ergibt `myid = 3 OR anotherfield = ''`

Es wird **nicht empfohlen** den gesamten Where-String mit Parametern und Werten zu übergeben:
`$sql->setWhere('myid="35" OR abc="zdf"');` (deprecated)

<a name="getvalue"></a>

## getValue

`getValue($colName)`

Gibt den Wert von `colName` des aktuellen Datensatzes zurück. Wird für `colName` kein Wert übergeben, wird ein Fehler vom Typ `rex_sql_exception` generiert.

Wenn der Name des Feldes in der Form `tablename.fieldname` übergeben wurde, wird direkt auf den Tabellennamen zugegriffen. Andernfalls versucht die Funktion den Feldnamen in der Abfrage zu finden. Ist dieser nicht eindeutig, wird ein Fehler generiert.

<a name="getarrayvalue"></a>

## getArrayValue

`getArrayValue($colName)`

Das in `colName` abgelegte Array wird per `json_decode` decodiert und zurückgegeben. Sie auch `setArrayValue`.

<a name="getdatetimevalue"></a>

## getDateTimeValue

`getDateTimeValue($colName)`

Gibt den in `colName` abgelegte als String abgelegten Datum-Zeit Wert als Unix Timestamp zurück. Siehe auch `setDateTimeValue`.

<a name="getrow"></a>

## getRow

`getRow($fetch_type = PDO::FETCH_ASSOC)`

Gibt den Wert der aktuellen Zeile zurück. Über `fetch_type` kann festgelegt werden von welchem Typ das Ergebnis ist. So gibt `PDO::FETCH_OBJ` das Ergebnis als Objekt zurück. Standard ist `PDO::FETCH_ASSOC`, womit ein assoziatives Array zurückgegeben wird.

<a name="hasvalue"></a>

## hasValue

`hasValue($feldname)`

Prüft, ob eine Spalte vorhanden ist. Gibt `true` zurück, wenn die Spalte gefunden wurde, `flase`, wenn sie nicht gefunden wurde. Die Funktion kann auch mit einem vorangestellten Alias aufgerufen werden: `tablename.feldname`.

<a name="in"></a>

## in

`in(array $values)`

Bereitet ein Array von ints und/oder strings vor für den Einsatz in einem mysql IN (...) statement:

```php 
$sql = rex_sql::factory();
$sql->setQuery('SELECT * FROM my_table WHERE my_col IN ('.$sql->in(['foo', 'bar']).')');
```

<a name="isnull"></a>

## isNull

`isNull($feldname)`

Prüft, ob das Feld mit dem Namen `feldname` null ist. Es wird `true` oder `false` zurückgegeben.

<a name="getrows"></a>

## getRows

`getRows()`

Gibt die Anzahl der Zeilen für eine gesetze Abfrage zurück.

<a name="getfields"></a>

## getFields

`getFields()`

Gibt die Anzahl der Spalten für eine gesetze Abfrage zurück.

<a name="getwhere"></a>

## getWhere

`getWhere()`

Gibt das aktuelle `where` Statement zurück.

<a name="select"></a>

## select

`select($fields = '*')`

Setzt eine Select-Abfrage auf die aktuelle Tabelle mit dem aktuellen `where` Statement ab. Die Angabe von `fields` ist optional, Standard ist `*`.

<a name="update"></a>

## update

`update()`

Setzt eine Update-Anweisung auf die angegebene Tabelle mit den gesetzten Werten (z.B. mit `setValue` oder `setValues`) und mit `setWhere` gesetzten WHERE Parametern ab.

<a name="insert"></a>

## insert

`insert()`

Setzt eine Insert-Anweisung auf die angegebene Tabelle mit den gesetzten Werten (z.B. mit `setValue` oder `setValues`). Bei Verstoß gegen eine NOT NULL Regel wird eine rex_sql_exception ausgelöst.

<a name="replace"></a>

## replace

`replace()`

Setzt eine Replace-Anweisung auf die angegebene Tabelle mit den gesetzten Werten (z.B. mit `setValue` oder `setValues`) und mit `setWhere` gesetzten WHERE Parametern ab.

<a name="delete"></a>

## delete

`delete()`

Setzt eine Delete-Anweisung auf die angegebene Tabelle mit den WHERE Parametern ab, die mit `setWhere` gesetzten wurden.

<a name="flush"></a>

## flush

`flush()`

Setzt alle Werte auf den Ursprungszustand zurück. Gibt das rex_sql Objekt zurück.

<a name="flushvalues"></a>

## flushValues

`flushValues()`

Stellt alle Values, die mit `setValue` oder `setValues` gesetzt wurden, zurück.

<a name="hasnext"></a>

## hasNext

`hasNext()`

Gibt `true` zurück, wenn das Resultset einen weiteren Datensatz enthält, ansonsten `false`.

<a name="reset"></a>

## reset

`reset()`

Setzt den Cursor des Resultsets zurück zum Anfang. Identisch mit `rewind`.

<a name="getlastid"></a>

## getLastId

`getLastId()`

Gibt die letzte InsertId zurück.

<a name="getdbarray"></a>

## getDBArray

`getDBArray($query = null, array $params = [], $fetchType = PDO::FETCH_ASSOC)`

Lädt das komplette Resultset in ein Array und gibt dieses zurück. Wechselt die DBID, falls vorhanden. Identisch mit `getArray`.

<a name="getarray"></a>

## getArray

`getArray($query = null, array $params = [], $fetchType = PDO::FETCH_ASSOC)`

Lädt das komplette Resultset in ein Array und gibt dieses zurück. Wechselt die DBID, falls vorhanden. Identisch mit `getDBArray`.

<a name="geterrno"></a>

## getErrno

`getErrno()`

Gibt die zuletzt aufgetretene Fehlernummer zurück.

<a name="getmysqlerrno"></a>

## getMysqlErrno

`getMysqlErrno()`

Gibt die treiberspezifische MySql Fehlernummer zurück.

<a name="geterror"></a>

## getError

`getError()`

Gibt ein Array mit Informationen des zuletzt aufgetretenen Fehlers zurück. Der Aufbau des Arrays entspricht folgendem Muster:

```text
[0] => 5-stelliger Fehlercode
[1] => Fehlernummer des MySQL Treibers
[2] => Fehlerbeschreibung
```

<a name="haserror"></a>

## hasError

`hasError()`

Prüft, ob ein Fehler aufgetreten ist. Bei einem Rückgabewert von `true` ist ein Fehler aufgetreten, bei `false` nicht.

<a name="setnewid"></a>

## setNewId

`setNewId($field, $start_id = 0)`

Setzt eine Spalte auf den nächstmöglichen `auto_increment` Wert. Um zu verhindern, dass das rex_sql Objekt verändert wird, wird in dieser Funktion ein eigenes rex_sql Objekt verwendet.

<a name="getfieldnames"></a>

## getFieldnames

`getFieldnames()`

Gibt die Spaltennamen des Resultsets zurück.

<a name="gettablenames"></a>

## getTablenames

`getTablenames()`

Gibt die Tabellennamen des Resultsets zurück.

<a name="escape"></a>

## escape

`escape($value)`

Escaped den übergeben Wert für den DB Query.

<a name="escapeidentifier"></a>

## escapeIdentifier

`escapeIdentifier($name)`

Escaped den übergebenen Wert und fügt Backticks am Anfang und am Ende dazu.

Aus `"Das sind Backticks: ``"` wird `"``Das sind Backticks: `````"`

<a name="addglobalupdatefields"></a>

## addGlobalUpdateFields

`addGlobalUpdateFields($user = null)`

Standardfelder `updatedate` und `updateuser` setzen. `updatedate` ist der aktuelle Wert von time() als Date Time String (über `setDateTimeValue`).
`user` ist standardmäßig der Login Name des aktuellen REDAXO Backend User oder ein übergebener String.

<a name="addglobalcreatefields"></a>

## addGlobalCreateFields

`addGlobalCreateFields($user = null)`

Standardfelder `createdate` und `createuser` setzen. `createdate` ist der aktuelle Wert von time() als Date Time String (über `setDateTimeValue`).
`user` ist standardmäßig der Login Name des aktuellen REDAXO Backend User oder ein übergebener String.

<a name="rewind"></a>

## rewind

`rewind()`

Setzt den Cursor des Resultsets zurück zum Anfang. Identisch mit `reset`.

<a name="current"></a>

## current

`current()`

Gibt das aktuelle rex_sql Objekt zurück.

<a name="key"></a>

## key

`key()`

Gibt den aktuellen Wert des Zeigers im Resultset zurück.

<a name="next"></a>

## next

`next()`

Setzt den Zeiger im Resultset um einen Datensatz vor.

<a name="valid"></a>

## valid

`valid()`

Gibt `true` zurück, wenn das Resultset einen weiteren Datensatz enthält, ansonsten `false`. Identisch mit `hasNext`.

<a name="showcreatetable"></a>

## showCreateTable

`rex_sql::showCreateTable($table, $DBID = 1)` (public static)

Erstellt das CREATE TABLE Statement um die Tabelle `$table` der Datenbankverbindung `$DBID` zu erstellen. Die Tabelle `$table` muss vorhanden sein, sonst wird ein Fehler ausgegeben.

<a name="showtables"></a>

## showTables (deprecated)

`rex_sql::showTables($DBID = 1, $tablePrefix = null)` (public static)

Sucht alle Tabellen der Datenbankverbindung `$DBID`. Falls `$tablePrefix` gesetzt ist, werden nur dem Prefix entsprechende Tabellen gesucht. Es wird ein Array mit den Namen aller in der Datenbank vorhandenen Tabellen zurückgegeben.

Die Funktion ist seit Version 5.6.2 deprecated. Es wird die Verwendung der nicht statischen Funktion `getTablesAndViews` empfohlen.

<a name="gettables"></a>

## getTables

`$sql->getTables($tablePrefix = null)`

Sucht alle Tabellen der Datenbankverbindung `$DBID`. Falls $tablePrefix gesetzt ist, werden nur dem Prefix entsprechende Tabellen gesucht. Als Rüclgabe erhält man ein Array der Tabellennamen.

<a name="gettablesandviews"></a>

## getTablesAndViews

`$sql->getTablesAndViews($tablePrefix = null)`

Sucht alle Tabellen der Datenbankverbindung `$DBID`. Falls `$tablePrefix` gesetzt ist, werden nur dem Prefix entsprechende Tabellen gesucht. Es wird ein Array mit den Namen aller in der Datenbank vorhandenen Tabellen und Views zurückgegeben. Ersetzt die statische Funktion `showTables`.

<a name="showcolumns"></a>

## showColumns

`rex_sql::showColumns($table, $DBID = 1)` (public static)

Gibt ein Array mit den Spalten der Tabelle `$table` zurück. Die Spalten werden ebenfalls als Array zurückgegeben.

```php
 [
 [0] => [
  "name" => "pid",
  "type" => "int(11)",
  "null" => "NO",
  "key" => "PRI",
  "default" => null,
  "extra" => "auto_increment"
  ],
 [1] => [
  "name" => "id",
  "type" => "int(11)",
  "null" => "NO",
  "key" => "MUL",
  "default" => null,
  "extra" => ""
  ]
]
```

<a name="getserverversion"></a>

## getServerVersion

`getServerVersion($DBID = 1)` (public static)

Gibt die Serverversion zurück.

<a name="factory"></a>

## factory

`factory($DBID = 1)` (public static)

Factory Methode. Erstellt eine neue Instanz des rex_sql Objekte und gibt diese zurück.

Standardmäßig wird auf die im System definierte Datenbankresource zugegriffen, die auch von REDAXO selbst genutzt wird. Optional unterstützt REDAXO eine weitere Datenbankquelle. Die Konfiguration kann in der Datei `redaxo/data/core/config.yml` eingetragen werden. Diese Datenbank ist dann über `$sql2 = rex_sql::factory(2)` angesprochen werden.

<a name="checkdbconnection"></a>

## checkDbConnection

`checkDbConnection($host, $login, $pw, $dbname, $createDb = false)` (public static)

Prüft die übergebenen Zugangsdaten auf Gültigkeit und legt ggf. die Datenbank an.

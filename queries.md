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

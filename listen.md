# Listen

* [Tabellen `rex_list` ](#rex-list)
* [Listenansicht von Datenbank-Tabellen](#listenansicht)
  + [Aufruf von rex_list und Parameter](#aufruf_von_rex_list)
  + [Ein einfaches Beispiel](#einfaches_beispiel)
  + [Formatierung und Verhalten der Liste](#beschreibung_der_methoden)
    - [addColumn](#addcolumn)
    - [addLinkAttribute](#addlinkattribute)
    - [addParam](#addparam)
    - [addTableAttribute](#addtableattribute)
    - [addTableColumnGroup](#addtablecolumngroup)
    - [getColumnLabel](#getcolumnlabel)
    - [setColumnLabel](#setcolumnlabel)
    - [getHeader()](#getheader)
    - [getUrl](#geturl)
    - [getParsedUrl](#getparsedurl)
    - [removeColumn](#removecolumn)
    - [setCaption](#setcaption)
    - [setRowAttributes](#setrowattributes)
    - [getRowAttributes](#getrowattributes)
    - [setColumnFormat](#setcolumnformat)
    - [setColumnParams](#setcolumnparams)
    - [setColumnSortable](#setcolumnsortable)
    - [setColumnPosition](#setcolumnposition)
    - [setNoRowsMessage](#setnorowsmessage)
  + [Ausgabe der Liste](#ausgabe_der_liste)
  + [Extension Point](#extension_point)
* [Ausgabe einer rex_list in einem Fragment](#ausgabe_im_fragment)
* [Ausgabe mehrerer rex_list-Instanzen mit Paginierung](#ausgabe_multiple)

 
<a name="rex-list"></a>

## Tabellen rex_list

<a name="listenansicht"></a>

## Listenansicht von Datenbank-Tabellen

Die Klasse `rex_list` ist eines der "heimlichen Heinzelmännchen" von REDAXO. Mit `rex_list` können die Ergebnisse Datenbankabfragen als tabellarische Listen dargestellt werden. Die Verwendung von `rex_list` kann sowohl im Backend als auch im Frontend sinnvoll sein.

Eine Listenansicht kann über die `rex_list` -Klassen mit verschiedenen Funktionen ausgestattet werden, z. B. mit einer Sortierfunktion für bestimmte Spalten oder mit Links, um Datensätze zu editieren, zu löschen oder mit eigenen Funktionen zu manipulieren. Die Klasse verfügt von Haus aus über eine Paging-Funktion über die Klasse `rex_pager` .

<a name="aufruf_von_rex_list"></a>

### Aufruf von rex_list und Parameter

Ein Listenobjekt erzeugen:

``` php
$list = rex_list::factory($query, $rowsPerPage, $listName, $debug);
```

| Parameter      | Erklärung                                                                                                                                    |
|----------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| `$query` | ein SQL-Query-String. Die in der Query angegebenen Felder werden in der Liste angezeigt, so kann man also die Spalten beeinflussen.          |
| `$rowsPerPage` | Anzahl Zeilen pro Seite. Standard ist 30. Werden mehr Datensätze angezeigt, wird automatisch eine Blätterfunktion aktiviert.                 |
| `$listName` | Der Wert wird an alle Links als GET Variable `list` angehängt. Wird dieser Parameter nicht angegeben wird ein md5 Wert aus dem Query erzeugt |
| `$debug` | true oder false, Standard ist false. Bei true wird die Debug Ausgabe eingeschaltet, sodass Fehler in der SQL-Query angezeigt werden          |

<a name="einfaches_beispiel"></a>

### Ein einfaches Beispiel

``` php
$list = rex_list::factory('SELECT name,vorname,plz,ort,telefon FROM rex_adressen');
$list->show();
```

Zeigt aus der Tabelle rex_adressen die Felder *name*, *vorname*, *plz*, *ort* und *telefon* an.

> **Hinweis:**

In diesem einfachen Beispiel funktioniert der Pager im Frontend nicht. Damit der Pager im Frontend funktioniert, muss noch folgende Zeile eingefügt werden: `$list->addParam('article_id',REX_ARTICLE_ID);` 

<a name="beschreibung_der_methoden"></a>

### Formatierung und Verhalten der Liste

Die Formatierung und das Verhalten der Liste kann weitestgehend konfiguriert werden. Hier werden nur die wichtigsten Methoden aufgeführt, die für eine Darstellung benötigt werden. Eine komplette Liste findet sich in der API-Dokumentation von REDAXO [https://friendsofredaxo.github.io/phpdoc/classes/rex-list.html](https://friendsofredaxo.github.io/phpdoc/classes/rex-list.html)

<a name="addcolumn"></a>

#### addColumn

`addColumn(string $columnHead, string $columnBody, integer $columnIndex = -1, array $columnLayout = null)` 

Fügt der Tabelle eine weitere Spalte hinzu. `$list->addColumn('edit','Bearbeiten');` fügt der Tabelle an der letzten Stelle eine Spalte hinzu. *edit* steht im Tabellenkopf, in jeder Tabellenzelle steht *Bearbeiten*.

<a name="addlinkattribute"></a>

#### addLinkAttribute

`addLinkAttribute(mixed $columnName, mixed $attrName, mixed $attrValue)` 

Definiert für einen Link in der angegebenen Spalte ein zusätzliches Link-Attribut. `$list->addLinkAttribute( 'name', 'data-id', '###id###' );` gibt im Link zusätzlich *data-id="999"* aus. Pro Spalte kann man mehrere Link-Attribute definieren.

<a name="addparam"></a>

#### addParam

`addParam( mixed $name, mixed $value )` 

Setzt einen klassenweiten Parameter, der für die Generierung von Links verwendet wird. Wird *rex_list* im Frontend eingesetzt, kann dadurch die Zielseite angegeben werden, in der ein Link geöffnet wird. Beispiel: `$list->addParam('article_id',REX_ARTICLE_ID)` - öffnet den Link in der aktuellen Seite.

<a name="addtableattribute"></a>

#### addTableAttribute

`addTableAttribute( mixed $attrName, mixed $attrValue )` 

Mit der Methode *addTableAttribute* können der Tabelle weitere Attribute hinzugefügt werden.
`$list->addTableAttribute('class', 'table-striped');` gibt die Tabelle mit dem Attribut *class="table-striped"* aus

<a name="addtablecolumngroup"></a>

#### addTableColumnGroup

`addTableColumnGroup( array $columns, integer $columnGroupSpan = null )` 

Die Methode kann verwendet werden, um die Spaltenbreiten über das HTML Element *colgroup* zu definieren.
Beispiele:

``` php
$list->addTableColumnGroup([40, '*', 240, 140, 200]);
$list->addTableColumnGroup([ ['width' => 40], ['width' => 240, 'span' => 2], ['width' => 240] ]);
$list->addTableColumnGroup([ ['class' => 'classname-a'], ['class' => 'classname-b'], ['class' => 'classname-c'] ]);
```
<a name="getcolumnlabel"></a>

#### getColumnLabel

`getColumnLabel( string $columnName, mixed $default = null )` 

<a name="setcolumnlabel"></a>

#### setColumnLabel

Mit der Methode *setColumnLabel* bekommen die Tabellenspalten eine aussagekräftige Bezeichnung.
Beispiel: `$list->setColumnLabel('name', 'Name des Teilnehmers');` überschreibt die Tabellenspalte *name* mit *Name des Teilnehmers*

<a name="getheader"></a>

#### getHeader()

`getHeader()` 

Der Header wird standardmäßig bereits im Kopf ausgegeben, wenn `$list->show()` verwendet wird. Mit `echo $list->getHeader();` kann man den Header (Pager sowie Anzahl Datensätze) zusätzlich auch noch nach der Tabelle ausgeben lassen.

<a name="geturl"></a>

#### getUrl

`getUrl(array $params = [], boolean $escape = true)` 

Erstellt eine URL für die aktuelle Seite. Kann verwendet werden, um ein Formular aufzurufen:
`echo '<a href="'.$list->getUrl(['func'=>'add']).'">Hinzufügen</a>';` 

<a name="getparsedurl"></a>

#### getParsedUrl

`getParsedUrl(array $params = [], boolean $escape = true)` 

Erstellt eine URL für die aktuelle Seite. Der URL werden die Standard-rex_list-Variablen (z. B. *sort*, *sorttype*) hinzugefügt. Kann verwendet werden, um ein Formular aufzurufen:
`echo '<a href="'.$list->getParsedUrl(['func'=>'add']).'">Hinzufügen</a>';` 

<a name="removecolumn"></a>

#### removeColumn

`removeColumn(string $columnName)` 

Eine Spalte wird aus der Tabelle entfernt. Dies kann sinnvoll sein, wenn in der SQL-Abfrage Werte stehen, die nicht angezeigt werden sollen (z. B. die id des Datensatzes): `removeColumn('id')` 

<a name="setcaption"></a>

#### setCaption

`setCaption(string $caption)` 

Setzt einen Titel über die Tabelle. Beispiel: `setCaption( 'Teilnehmerliste' )` .
Es wird innerhalb der Tabelle das *<caption>* Tag gesetzt.

<a name="setrowattributes"></a>

#### setRowAttributes

`setRowAttributes(array $attributes)`

`setRowAttributes(callable $customfunction)`

Die Funktion ergänzt die Tabellenzeile im TR-Tag mit Attributen. Die Attribute werden als Array
`['attribut' => wert,...]` übergeben und als `attribut="wert" ...` in den Tag eingebaut. Da der Wert auch
Platzhalter enthalten darf, können Datensatzinhalte eingefügt werden: `['data-id' => '###id###,'class="marker-###privacy###"']`.
Als Alternative zum Array kann eine Callback-Funktion übergeben werden, die ihrerseits die
Attribute als String zurück gibt. Die Callback-Funktion kann komplexere Analysen im Datensatz
durchführen. Beispiel: wenn die Datensatz-ID gleich der ID des zuletzt geänderten Datensatzes ist, wird die
Zeile farblich hervorgehoben. 

<a name="getrowattributes"></a>

#### getRowAttributes

`getRowAttributes()` 

Die Funktion fragt die aktuell eingestellten Zeilen-Attribute ab. Rückgabe ist entweder
- `null`, wenn keine Attribute gesetzt sind
- ein Callable
- ein Attribute-Array

<a name="setcolumnformat"></a>

#### setColumnFormat

`setColumnFormat(string $columnName, string $format_type, mixed $format = '', array $params = [])` 

Setzt das Format einer Tabellenspalte. Um die Spalte *datum* als formatiertes Datum auszugeben, kann man `$list->setColumnFormat('datum', 'date','d.m.Y');` verwenden.
Die Methode erlaubt auch eine Custom-Function. So kann man mit `$list->setColumnFormat('datum', 'custom','myclass::myfunction',['param1'=>'value1']);` eine Funktion aufrufen, die den anzuzeigenden Wert zurückliefert. Die Funktion bekommt als Parameter ein Array mit dem Listenobjekt (*list*), den Feldnamen (*field*), den Wert (*value*), das Format (*format*, in diesem Falle *custom*) und die Parameter (*params*) übergeben.
Als Parameter können auch Platzhalter in der Form *###fieldname###* gesetzt werden. Somit können auch andere Werte aus der Datenbankabfrage an die Funktion übergeben werden. So kann in eine mit *addColumn* hinzugefügte Spalte ein Link eingefügt werden: `$list->setColumnFormat('delete', 'custom', ['myclass','mydeletefunc'],['id' => '###id###']);` Die Funktion *myclass::mydeletefunc* kann dann mittels `return '<a href="'.rex_getUrl(rex_article::getCurrentId(),'',['func'=>'delete']).'&id='.$params['params']['id'].'" onclick="return confirm(\'Wirklich löschen?\')">löschen</a>'` einen Link zum Löschen des Datensatzes in der Tabelle ausgeben. Die Löschfunktion selbst wird allerdings nicht von der *rex_list*-Klasse zur Verfügung gestellt, sondern muss selbst programmiert werden.

<a name="setcolumnparams"></a>

#### setColumnParams

`setColumnParams(string $columnName, array $params = [])` 

Verlinkt eine Spalte mit den übergebenen Parametern. `$list->setColumnParams('name', ['func' => 'edit', 'id' => '###id###', 'start' => rex_request('start','int',0) ]);` Dadurch erhält jeder Wert in der Spalte `name` einen Link mit dem Parametern `?func=edit&id=999&start=990`. Die Verarbeitung muss durch die Applikation durchgeführt werden.

<a name="setcolumnsortable"></a>

#### setColumnSortable

`setColumnSortable(string $columnName, string $direction = 'asc')` 

`$list->setColumnSortable('name');` definiert die Spalte als sortierbar. Durch Anklicken im Tabellenkopf wird die Tabelle dann automatisch sortiert nach dieser Spalte ausgegeben.

<a name="setcolumnposition"></a>

#### setColumnPosition
  
`$newPosition = setColumnPosition(string $columnName, string|int $columnIndex)`

Verschiebt die über `$columnName` angegebene Spalte an eine neue Position `$columnIndex` in der Tabelle. Die Zielposition wird entweder als numerischer Index oder
ebenfalls über den Spaltennamen festgelegt. Die interne Liste der Spaltennamen beinhaltet auch ausgeblendete Spalten (siehe [removeColumn](#removecolumn)); daher sollte der Spaltenname statt des numerischen Index benutzt werden. `$newPosition = setColumnPosition('spalte', 'zielspalte');`
Die Zielposition ist <em>vor</em> der angegebenen Zielspalte, die ihrerseits nach rechts verschoben wird. So können Spalten vor die erste Spalte verschoben werden.
Mit dem Zielindex `-1` wird die Spalte an das Ende der Tabelle verschoben. `$newPosition = setColumnPosition('spalte', -1);`
Der zu einem Spaltennamen gehörende Index kann mit `$position = getColumnPosition($columnName);` abgefragt werden. Ungültige Namen lösen eine Exception aus.

<a name="setnorowsmessage"></a>

#### setNoRowsMessage

`setNoRowsMessage(mixed $msg)` 

Damit wird ein Text definiert, der angezeigt wird, falls keine Datensätze gefunden werden. Als Standard wird der über *rex_i18n* übersetzte String aus *list_no_rows* verwendet.

<a name="ausgabe_der_liste"></a>

### Ausgabe der Liste

Durch die *get*-Methode wird die Liste final ausgegeben.

``` php
echo $list->get();
```

Alternativ kann auch `$list->show();` verwendet werden.

<a name="extension_point"></a>

### Extension Point

Die *rex_list*-Klasse bringt einen Extension-Point mit: `REX_LIST_GET` . Der Extension-Point wird vor der Listenausgabe aufgerufen.

<a name="zusammenspiel_mit_rex_form"></a>

## Zusammenspiel mit rex_form

Die *rex_list*-Klasse kann sehr gut mit der [*rex_form*-Klasse](/{{path}}/{{version}}/formulare) zusammen eingesetzt werden, um einen Datensatz zu editieren.

* Mit dem Parameter-Key *func* kann kann man entsprechend eine `rex_form` Instanz ansteuern.
* Mit dem Parameter-Key *[Instanzname]_start* lässt sich die Position der Paginierungs-Seite übergeben, wodurch ein Zurückkehren auf diese Position in der *rex_form*-Instanz ermöglicht wird.
* Durch *###id###* wird die entsprechende ID des jeweiligen Datensatzes als Value des Parameters-Keys *id* dem Link als Get-Parameter geliefert. Nach diesem Muster können auch andere Werte eines Datensatzes an die Link-Parameter übergeben werden.

<a name="ausgabe_im_fragment"></a>

## Ausgabe einer rex_list in einem Fragment

Im AddOn-Kontext bietet es sich an, für die Anzeige der Liste im REDAXO-Backend das Content-Fragment zu nutzen.

``` php
$fragment = new rex_fragment();
$fragment->setVar('title', 'Locations');
$fragment->setVar('content', $list->get(), false);
echo $fragment->parse('core/page/section.php');
```

<a name="ausgabe_multiple"></a>

## Ausgabe mehrerer rex_list-Instanzen mit Paginierung

Bei der Ausgabe mehrerer rex_list-Instanzen auf einer AddOn-Seite gilt zu beachten, dass das Offset beider Listen in der jeweils anderen als Parameter mitgegeben werden muss. Andernfalls wird, wenn man die Paginierung einer Liste verwendet, die Paginierung aller anderen Listen zurückgesetzt.

``` php
// 1. rex_list
$list = rex_list::factory('SELECT * FROM ...', 10, 'liste1');
$list->addParam('liste2_start', rex_request('liste2_start', 'int'));
echo $list->get();

// 2. rex_list
$list = rex_list::factory('SELECT * FROM ...', 10, 'liste2');
$list->addParam('liste1_start', rex_request('liste1_start', 'int'));
echo $list->get();

```

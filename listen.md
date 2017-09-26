# Listen
    
- [Tabellen `rex_list`](#rex-list)
- [Listenansicht von Datenbank-Tabellen](#listenansicht)
	- [Aufruf von rex_list und Parameter](#aufruf_von_rex_list)
	- [Ein einfaches Beispiel](#einfaches_beispiel)
	- [Beschreibung der Methoden zur Formatierung und zum Verhalten der Liste](#beschreibung_der_methoden)
	- [Ausgabe der Liste](#ausgabe_der_liste)
	- [Extension Point](#extension_point)
- [Ausgabe einer rex_list in einem Fragment](#ausgabe_im_fragment)
	

<a name="rex-list"></a>
## Tabellen `rex_list`


<a name="listenansicht"></a>
## Listenansicht von Datenbank-Tabellen

Die Klasse `rex_list` ist eines der heimlichen Heinzelmännchen von REDAXO. Mit `rex_list` können Datenbankabfragen als tabellarische Listen dargestellt werden. Die Verwendung von `rex_list` kann sowohl im Backend als auch im Frontend sinnvoll sein. Eine Listenansicht kann über die `rex_list` Klassen mit verschiedenen Funktionen ausgestattet werden, z.B. mit einer Sortierfunktion für bestimmte Spalten oder mit Links, um Datensätze zu editieren, zu löschen oder mit eigenen Funktionen zu manipulieren.
Die Klasse verfügt von Haus aus über eine Paging Funktion über die Klasse `rex_pager`.

<a name="aufruf_von_rex_list"></a>
### Aufruf von rex_list und Parameter

Ein Listenobjekt erzeugen:

```
$list = rex_list::factory($query, $rowsPerPage, $listName, $debug);
```

Parameter | Erklärung
------------- | ------------- 
`$query`  | ein SQL Query String. Die in der Query angegebenen Felder werden in der Liste angezeigt.
`$rowsPerPage`  | Anzahl Zeilen pro Seite. Standard ist 30. Werden mehr Datensätze angezeigt, wird automatisch eine Blätterfunktion aktiviert
`$listName`  | Der Wert wird an alle Links als GET Variable `list` angehängt. Wird dieser Parameter nicht angegeben wird ein md5 Wert aus dem Query erzeugt
`$debug`  | true oder false, Standard ist false. Bei true wird die Debug Ausgabe eingeschaltet, sodass Fehler in der SQL Query angezeigt werden 


<a name="einfaches_beispiel"></a>
### Ein einfaches Beispiel

```
$list = rex_list::factory('SELECT name,vorname,plz,ort,telefon FROM rex_adressen');
$list->show();
```

Zeigt aus der Tabelle rex_adressen die Felder name, vorname, plz, ort und telefon an.

> **Hinweis:** In diesem einfachen Beispiel funktioniert der Pager im Frontend nicht. Damit der Pager im Frontend funktioniert, muss noch folgende Zeile eingefügt werden: `$list->addParam('article_id',REX_ARTICLE_ID);`

<a name="beschreibung_der_methoden"></a>
### Beschreibung der Methoden zur Formatierung und zum Verhalten der Liste

Die Formatierung und das Verhalten der Liste kann weitestgehend konfiguriert werden. Hier werden die wichtigsten Methoden aufgeführt, die für eine Darstellung benötigt werden. Eine komplette Liste findet sich in der api Dokumentation von REDAXO https://redaxo.org/api/master/class-rex_list.html

#### `addColumn( string $columnHead, string $columnBody, integer $columnIndex = -1, array $columnLayout = null )`

Fügt der Tabelle eine weitere Spalte hinzu. `$list->addColumn('edit','Bearbeiten');` fügt der Tabelle an der letzten Stelle eine Spalte hinzu. `edit` steht im Tabellenkopf, in jeder Tabellenzelle steht `Bearbeiten`.

#### `addLinkAttribute( mixed $columnName, mixed $attrName, mixed $attrValue )`

Definiert für einen Link in der angegebenen Spalte ein zusätzliches Link-Attribut. `$list->addLinkAttribute( 'name', 'data-id', '###id###' );` gibt im Link zusätzlich `data-id="999"` aus. Pro Spalte können mehrere Link Attribute definiert werden.

#### `addParam( mixed $name, mixed $value )`

Setzt einen klassenweiten Parameter, der für die Generierung von Links verwendet wird. Wird `rex_list` im Frontend eingesetzt, kann hier die Zielseite angegeben werden, in der ein Link geöffnet wird. Beispiel: `$list->addParam('article_id',REX_ARTICLE_ID)` - öffnet den Link in der aktuellen Seite.

#### `addTableAttribute( mixed $attrName, mixed $attrValue )`

Mit der Methode `addTableAttribute` können der Tabelle weitere Attribute hinzugefügt werden.
Mit `$list->addTableAttribute('class', 'table-striped');` wird die Tabelle mit dem Attribut class="table-striped" ausgegeben

#### `addTableColumnGroup( array $columns, integer $columnGroupSpan = null )`

Die Methode kann verwendet werden, um die Spaltenbreiten über das HTML Element `colgroup` zu definieren.
Beispiele:
```
$list->addTableColumnGroup([40, '*', 240, 140, 200]);
$list->addTableColumnGroup([ ['width' => 40], ['width' => 240, 'span' => 2], ['width' => 240] ]);
$list->addTableColumnGroup([ ['class' => 'classname-a'], ['class' => 'classname-b'], ['class' => 'classname-c'] ]);
```

#### `getColumnLabel( string $columnName, mixed $default = null )`

Mit der Methode `setColumnLabel` bekommen die Tabellenspalten eine aussagekräftige Bezeichnung.
Mit `$list->setColumnLabel('name', 'Name des Teilnehmers');` wird die Tabellenspalte name mit "Name des Teilnehmers" überschrieben

#### `getHeader()`

Der Header wird standardmäßig bereits im Kopf ausgegeben, wenn `$list->show()` verwendet wird. Mit `echo $list->getHeader();` kann man den Header (Pager sowie Anzahl Datensätze) zusätzlich auch noch nach der Tabelle ausgeben lassen.

#### `removeColumn( string $columnName )`

Eine Spalte wird aus der Tabelle entfernt. Dies kann sinnvoll sein, wenn in der SQL-Abfrage Werte stehen, die nicht angezeigt werden sollen (z.B. die id des Datensatzes) `removeColumn( 'id' )`

#### `setCaption( string $caption )`

Setzt einen Titel über die Tabelle. Beispiel: `setCaption( 'Teilnehmerliste' )`. Es wird innerhalb der Tabelle das `<caption>` Tag gesetzt.

#### `setColumnFormat( string $columnName, string $format_type, mixed $format = '', array $params = [] )`

Setzt das Format einer Tabellenspalte. Um die Spalte datum als formatiertes Datum auszugeben, kann man `$list->setColumnFormat('datum', 'date','d.m.Y');` verwenden.
Die Methode erlaubt auch eine Custom Function. So kann man mit `$list->setColumnFormat('datum', 'custom','myclass::myfunction',['param1'=>'value1']);` eine Funktion aufrufen, die den anzuzeigenden Wert zurück liefert. Die Funktion bekommt als Parameter ein Array mit dem Listenobjekt (list), den Feldnamen (field), den Wert (value), das Format (format, in diesem Falle `custom`) und die Parameter (params) übergeben.
Als Parameter können auch Platzhalter in der Form `###fieldname###` gesetzt werden. Somit können auch andere Werte aus der Datenbankabfrage an die Funktion übergeben werden. So kann in eine mit `addColumn` hinzugefügte Spalte ein Link eingefügt werden: `$list->setColumnFormat('delete', 'custom', ['myclass','mydeletefunc'],['id' => '###id###']);` Die Funktion myclass::mydeletefunc kann dann mittels `return '<a href="'.rex_getUrl(rex_article::getCurrentId(),'',['func'=>'delete']).'&id='.$params['params']['id'].'" onclick="return confirm(\'Wirklich löschen?\')">löschen</a>'` einen Link zum Löschen des Datensatzes in der Tabelle ausgeben. Die Löschfunktion selbst wird nicht von der rex_list Klasse zur Verfügung gestellt, sondern muss selbst programmiert werden.

#### `setColumnParams( string $columnName, array $params = [] )`

Verlinkt eine Spalte mit den übergebenen Parametern. `$list->setColumnParams('name', ['func' => 'edit', 'id' => '###id###', 'start' => rex_request('start','int',0) ]);` Erzeugt in der Spalte `name` bei jedem Wert einen Link mit dem Parametern ...?func=edit&id=999&start=990. Die Verarbeitung muss durch die Applikation durchgeführt werden.

#### `setColumnSortable( string $columnName, string $direction = 'asc' )`

`$list->setColumnSortable('name');` definiert die Spalte als sortierbar. Sie kann im Tabellenkopf angeklickt werden und wird dann automatisch sortiert nach dieser Spalte ausgegeben.

#### `setNoRowsMessage( mixed $msg )`

Damit kann ein Text definiert werden, der angezeigt wird, wenn keine Datensätze gefunden werden. Als Standard wird der über rex_i18n übersetzte String aus `list_no_rows` verwendet.


<a name="ausgabe_der_liste"></a>
### Ausgabe der Liste

Durch die `get` Methode wird die Liste final ausgegeben.

```
echo $list->get();
```

Alternativ kann auch `$list->show();` verwendet werden.


<a name="extension_point"></a>
### Extension Point

Die `rex_list` Klasse bringt einen Extensionpoint mit: `REX_LIST_GET`. Der Extensionpoint wird vor der Listenausgabe aufgerufen.


<a name="zusammenspiel_mit_rex_form"></a>
## Zusammenspiel mit rex_form

Die `rex_list` Klasse kann sehr gut mit der `rex_form` Klasse zusammen eingesetzt werden, um einen Datensatz zu editieren.

* Der Parameter-Key `func` kann genutzt werden, um entsprechend eine `rex_form` Instanz ansteuern zu können. 
* Mit der Parameter-Key `start` übergeben wir die Position der Paginierungs-Seite, wodurch ein zurückkehren auf von der `rex_form` Instanz auf diese Position ermöglicht wird.
* Durch `###id###` wird als Value des Parameters-Keys `id` des Get-Parameters dem Link die entsprechende ID es jeweiligen Datensatzes geliefert. Nach diesem Muster können auch andere Werte eines Datensatzes an die Link-Parameter übergeben werden.


<a name="ausgabe_im_fragment"></a>
## Ausgabe einer rex_list in einem Fragment

Im Addon-Kontext bietet es sich an für die Anzeige der Liste im Redaxo-Backend das Content-Fragment zu nutzen.

```
$fragment = new rex_fragment();
$fragment->setVar('title', 'Locations');
$fragment->setVar('content', $list->get(), false);
echo $fragment->parse('core/page/section.php');

```

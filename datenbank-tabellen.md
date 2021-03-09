# Datenbank - Tabellen

- [rex_sql_table](#table)
  - [Abruf der Struktur](#abruf-der-struktur)
    - [get](#get)
    - [exists](#exists)
    - [getName](#getname)
    - [hasColumn](#hascolumn)
    - [getColumn](#getcolumn)
    - [getColumns](#getcolumns)
    - [getPrimaryKey](#getprimarykey)
    - [hasIndex](#hasindex)
    - [getIndex](#getindex)
    - [getIndexes](#getindexes)
    - [hasForeignKey](#hasforeignkey)
    - [getForeignKey](#getforeignkey)
    - [getForeignKeys](#getforeignkeys)
  - [Änderungen ausführen](#aenderungen-ausfuehren)
    - [create](#create)
    - [alter](#alter)
    - [ensure](#ensure)
    - [drop](#drop)
  - [Änderungen definieren](#aenderungen-definieren)
    - [setName](#setname)
    - [addColumn](#addcolumn)
    - [ensureColumn](#ensurecolumn)
    - [ensurePrimaryIdColumn](#ensureprimaryidcolumn)
    - [ensureGlobalColumns](#ensureglobalcolumns)
    - [renameColumn](#renamecolumn)
    - [removeColumn](#removecolumn)
    - [addIndex](#addindex)
    - [ensureIndex](#ensureindex)
    - [renameIndex](#renameindex)
    - [removeIndex](#removeindex)
    - [addForeignKey](#addforeignkey)
    - [ensureForeignKey](#ensureforeignkey)
    - [renameForeignKey](#renameforeignkey)
    - [removeForeignKey](#removeforeignkey)
- [rex_sql_column](#column)
- [rex_sql_index](#index)
- [rex_sql_foreign_key](#foreign-key)
- [rex_sql_util](#util)

<a name="table"></a>

## rex_sql_table

Mit der Klasse `rex_sql_table` kann man die Struktur der Datenbanktabellen auslesen und verändern.

Die Klasse ist vor allem nützlich bei der Entwicklung von AddOns, um bei der Installation die nötigen Tabellen des AddOns anzulegen, bzw. sie bei der Deinstallation wieder zu löschen.

Beispiel für eine `install.php`:

```php
rex_sql_table::get(rex::getTable('foo'))
    ->ensurePrimaryIdColumn()
    ->ensureColumn(new rex_sql_column('title', 'varchar(255)'))
    ->ensureColumn(new rex_sql_column('description', 'text', true))
    ->ensureColumn(new rex_sql_column('status', 'tinyint(1)', false, 1))
    ->ensureIndex(new rex_sql_index('i_title', ['title']))
    ->ensure();
```

Durch diesen Code wird die Tabelle in der angegebenen Struktur sichergestellt. Sie wird also erstellt, falls noch nicht vorhanden, bzw. modifiziert, falls einzelne Spalten oder Indizes nicht der gewünschten Struktur entsprechen.

> **Tipp:**
Über das Adminer-AddOn kann man sich den `rex_sql_table`-Code für eine Tabelle generieren lassen. Alternativ ist dies auch möglich über den Konsolenbefehl `redaxo/bin/console db:dump-schema <table>`.

Beispiel für eine `uninstall.php`:

```php
rex_sql_table::get(rex::getTable('foo'))->drop();
```

<a name="abruf-der-struktur"></a>

### Abruf der Struktur

<a name="get"></a>

#### get

`get($name,$db)`

Mit `rex_sql_table::get($name)` holt man sich das Objekt zu der Tabelle mit dem Namen `$name` und *optional* der Datebank $db (numerisch muss in der config.yml von REDAXO hinterlegt sein). Diese Methode wird verwendet unabhängig davon, ob man eine existieren Tabelle abrufen, bzw. editieren möchte, oder ob man eine neue Tabelle erstellen möchte.

<a name="exists"></a>

#### exists

`exists()`

Prüft, ob die Tabelle existiert (`$table->exists()`).

<a name="getname"></a>

#### getName

`getName()`

Gibt den Tabellennamen zurück.

<a name="hascolumn"></a>

#### hasColumn

`hasColumn($name)`

Prüft, ob die angegebene Spalte existiert.

<a name="getcolumn"></a>

#### getColumn

`getColumn($name)`

Liefert das `rex_sql_column`-Objekt zu der angegebenen Spalte, oder `null` falls die Spalte nicht existiert.

<a name="getcolumns"></a>

#### getColumns

`getColumns()`

Liefert ein Array mit allen Spalten der Tabelle als `rex_sql_column`-Objekte.

<a name="getprimarykey"></a>

#### getPrimaryKey

`getPrimaryKey()`

Liefert den Primärschlüssel der Tabelle als Array mit den Spaltennamen, zum Beispiel `['id']`.

<a name="hasindex"></a>

#### hasIndex

`hasIndex($name)`

Prüft, ob der angegebene Index existiert.

<a name="getindex"></a>

#### getIndex

`getIndex($name)`

Liefert das `rex_sql_index`-Objekt zu dem angegebenen Index, oder `null` falls der Index nicht existiert.

<a name="getindexes"></a>

#### getIndexes

`getIndexes()`

Liefert ein Array mit allen Indizes der Tabelle als `rex_sql_index`-Objekte.

<a name="hasforeignkey"></a>

#### hasForeignKey

`hasForeignKey($name)`

Prüft, ob der angegebene Fremdschlüssel existiert.

<a name="getforeignkey"></a>

#### getForeignKey

`getForeignKey($name)`

Liefert das `rex_sql_foreign_key`-Objekt zu dem angegebenen Fremdschlüssel, oder `null` falls der Fremdschlüssel nicht existiert.

<a name="getforeignkeys"></a>

#### getForeignKeys

`getForeignKeys()`

Liefert ein Array mit allen Fremdschlüsseln der Tabelle als `rex_sql_foreign_key`-Objekte.

<a name="aenderungen-ausfuehren"></a>

### Änderungen ausführen

<a name="create"></a>

#### create

`create()`

Erstellt die Tabelle mit der zuvor angegebenen Definition. Falls die Tabelle bereits existiert, wird eine Exception geworfen.

<a name="alter"></a>

#### alter

`alter()`

Ändert die Tabelle entsprechend der zuvor angegebenen Änderungen. Falls die Tabelle noch nicht existiert, wird eine Exception geworfen.

<a name="ensure"></a>

#### ensure

`ensure()`

Stellt die zuvor angegebene Definition sicher. Falls die Tabelle noch nicht existiert, wird sie angelegt. Ansonsten wird sie bei Bedarf entsprechend der Definition geändert. Dabei wird auch sichergestellt, dass die Spalten in der definierten Reihenfolge (Reihenfolge der `ensureColumn()`-Aufrufe, oder über explizite Positionsangaben) vorliegen. Daher sollte diese Methode nur verwendet werden, wenn die komplette Tabellen-Definition angegeben wurde, die sicherzustellen ist. Bei Angabe von nur einzelnen Änderungen sollte stattdessen `alter()` verwendet werden.

<a name="drop"></a>

#### drop

`drop()`

Löscht die Tabelle. Falls sie gar nicht existiert, macht die Methode nichts, es wird also keine Exception geworfen.

<a name="aenderungen-definieren"></a>

### Änderungen definieren

Die folgenden Methoden führen die jeweiligen Änderungen nicht sofort aus, sondern dafür bedarf es immer den Aufruf einer der Methoden `create()`, `alter()` oder `ensure()`.

<a name="setname"></a>

#### setName

`setName($name)`

Ändert den Tabellennamen.

<a name="addcolumn"></a>

#### addColumn

`addColumn(rex_sql_column $column, $afterColumn = null)`

Fügt eine neue Spalte hinzu. Falls eine Spalte mit dem Namen bereits existiert, wird eine Exception geworfen.
Optional kann die Position für die neue Spalte mit dem zweiten Parameter gesetzt werden, entweder durch Angabe eines anderen Spaltennamens, nach der die Spalte eingefügt werden soll, oder `rex_sql_table::FIRST`.

<a name="ensurecolumn"></a>

#### ensureColumn

`ensureColumn(rex_sql_column $column, $afterColumn = null)`

Stellt sicher, dass die Spalte mit der angegebenen Definition existiert. Die Spalte wird also ggf. angelegt oder geändert.
Optional kann die Position für die neue Spalte mit dem zweiten Parameter gesetzt werden, entweder durch Angabe eines anderen Spaltennamens, nach der die Spalte eingefügt werden soll, oder `rex_sql_table::FIRST`.

<a name="ensureprimaryidcolumn"></a>

#### ensurePrimaryIdColumn

`ensurePrimaryIdColumn()`

Dies ist eine Shortcut-Methode für diesen Aufruf:

```php
$table
    ->ensureColumn(new rex_sql_column('id', 'int(10) unsigned', false, null, 'auto_increment'))
    ->setPrimaryKey('id');
```

<a name="ensureglobalcolumns"></a>

#### ensureGlobalColumns

`ensureGlobalColumns()`

Dies ist eine Shortcut-Methode für diesen Aufruf:

```php
$table
    ->ensureColumn(new rex_sql_column('createdate', 'datetime'))
    ->ensureColumn(new rex_sql_column('createuser', 'varchar(255)'))
    ->ensureColumn(new rex_sql_column('updatedate', 'datetime'))
    ->ensureColumn(new rex_sql_column('updateuser', 'varchar(255)'));
```

<a name="renamecolumn"></a>

#### renameColumn

`renameColumn($oldName, $newName)`

Benennt eine Spalte um.

<a name="removecolumn"></a>

#### removeColumn

`removeColumn($name)`

Entfernt eine Spalte.

<a name="setprimarykey"></a>

#### setPrimaryKey

`setPrimaryKey($columns)`

Setzt den Primärschlüssel. Falls dieser nur für eine Spalte gesetzt werden soll, kann diese als String angegeben werden (`$table->setPrimaryKey('id')`), ansonsten als Array (`$table->setPrimaryKey(['namespace', 'key'])`).

<a name="hasindex"></a>

#### addIndex

`addIndex(rex_sql_index $index)`

Fügt einen neuen Index hinzu. Falls ein Index mit dem Namen bereits existiert, wird eine Exception geworfen.

<a name="ensureindex"></a>

#### ensureIndex

`ensureIndex(rex_sql_index $index)`

Stellt sicher, dass der Index mit der angegebenen Definition existiert. Der Index wird also ggf. angelegt, oder geändert.

<a name="renameindex"></a>

#### renameIndex

`renameIndex($oldName, $newName)`

Benennt einen Index um.

<a name="removeindex"></a>

#### removeIndex

`removeIndex($name)`

Entfernt einen Index.

<a name="addforeignkey"></a>

#### addForeignKey

`addForeignKey(rex_sql_foreign_key $foreignKey)`

Fügt einen neuen Fremdschlüssel hinzu. Falls ein Fremdschlüssel mit dem Namen bereits existiert, wird eine Exception geworfen.

<a name="ensureforeignkey"></a>

#### ensureForeignKey

`ensureForeignKey(rex_sql_foreign_key $foreignKey)`

Stellt sicher, dass der Fremdschlüssel mit der angegebenen Definition existiert. Der Fremdschlüssel wird also ggf. angelegt oder geändert.

<a name="renameforeignkey"></a>

#### renameForeignKey

`renameForeignKey($oldName, $newName)`

Benennt einen Fremdschlüssel um.

<a name="removeforeignkey"></a>

#### removeForeignKey

`removeForeignKey($name)`

Entfernt einen Fremdschlüssel.

<a name="column"></a>

## rex_sql_column

`new rex_sql_column($name, $type, $nullable = false, $default = null, $extra = null)`

Parameter | Erklärung
------------- | -------------
`$name`  | Name der Spalte
`$type`  | Typ der Spalte als String, zum Beispiel `varchar(255)`, `int(10) unsigned`, `datetime`...
`$nullable`  | Definiert, ob die Spalte auch den Wert `null` erlaubt (`true`/`false`)
`$default`  | Default-Wert der Spalte
`$extra`  | Zusätzeliche Spaltendefinitionen, wie zum Beispiel `'auto_increment'`.

Über die Methoden `getName()`, `getType()`, `isNullable()`, `getDefault()` und `getExtra()` können die Werte abgefragt werden.

<a name="index"></a>

## rex_sql_index

`new rex_sql_index($name, array $columns, $type = self::INDEX)`

Parameter | Erklärung
------------- | -------------
`$name`  | Name des Indexes
`$columns`  | Array mit den Spaltennamen, auf die sich der Index beziehen soll (z. B. `['id', 'clang_id']`)
`$type`  | Index-Typ: ``rex_sql_index`::INDEX` (default), `rex_sql_index::UNIQUE` oder `rex_sql_index::FULLTEXT`

Über die Methoden `getName()`, `getColumns()` und `getType()` können die Werte abgefragt werden.

<a name="foreign-key"></a>

## rex_sql_foreign_key

`new rex_sql_foreign_key($name, $table, array $columns, $onUpdate = self::RESTRICT, $onDelete = self::RESTRICT)`

Parameter | Erklärung
------------- | -------------
`$name` | Name des Fremdschlüssels
`$table` | Name der Tabelle, die über den Fremdschlüssel referenziert wird
`$columns` | Assoziatives Array, welches die Spalten des Fremdschlüssels den Spalten in der referenzierten Tabelle zuordnet (z. B. `['foo_id' => 'id']`)
`$onUpdate` | `ON UPDATE`-Aktion: `rex_sql_foreign_key::RESTRICT` (default), `rex_sql_foreign_key::CASCADE` oder `rex_sql_foreign_key::SET_NULL`
`$onDelete` | `ON DELETE`-Aktion: `rex_sql_foreign_key::RESTRICT` (default), `rex_sql_foreign_key::CASCADE` oder `rex_sql_foreign_key::SET_NULL`

Über die Methoden `getName()`, `getTable()`, `getColumns()`, `getOnUpdate()` und `getOnDelete()` können die Werte abgefragt werden.

<a name="util"></a>

## rex_sql_util

### Kopieren von Tabellenstrukturen mit/oder ohne Daten

> Beim Kopieren von REDAXO-Tabellen wird nicht automatisch der Prefix gesetzt. 

```php
// Nur Tabellenstruktur kopieren von rex_table1 zu neuer Tabelle rex_table2
rex_sql_util::copyTable('rex_table1', 'rex_table2');
```
```php
// Tabellenstruktur und Daten kopieren
rex_sql_util::copyTableWithData('rex_table1', 'rex_table2');
```

### Beispiel
```php
 rex_sql_util::copyTableWithData(rex::getTablePrefix() . 'old_data',rex::getTablePrefix() . 'new_data');
```

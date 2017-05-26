# Listen
    
- [Auswahllisten `rex_select`](#rex-select)
- [Tabellen `rex_list`](#rex-list)


<a name="rex-select"></a>
## Auswahllisten `rex_select `


<a name="rex-list"></a>
## Tabellen `rex_list`


## Listenansicht von Datenbank-Tabellen

Die `rex_list` Klasse ist "Part 1" der Redaxo eigenen Datenbankverwaltung für Addons, kann aber auch darüberhinaus eingesetzt werden. `rex_list` ermöglicht das Anzeigen von Datensätzen einer Datenbanktabelle in tabellarischer Listen-Ansicht. 
Die Darstellung der `rex_list` Liste kann durch diverse Optionen modifiziert werden. `rex_list` nutzt zur Paginierung die `rex_pager` Klasse, durch welche das Handling von vielen Datensätzen erheblich erleichtert wird.


* TODO GENERELL Übergabe Parameter auflisten für alle besprochenen Methoden!


### Instanzierung

* TODO listName Parameter
* TODO debug Modus


Die `rex_list` Klasse wurde als Singelton design und nutzt die `rex_factory_trait` zur wiederkehrenden Instanzierung des `rex_list` Objekts. Für die entsprechende Instanzierung des Objekts ist die statische Methode `factory` implementiert. 

```
$list = rex_list::factory($query, $rowsPerPage, $listName, $debug);
```

Durch den Übergabe-Parameter `$query` wird der `factory` Methode ein SQL-Select-Statement übergeben, dieses ist zwingend notwendig und sorgt dafür, dass die `rex_list` Klasse die entsprechenden Datensätze aus der im SELECT definierten Datenbanktabelle zur Anzeige in der Tabellen-Ansicht verwenden kann. 

Alle durch das SELECT selektierten Zeilen der Datenbanktabelle werden per default ohne Ausnahme in die Listen-Tabelle geschrieben. Per default ist die Paginierung auf 30 Datensätze gestellt. Zu berücksichtigen hierbei ist, dass die Records der Paginierungsviews durch ein automatisch generiertes LIMIT, dass dem SQL-Select-Statement angehangen wird, erzeugt werden.

Im folgenden Beispiel sollen alle Datensätze aus der Tabelle `locations` durch die Listen-Ansicht der `rex_list` Klasse zugänglich gemacht werden.

```
$list = rex_list::factory('SELECT * FROM rex_locations ORDER BY id');
```


### Tabellen Parameter

TODO `addParam`


### Tabellen Attribute

TODO `addTableAttribute`


### Tabellen Titel

TODO `setCaption`


### Ausschluss

Zum Ausschließen einzelner Spalten dient die Methode `removeColumn` durch welche im folgenden Beispiel einige Stammdaten der Location ausgeblendet werden.

```
$list->removeColumn('id');
$list->removeColumn('phone');
$list->removeColumn('street');
$list->removeColumn('house_number');
$list->removeColumn('county');
$list->removeColumn('zip_code');
$list->removeColumn('lat');
$list->removeColumn('lon');
```

### Selektierung

Es bietet sich natürlich alternativ an ausschließlich die Spalten im Select-Statement zu definieren, welche man nutzen möchte. 

```
$list = rex_list::factory('SELECT id, location_name, city, country FROM rex_locations ORDER BY id');
```

### Sortierung

Die rex_list Klasse ermöglicht es durch die `setColumnSortable` Methode eine bestimmte Datenbankspalte auf- und absteigend sortierbar zu machen.

```
$list->setColumnSortable('country');
$list->setColumnSortable('city');
```

### Spaltenlabel

Per default werden die Row-Namen der Datenbankspalten als Label der Tabellenspalten angezeigt. Alternativ ist es durch die `setColumnLabel` Methode möglich ein spezifischen Label für eine Tabellenspalte zu definieren. 

```
$list->setColumnLabel('location_name', 'Niederlassung');
```

### Linkparameter

Mithilfe der `setColumnParams` Methode kann der Value einer jeweiligen Tabellenspalte als Link mit entsprechend deklarierten Parametern formatiert werden.

```
$list->setColumnParams('location_name', ['func' => 'edit', 'id' => '###id###', 'start' => rex_request::request('start', 'int', NULL)]);
```

Im obigen Beispiel werden also die Values der Tabellenzeile 'location_name' als Link formatiert. Die Links sind mit den nötigen Parametern versehen, welche von einem rex_form-Formular benötigt würden um den entsprechenden Datensatz editier zu können.

* Der Parameter-Key `func` kann genutzt werden um entsprechend eine `rex_form` Instanz ansteuern zu können. 
* Mit der Parameter-Key `start` übergeben wir die Position der Paginierungs-Seite, wodurch ein zurückkehren auf von der `rex_form` Instanz auf diese Position ermöglicht wird.
* Durch `###id###` wird als Value des Parameters-Keys `id` des Get-Parameters dem Link die entsprechende inkrementelle ID es jeweiligen Datensatzes geliefert. Nach diesem Muster können auch andere Werte eines Datensatzes an die Link-Parameter übergeben werden.


### Linkattribute

TODO `addLinkAttribute`


### Format

Es kommt durchaus vor, dass man auf die Erscheinung der Werte in den Tabellenspalten einfluss nehmen möchte. Zudem ergibt es sich auch, dass man die breite der jeweiligen Spalten der Tabelle explizit definieren möchte, beides ermöglicht die `rex_list` Klasse.


#### Format von Werten

Mit der Methode `setColumnFormat` besteht die Möglichkeit einfluss auf die Anzeige der Werte in der jeweiligen Spalte nehmen zu können. 


### Spalten Gruppierungen

TODO `addTableColumnGroup`


### Zusätzliche Spalten

Die Methode `addColumn` ermöglicht das hinzufügen zusätzlicher Spalten deren Inhalt den Parametern der Methode übergeben werden kann. Wie bereits den Linkparametern durch die Verwendung des Schemas `###value###` im obigen Beispiel die inkrementelle ID des Datensatze geliefert werden konnte so ist es hier auch möglich auf die selektierten Spalten eines Datensatzes zur Anzeige zurück greifen zu können.


### Keine Einträge vorhanden

TODO `setNoRowsMessage`



### View


Durch die `get` Methode wird die Liste final ausgegeben.

```
echo $list->get();
```

Im Addon-Kontext bietet es sich an für die Anzeige der Liste im Redaxo-Backend das Content-Fragment zu nutzen.

```
$fragment = new rex_fragment();
$fragment->setVar('title', 'Locations');
$fragment->setVar('content', $list->get(), false);
echo $fragment->parse('core/page/section.php');

```

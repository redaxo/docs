# Formulare

- [Formulare `rex_form`](#rex-form)
- [Formularansicht von Datensätzen](#formularansicht)
	- [Aufruf von rex_form und Parameter](#aufruf_von_rex_form)
	- [Ein einfaches Beispiel](#einfaches_beispiel)
	- [Beschreibung der Methoden zur Formatierung und zum Verhalten des Formulars](#beschreibung_der_methoden)
	- [Beispiel mit im Zusammenspiel mit `rex_list`](#beispiel_mit_rex_list)
	- [Eingabefelder validieren](#eingabefelder-validieren)

<a name="rex-form"></a>
## Formular `rex_form`

<a name="formularansicht"></a>
## Formularansicht von Datensätzen

Die Klasse `rex_form` bietet die Möglichkeit Eingabeformulare in AddOn-Seiten zu erstellen. Die Verwendung im Frontend ist auch möglich, wird aber nicht empfohlen. `rex_form` bietet sich an gemeinsam mit `rex_list` zu verwenden.

<a name="aufruf_von_rex_form"></a>
### Aufruf von rex_form und Parameter

Die Erstellung eines `rex_form`-Objektes geschieht über die Factory Methode:

```
$form = rex_form::factory( string $tableName, string $fieldset, string $whereCondition, string $method = 'post', boolean $debug = false )
```

Parameter | Erklärung
------------- | ------------- 
`$tableName`  | der Name einer SQL Tabelle in der REDAXO Datenbank. Die Tabelle muss bereits angelegt sein.
`$fieldset`  | Name des Fieldsets. Wird als `<fieldset>...</fieldset>` im Formular ausgegeben.
`$whereCondition`  | eine WHERE Kondition, die zu einem eindeutigen Datensatz führt.
`$method`  | GET oder POST, Standard ist POST.
`$debug`  | true oder false, Standard ist false. Bei true wird die Debug Ausgabe eingeschaltet, sodass Fehler in der SQL Query angezeigt werden 


<a name="einfaches_beispiel"></a>
### Ein einfaches Beispiel

```
$form = rex_form::factory('rex_adressen', 'adressen', 'id=' . rex_request('id', 'int', 0));
$form->addParam('id',rex_request('id', 'int', 0));
$field = $form->addTextField('name');
$field->setLabel('Name');
$field = $form->addTextField('vorname');
$field->setLabel('Vorname');
$field = $form->addTextAreaField('text');
$field->setLabel('Notizen');
$form->show();
```

Erstellt ein Bearbeitungsformular für die Tabelle rex_adressen und fügt drei Felder in das Formular ein: name (input/text), vorname (input/text) und text (textarea). Das Formular muss mit einer gültigen Datensatz id aufgerufen werden.

<a name="beschreibung_der_methoden"></a>
### Beschreibung der Methoden zur Formatierung und zum Verhalten des Formulars

Die Formatierung und das Verhalten des Formulars kann weitestgehend konfiguriert werden. Hier werden die wichtigsten Methoden aufgeführt, die für eine Darstellung benötigt werden. Eine komplette Liste findet sich in der api Dokumentation von REDAXO https://redaxo.org/api/master/class-rex_form.html

#### `getUrl(array $params = [], $escape = true)`

Gibt eine Formular-Url zurück.
Beispiel: `echo '<a href="'.$form->getUrl(['id'=>0,'func'=>'add']).'">neuer Datensatz</a>'` erstellt ein leeres Formular, um einen neuen Datensatz zu erfassen.

#### `addFieldset($fieldset)`

Es wird ein neues Fieldset angelegt. Ein bereits geöffnetes Fieldset wird automatisch geschlossen. Beispiel: `$form->addFieldset('Details')`

> ***Hinweis:*** Alle Methoden, die Felder zum Formular hinzufügen, geben ein Objekt der Klasse `rex_form_element` zurück, welches weiter formatiert werden kann.

#### `addField($tag, $name, $value = null, array $attributes = [], $addElement = true)`

Fügt dem Formular ein Feld vom Typ `$tag` hinzu. Alle Methoden, welche Felder hinzufügen, rufen `addField` auf. Man benötigt diese Methode eher selten und nur für spezielle Fälle, in denen man das Feld besonders behandeln will. Im Normalfall werden die Standardmethoden verwendet.
Beispiel: `$form->addField('input','ort');` fügt ein Input type=text Feld für das Datenbankfeld ort in das Formular.

#### `addContainerField($name, $value = null, array $attributes = [])`

Fügt dem Formular ein Container-Feld hinzu. Ein Container-Feld kann weitere Felder enthalten. +++++ offen +++++

#### `addInputField($type, $name, $value = null, array $attributes = [], $addElement = true)`

Fügt dem Formular ein Input-Feld mit dem Type `$type` hinzu. Alle Methoden, welche Felder hinzufügen, rufen `addInputField` auf. Wird nur im Ausnahmefall direkt benötigt.

#### `addTextField($name, $value = null, array $attributes = [])`

Fügt dem Formular ein Text-Feld hinzu. Beispiel: `$field = $form->addTextField('vorname');` erzeugt ein Input Feld für das Datenbankfeld vorname.

#### `addReadOnlyTextField($name, $value = null, array $attributes = [])`

Fügt dem Formular ein Readonly Text-Feld hinzu. Beispiel: `$field = $form->addReadOnlyTextField('vorname');` erzeugt ein Input Feld für das Datenbankfeld vorname, welches mit dem HTML Attribute readonly versehen ist.

#### `addReadOnlyField($name, $value = null, array $attributes = [])`

Fügt dem Formular den Wert eines Feldes in einem `<p>`-Tag hinzu. Beispiel: `$field = $form->addReadOnlyField('vorname');`

#### `addHiddenField($name, $value = null, array $attributes = [])`

Fügt dem Fomular ein Hidden-Feld hinzu. Beispiel: `$form->addHiddenField('createdate', date())`. Ins Feld createdate wird das aktuelle Datum geschrieben.
***Hinweis:*** Da der Feldname von rex_form in ein Array umgewandelt wird, kann man Hidden Felder nicht zur Steuerung des Programms verwenden. Hierzu sollte man die Methode `addRawField` verwenden.

#### `addCheckboxField($name, $value = null, array $attributes = [])`

Fügt dem Fomular eine Checkbox-Gruppe hinzu. `addOption` fügt jeweils eine weitere Checkbox zur Gruppe hinzu, wie das Beispiel zeigt. Die Werte werden im Datenbankfeld mit Pipe (senkrechter Strich `|`) getrennt abgelegt. Daher ist es sinnvoll auf senkrechte Striche in den Werten zu verzichten.

```
$field = $form->addCheckboxField('bestellung');
$field->setLabel("Checkbox");
$field->addOption('Pizza Margherita', 'pizza_436');
$field->addOption('Pasta Gorgonzola', 'pasta_768');
```

#### `addRadioField($name, $value = null, array $attributes = [])`

Fügt dem Fomular eine Radiobutton-Gruppe hinzu. `addOption` fügt jeweils einen weiteren Radiobutton zur Gruppe hinzu, wie das Beispiel zeigt.

```
$field = $form->addRadioField ('getraenk');
$field->setLabel('Getränk');
$field->addOption ('Bier (0,33l)', 'bier_033');
$field->addOption ('Limo (0,5l)', 'limo_05');
```

#### `addTextAreaField($name, $value = null, array $attributes = [])`

Fügt dem Formular ein Textarea-Feld hinzu. Beispiel: `$field = $form->addTextAreaField('text');`. Die rex_form Klasse prüft keine Datentypen. Daher ist die Programmiererin selbst dafür verantwortlich, dass das Datenbankfeld auch vom Typ text ist.

#### `addSelectField($name, $value = null, array $attributes = [])`

Fügt dem Formular ein Select/Auswahl-Feld hinzu. Das Beispiel zeigt die Optionen für das Select-Feld:

```
$field = $form->addSelectField('bestellung','',['class'=>'form-control selectpicker']); // die Klasse selectpicker aktiviert den Selectpicker von Bootstrap
$field->setAttribute('multiple', 'multiple');
$field->setLabel("Select");
$select = $field->getSelect();
$select->setSize(3);
$select->addOption('Fisch', 'fisch');
$select->addOption('Fleisch', 'fleisch');
$select->addOption('Vegetarisch', 'vegetarisch');
```

#### `addPrioField($name, $value = null, array $attributes = [])`

Etwas ganz tolles: das Prio-Feld aktualisiert automatisch einen Sortierschlüssel, der für eine sortierte Ausgabe verwendet werden kann.

```
$field = $form->addPrioField('prio');
$field->setLabel('Priorität');
$field->setAttribute('class', 'selectpicker form-control');
$field->setLabelField('name');
```

**Hinweis:** Das Prio-Feld muss vom Typ int sein. Die Angabe von setLabelField ist zwingend. Das LabelField wird bei der Anzeige des Prio Feldes benötigt, um einen Datensatz bei der Auswahl zu identifizieren.

#### `addMediaField($name, $value = null, array $attributes = [])`

Fügt dem Formular ein Feld hinzu mit dem der Medienpool angebunden wird. Es kann nur ein Element aus dem Medienpool eingefügt werden.
Beispiel: `$field = $form->addMediaField('bild');` fügt ein Mediafeld für die Tabellenspalte *bild* ein.

#### `addMedialistField($name, $value = null, array $attributes = [])`

Fügt dem Formular ein Feld hinzu mit dem der Medienpool angebunden wird. Damit können mehrere Elemente aus dem Medienpool eingefügt werden. Die einzelnen Medien werden im Datenfeld durch Komma getrennt.
Beispiel: `$field = $form->addMedialistField('bilder');` fügt ein Medialistfeld für die Tabellenspalte *bilder* ein.

#### `addLinkmapField($name, $value = null, array $attributes = [])`

Fügt dem Formular ein Feld hinzu mit dem die Struktur-Verwaltung angebunden wird. Es kann nur ein Element aus der Struktur eingefügt werden.
Beispiel: `$field = $form->addLinkmapField('link');` fügt ein Linkfeld für die Tabellenspalte *link* ein.

#### `addLinklistField($name, $value = null, array $attributes = [])`

Fügt dem Formular ein Feld hinzu mit dem die Struktur-Verwaltung angebunden wird. Es können mehrere Elemente aus der Struktur eingefügt werden.
Beispiel: `$field = $form->addLinklistField('links');` fügt ein Linklistfeld für die Tabellenspalte *links* ein.

#### `addRawField($html)`

Fügt dem Formular beliebiges HTML zu. Braucht man auch immer mal wieder.
Beispiel: `$field = $form->addRawField('<input type="hidden" name="id" value="'.rex_request('id', 'int', 0).'">');` fügt dem Formular ein Hidden Field per HTML hinzu, welches mit einem Wert aus dem Request gefüllt wird.

#### `addErrorMessage($errorCode, $errorMessage)`

Fügt dem Formular eine Fehlermeldung hinzu. ??????????

#### `addParam($name, $value)`

Fügt dem Formular einen Parameter hinzu. Diese werden an den Stellen eingefuegt, an denen das Fomular neue Requests erzeugt.
Damit lassen sich Werte "merken", z.B. die aktuelle Position des Pagers, oder Sortiereinstellung und Sortierrichtung der aufrufenden Liste.
Beispiele:
`$form->addParam('id',rex_request('id', 'int', 0));
$form->addParam('sort',rex_request('sort', 'string', ''));
$form->addParam('sorttype',rex_request('sorttype', 'string', ''));
$form->addParam('start',rex_request('start', 'int', 0));`

#### `getParams()`

Gibt alle Parameter des Fomulars zurück.
Beispiel: `dump($form->getParams())`

	array:7 [
		"page" => "project"
		"func" => "edit"
		"list" => "adressen"
		"id" => 8
		"sort" => "name"
		"sorttype" => "asc"
		"start" => 10
	]

#### `getWhereCondition()`

Gibt die Where-Bedingung des Formulars als String zurück.
Beispiel: `dump($form->getWhereCondition())` zeigt `id=8`

#### `getParam($name, $default = null)`

Gibt den Wert des Parameters `$name` zurück oder `$default` wenn kein Parameter mit dem Namen exisitiert.
Beispiel: `dump($form->getParam('id',0);)` zeigt z.B. `8`

#### `createInput($inputType, $name, $value = null, array $attributes = [])`

Erstellt ein Input-Element anhand des Strings `$inputType`.

#### `setLanguageSupport($idField, $clangField)`

Mehrsprachigkeit unterstützen.

#### `setEditMode($isEditMode)`

Wechselt den Modus des Formulars.
Beispiel: `$form->setEditMode($func == 'edit');`

#### `isEditMode()`

Prüft ob sich das Formular im Edit-Modus befindet.

#### `setApplyUrl($url)`

Setzt die Url die bei der apply-action genutzt wird.
Beispiel: `$form->setApplyUrl(rex_url::currentBackendPage());`

<a name="beispiel_mit_rex_list"></a>
### Beispiel mit im Zusammenspiel mit `rex_list`

Dies ist ein einfaches Beispiel für die Darstellung einer Liste und eines Bearbeitungsformulars mit den Funktionen *bearbeiten*, *hinzufügen* und *löschen* (im Formular) auf Basis einer einfachen Datentabelle `rex_adressen`. In diesem Beispiel werden nur die Felder id, name und vorname verwendet.

Zusätzlich wird für die Ausgabe ein Fragment verwendet.

```
$func = rex_request('func','string','');
$table = 'adressen'; // rex_adressen - Prefix wird durch rex::getTable hinzugefügt

// Das Formular wird angezeigt, wenn der Request Parameter func (get oder post) gleich "add" oder "edit" ist
if (in_array($func,['add','edit'])) {
    // Formular Objekt erstellen
    $form = rex_form::factory(rex::getTable($table), 'Adressen', 'id=' . rex_request('id', 'int', 0),'post',false);
    // Die Id muss immer mit übergeben werden, sonst funktioniert das Speichern nicht
    $form->addParam('id',rex_request('id', 'int', 0));
    // Sortierparameter werden ebenso behalten wie die Position in der Liste
    $form->addParam('sort',rex_request('sort', 'string', ''));
    $form->addParam('sorttype',rex_request('sorttype', 'string', ''));
    $form->addParam('start',rex_request('start', 'int', 0));
    
    // Textfeld Name mit Label Nachname
    $field = $form->addTextField('name');
    $field->setLabel('Nachname');
	$field->getValidator()->add( 'notEmpty', 'Das Feld Nachname darf nicht leer sein.');
    
    // Textfeld vorname mit Label Vorname
    $field = $form->addTextField('vorname');
    $field->setLabel('Vorname');
    
    // Formular auslesen
    $content = $form->get();
    
} else {
    // Listenobjekt erstellen. 10 Datensätze pro Seite
    $list = rex_list::factory('SELECT id,name,vorname FROM '.rex::getTable($table), 5, $table, 0);
    
    // Icon für die erste Spalte "+" = hinzufügen
    $th_icon = '<a href="'.$list->getUrl(['func' => 'add']).'" title="'.rex_i18n::msg('add').'"><i class="rex-icon rex-icon-add-action"></i></a>';
    // Edit-Icon
    $td_icon = '<i class="rex-icon fa-file-text-o"></i>';
    $list->addColumn($th_icon, $td_icon, 0, ['<th class="rex-table-icon">###VALUE###</th>', '<td class="rex-table-icon">###VALUE###</td>']);
    $list->setColumnParams($th_icon, ['func' => 'edit', 'id' => '###id###', 'start' => rex_request('start', 'int', NULL)]);
    
    // die Spalte name wird sortierbar
    $list->setColumnSortable('name');
    // Liste auslesen
    $content = $list->get();
}

// Listen- und Formularinhalt in Fragment "section" ausgeben
$fragment = new rex_fragment();
$fragment->setVar('class', 'edit', false);
$fragment->setVar('title', 'Formlabel', false);
$fragment->setVar('body', $content, false);
$content = $fragment->parse('core/page/section.php');

echo $content;
```

<a name="eingabefelder-validieren"></a>
### Eingabefelder validieren

Die Eingaben von rex_form-Eingabefeldern können vor dem Absenden des Formulars validiert werden. Dazu werden dem validator-Objekt des Eingabefelds ein oder mehrere Validatoren hinzugefügt:

    $field->getValidator()->add( string $type, null|string $message = null, mixed $option = null )
    
$type bezeichnet die Validator-Funktion, $message die auszugebende Fehlermeldung und $option weitere Parameter für die Prüfung

Folgende Validatoren sind verfügbar:

Name | Beschreibung | Parameter | Beispiel
------------- | ------------- | ------------- | -------------
notEmpty	| prüft, ob ein Eingabefeld leer ist | - | `$field->getValidator()->add( 'notEmpty', 'Das Feld Nachname darf nicht leer sein.');`
type	| prüft den Wert des Eingabefelds auf einen Variablentyp | Variablentyp: (int/integer, float, real) | `$field->getValidator()->add( 'type', 'Bitte einen ganzzahligen Wert eingeben', 'int');`
minLength | prüft auf eine Mindestlänge des Feldinhalts | Anzahl Zeichen Mindestlänge | `$field->getValidator()->add( 'minLength', 'Min 10 Zeichen', 10);`
maxLength | prüft auf eine Maximallänge des Feldinhalts | Anzahl Zeichen Maximallänge | `$field->getValidator()->add( 'maxLength', 'Max 12 Zeichen', 12);`
match | Wendet einen regulären Ausdruck an | regulärer Ausdruck | `$field->getValidator()->add( 'match', 'Das Feld PLZ muss fünf Ziffern enthalten.', '/^[0-9]{5}$/');`
notMatch | prüft, ob regulärer Ausdruck nicht erfüllt ist. | regulärer Ausdruck | `$field->getValidator()->add( 'notMatch', 'Bitte keine Ziffern eingeben', '/[0-9]/');`
min  | prüft, ob der eingegebene Wert größer oder gleich dem Vergleichswert ist.  | Vergleichswert  | $field->getValidator()->add( 'min', 'Mindestens 9999 eingeben', 9999);
max  | prüft, ob der eingegebene Wert kleiner oder gleich dem Vergleichswert ist.  | Vergleichswert  | $field->getValidator()->add( 'max', 'Mindestens 9999 eingeben', 9999);
url  | prüft auf url  | - | `$field->getValidator()->add( 'url', 'Bitte eine url eingeben');`
email  | prüft auf E-Mail Adresse  | - | `$field->getValidator()->add( 'email', 'Bitte eine E-Mail Adresse eingeben');`
values  | prüft, ob der eingegebene Wert einem der Werte entspricht  | `$field->getValidator()->add( 'values', 'eins, zwei oder drei eingeben', ['eins','zwei','drei']);`
custom  | prüft über eine Custom Function. Die Funktion erhält als Parameter den Wert des Feldes. Wenn die Funktion false zurück gibt, wird die Fehlermeldung ausgegeben.  | `$field->getValidator()->add( 'custom', 'Eingabe ungültig', 'myclass::myfunc');`

> **Hinweis:** 
Alle Validator-Typen außer notempty führen die Prüfung erst dann durch, wenn der Feldinhalt nicht leer ist. Soll also z.B. ein Eingabefeld obligatorisch eine deutsche Postleitzahl enthalten, muss zusätzlich zum match auf /^[0-9]{5}$/' auch ein notempty-Validator hinzugefügt werden.
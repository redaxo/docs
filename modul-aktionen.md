# Modul-Aktionen

- [Aktions-Übersicht](#aktions-uebersicht)
- [Aktion erstellen](#aktion-erstellen)
  - [Auf Werte zugreifen](#auf-werte-zugreifen)
  - [Speichern (verhindern)](#speichern-verhindern)
  - [Meldung ausgeben](#meldung-ausgeben)
- [Beispiele](#beispiele)
  - [Preview-Aktion](#beispiel-preview-aktion)
  - [Presave-Aktionen](#beispiel-presave-aktionen)
    - [Beispiel 1: HTML Text aus WYSIWYG-Editoren modifizieren](#beispiel-html-text)
    - [Beispiel 2: Multiselect aus Datenbank speichern](#beispiel-multiselect)
    - [Beispiel 3: Validierung](#beispiel-validierung)
  - [Postsave-Aktion](#beispiel-postsave-aktion)

<a name="aktions-uebersicht"></a>

## Aktions-Übersicht

In der Standardkonfiguration von REDAXO existieren drei Events, bzw. Aktionen für Module, die automatisch ausgeführt werden.

Aktion | Beschreibung
------------- | -------------
Preview | Wird vor dem Anzeigen des Moduls ausgeführt.
Presave | Wird vor dem Speichern des Moduls ausgeführt.
Postsave | Wird nach dem Speichern des Moduls ausgeführt.

<a name="aktion-erstellen"></a>

## Aktion erstellen

Es ist wichtig, die korrekte Aktion zu verwenden:

- Presave eignet sich sehr gut, um Daten vor dem Speichervorgang zu manipulieren.
- Mit Postsave kann man Daten nach dem Speichervorgang weiter verarbeiten.

Aktionen finden sich in einem eigenen Tab bei den Modulen. Wenn man eine neue Aktion anlegt, wird der betreffende Code in die Felder für Preview, Presave und/oder Postsave eingesetzt. Für jede dieser drei Varianten lässt sich definieren, bei welchem Event die Aktion ausgeführt wird: beim Hinzufügen eines Modules (ADD), beim Bearbeiten eines Moduls (EDIT) oder beim Löschen eines Moduls (DELETE). Letzteres Event steht bei der Preview-Aktion nicht zur Verfügung.

Sobald eine Aktion existiert, findet sich beim Bearbeiten eines Moduls ein weiteres Select-Feld, mit dem man die Aktion schließlich dem Modul hinzufügen kann.

  > **Hinweis:**
Eine Aktion kann einem Modul erst zugewiesen werden, nachdem das Modul gespeichert wurde. Es ist also nicht möglich, die Aktion direkt bei der Erstellung eines Moduls zuzuweisen. Die Auswahlmöglichkeit für die Zuweisung einer Aktion zu einem Modul erscheint erst, wenn das Modul bereits existiert.

<a name="auf-werte-zugreifen"></a>

### Auf Werte zugreifen

Normalerweise wird man beispielsweise in Presave-Aktionen Werte überprüfen oder verändern, die zuvor in einem Modulblock eingegeben wurden. Auf die entsprechenden Werte kann man zugreifen mit

    $text = $this->getValue(1);  // Beispiel für REX_VALUE[1]

oder

    $medialist1 = $this->sql->getValue('medialist1'); // Beispiel für das Feld medialist1

Wenn man die Werte in einer Presave-Aktion ändern will, so kann man diese speichern mit

    $this->setValue(1,$text); // Beispiel für REX_VALUE[1]

oder

    $this->sql->setValue('medialist2','ichbinaucheinbild.jpg'); // Beispiel für das Feld medialist2

Man kann auf alle Werte im Slice zugreifen, also auf alle Felder, die in einem Modulblock eingetragen wurden. Auch eigene Datenfelder, die zuvor in der Tabelle `rex_article_slice` angelegt wurden, können mit Aktionen bearbeitet werden.

<a name="speichern-verhindern"></a>

### Speichern verhindern

Die die Werte werden gewohnt verarbeitet.

Möchte man das Speichern verhindern steht folgedne Methode zur Verfügung

```php
$this->setSave(false);
```

Um das Speichern durchzuführen

```php
$this->setSave(true);
```

<a name="meldung-ausgeben"></a>

### Medlung ausgeben

```php
 $this->messages[] = 'Beliebieger Text';
```

<a name="beispiele"></a>

## Beispiele

<a name="beispiel-preview-aktion"></a>

### Preview-Aktion

In einem Modul soll es ein Feld für die Datumseingabe geben, das Feld soll aber änderbar sein. Beim Anlegen soll das Feld mit dem aktuellen Wert vorausgefüllt werden. Das Beispiel geht davon aus, dass es sich um das Feld REX_VALUE[2] handelt.

    <?php
    if ($this->getValue(2) == '') {
       $this->setValue(2,date('d.m.Y'));
    }
    ?>

<a name="beispiel-presave-aktionen"></a>

### Presave-Aktionen

<a name="beispiel-html-text"></a>

#### Beispiel 1: HTML Text aus Wysiwyg-Editoren modifizieren

In dieser Aktion geht es darum, aus einem Wysiwyg-Editor (z.B. Redactor, TinyMCE) stammenden HTML-Text zu prüfen und gegebenenfalls zu ändern.
Folgender Code wird also ins Feld "Presave-Aktion" eintragen und dann den Events Add und Edit zugewiesen:

    <?php
    // REX_VALUE[1] auslesen
    $text = $this->getValue(1);
    // alle style="..." Stellen löschen
    $text = preg_replace('/ style=".*?"/', '', $text);
    // alle leeren Absätze löschen
    $text = preg_replace('/<p>\s*<\/p>/', '', $text);
    // alle Urls aus Ankerlinks löschen
    $text = preg_replace('/ href="(.*?)#(.{1,30})"/', ' href="#$2"', $text);
    // Alle Zeilenumbrüche raus
    $text = preg_replace("/\r|\n|\r\n/", ' ', $text);
    // ersetzten Text wieder in REX_VALUE[1] schreiben
    $this->setValue(1,$text);                            
    ?>

Die fertige Aktion muss man dann noch dem Modul mit dem Wysywig-Text zuweisen. Die Aktion geht davon aus, dass das Modul den Text in das Feld REX_VALUE[1] speichert.

<a name="beispiel-multiselect"></a>

#### Beispiel 2: Multiselect aus Datenbank speichern

Um ein Multiselect-Feld in einem Modul für das Backend zu erstellen, muss man einen kleinen Umweg gehen, da die REX_VALUE-Felder Text zurückgeben, Werte aus Multiselect-Feldern aber sinnvollerweise als Array verarbeitet werden.
Die im Multiselect ausgewählten Werte (in diesem Falle IDs) sollen kommasepariert im REX_VALUE[1] abgelegt werden.

Der komplette Modul-Input kann dann beispielsweise so aussehen:

    <?php
      // Datenbankelemente für Multiselect-Feld auslesen
      $sql = rex_sql::factory();
      $qry = "SELECT name, id FROM rex_meinetabelle ORDER BY name";
      $sql->setQuery($qry);
      $res = $sql->getArray();

      // Multiselect-Werte aus REX_VALUE[1] auslesen 
      $multiselect = explode(',',"REX_VALUE[1]");
    ?>

    // Select-Feld kann einen beliebigen Namen haben, muss aber als Array definiert werden
    <select name="my_multiselect[]" multiple="multiple" size="5">
      <?php foreach ($res as $o) : ?>
       <option value="<?= $o['id'] ?>" <?= in_array($o['id'],$multiselect) ? 'selected="selected" ' : '' ?>><?= $o['name'] ?> ?></option>
       <?php endforeach ?>
    </select>

Die hierzu passende Presave-Aktion nimmt die Werte von `my_multiselect` entgegen, macht einen kommaseparierten String daraus und gibt den String an `value1` weiter.

    <?php
    $this->sql->setValue('value1',implode(',',rex_post('my_multiselect','array')));
    ?>

<a name="beispiel-validierung"></a>

#### Beispiel 3: Validierung

Eingaben können in REDAXO-Modulen per Javascript validiert werden, doch manchmal ist eine Aktion, wo man PHP verwenden kann, die bessere Wahl. Auch hierzu wird wieder die Presave-Aktion verwendet. Im Beispiel wird geprüft, ob REX_VALUE[1] leer ist. Ist die Bedingung erfüllt, wird der Block nicht gespeichert und stattdessen eine Meldung ausgegeben.

    <?php
    if ($this->getValue(1) == '') {
       // Der Block wird nicht gespeichert
       $this->save = false;
       // Meldung ausgeben
       $this->messages[] = 'Bitte Wert in Feld 1 eintragen.';   
    }
    ?>

<a name="beispiel-postsave-aktion"></a>

### Postsave-Aktion

Postsave-Aktionen werden hauptsächlich verwendet, um nach dem Speichern des Slices weitere Aktionen durchzuführen, z.B. eine Benachrichtung absetzen oder eine Meldung auf Twitter zu hinterlegen. Hierfür wird manchmal auch die ID des Slices benötigt. Die Slice-ID wird jedoch erst beim Speichervorgang vergeben und ist daher bei einem neu angelegten Slice noch nicht direkt verfügbar. Das Beispiel zeigt, wie man dann trotzdem an die Slice-ID kommt. Außerdem demonstriert das Beispiel, wie man an die Werte von REX_ARTICLE_ID, REX_CLANG_ID, REX_CTYPE_ID und REX_MODULE_ID erreicht.

    <?php
    $slice_id = "REX_SLICE_ID";
    if ($slice_id == 0 && $this->event == 'add') {
       $qry = 'SELECT id id FROM '.rex::getTablePrefix().'article_slice WHERE '
             . 'clang_id = REX_CLANG_ID AND '
             . 'ctype_id = REX_CTYPE_ID AND '
             . 'article_id = REX_ARTICLE_ID AND '
             . 'module_id = REX_MODULE_ID AND '
             . 'createuser = "'.rex::getUser()->getValue('login').'"'
             . ' ORDER BY id DESC';

       $sql = rex_sql::factory();
       $sql->setQuery($qry);
       if ($res = $sql->getArray()) {
          $slice_id = $res[0]['id'];
       }   
    }
    ?>

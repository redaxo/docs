# Module

- [Einführung](#einfuehrung)
- [Entwickler: Module erstellen](#entwickler)
  - [Input](#input)
  - [Output](#output)
  - [Aktionen](#aktionen)
- [Administratoren: Module verwalten](#redakteure)
  - [Module in Templates und C-Types beschränken](#beschraenken)
- [Redakteure: Module verwenden](#redakteure)
  - [Inhaltsblöcke hinzufügen](#hinzufuegen)
  - [Slices verschieben](#verschieben)
- [Beispiele](#beispiele)
  - [Einfaches Textmodul](#textmodul)
  - [Bildmodul](#bildmodul)
  - [Inhaltsübersicht für Artikel](#teaser)
  - [Interne Linkliste mit `REX_LINKLIST`](#linkliste)
  - [Checkboxen in Modulen](#checkbox)
- [PHP-Alternativen für REDAXO-Variablen](#php-alternativen)

<a name="einfuehrung"></a>

## Einführung

Jede Inhaltsseite in einer REDAXO-Website ist aus einem oder mehreren Modulen zusammengesetzt. Module bilden die Inhaltscontainer und werden als Blöcke im Backend auf einer Seite (Artikel) platziert.

Jedes Modul hat einen Eingabeteil, der mit verschiedensten Eingabeelementen versehen werden kann. Der Eingabeteil kann auch entfallen, wenn keine redaktionellen Inhalte erfasst werden sollen.

Eingabeelemente können zum Beispiel sein:

- ein oder mehrere Textfelder
- Elemente für die Auswahl von Dateien aus dem Medienpool
- Elemente für die Auswahl von Links
- Auswahlelemente (Selectfelder)

In einen Artikel eingesetzte Modulblöcke bilden die so genannten Slices, aus denen sich der gesamte Inhalt einer Seite zusammensetzt.

Ein Slice hat einen vordefinierten Satz an Variablen, die für die Benutzerelemente zur Verfügung stehen. Diese Variablen werden über eine eigene Syntax angesprochen. Die Variablen sowohl für die Eingabe als auch für die Ausgabe werden ausführlich im Kapitel [REDAXO-Variablen (REX_VARs)](/{{path}}/{{version}}/redaxo-variablen) beschrieben.

<a name="entwickler"></a>

## Entwickler: Module erstellen

Ein Modul wird im Backend beim Menüpunkt `Module` erstellt. Die Benennung der Module kann frei gewählt werden. Da die Reihenfolge der Module in der Auswahlliste nach Namen sortiert wird, sind die Namen für eine gewisse Struktur relevant. Um die Reihenfolge besser kontrollieren zu können, könnte man dem Namen Zahlen voranstellen.

<a name="input"></a>

### Input

Im Eingabeteil werden die Felder definiert, die der Redakteur bei der Eingabe der Inhalte sieht. Der Eingabeteil kann individuell gestaltet werden und mit beliebigem HTML-Code formatiert werden. Da das REDAXO-Backend auf dem Frontend-Framework Bootstrap basiert, kann man Bootstrap-Markup verwenden. Der Eingabeteil kann aus PHP-Code und HTML bestehen. Alle Klassen des Frameworks (Core, AddOns) stehen zur Verfügung.

<a name="output"></a>

### Output

Der Ausgabecode wird von REDAXO ausgeführt und im Frontend ausgegeben. Auch hier stehen alle Klassen und Funktionen des Frameworks zur Verfügung.

PHP-Variablen, die in einem Modul definiert wurden, stehen in den nachfolgenden Slices zur Verfügung. So kann beispielsweise die Anzahl der Module auf einer Seite gezählt werden.

**TIPP** Die Abarbeitung eines Moduls kann in der Ausgabe mittels `return` beendet werden. Die Verarbeitung wird dann mit dem nächsten Modul fortgesetzt.

```php
<p>Dieser Text wird ausgegeben</p>
<?php return; ?>
<p>Dieser Text wird nicht ausgegeben</p>
```

<a name="aktionen"></a>

### Aktionen

Beim Anzeigen oder Speichern eines Moduls können zusätzliche Aktionen ausgeführt werden. Siehe hierzu das Kapitel [Aktionen](/{{path}}/{{version}}/aktionen).

> **Hinweis:** Wenn ein Modulblock in einem Artikel neu hinzugefügt wird, so ist die Slice-ID noch nicht vergeben. Daher können dem Slice beim einfügen auch keine Aktionen zugewiesen werden.

<a name="administratoren"></a>

## Administratoren: Module verwalten

<a name="beschraenken"></a>

### Module in Templates und C-Types beschränken

Der Administrator kann die Verwendung von Modulen für Benutzergruppen und Templates einschränken. In jedem Template lässt sich einstellen, ob bestimmte Module für bestimmte C-Types (Spalten) zur Verfügung stehen oder nicht.  Nähere Informationen dazu liefert das [Template-Kapitel](/{{path}}/{{version}}/templates).

Auch für Benutzergruppen (Rollen) lässt sich einstellen, ob alle Module verfügbar sein sollen oder nur ausgewählte Module. Dadurch kann man die Übersicht bei der Modulauswahl verbessern. Auch lässt sich durch eine definierte Verfügbarkeit die fälschliche Verwendung von Inhaltsmodulen vermeiden: Wenn ein Modul erstellt wurde, welches nur in der Seitenspalte einer Seite verwendet werden soll, so kann es bei korrekter Einstellung nicht in der Hauptspalte eingesetzt werden.

<a name="redakteure"></a>

## Redakteure: Module verwenden

<a name="hinzufuegen"></a>

### Inhaltsblöcke hinzufügen

REDAXO Artikel sind, wenn sie erstellt werden, zunächst leer. Über die Dropdownliste `Block hinzufügen` lässt sich ein neuer Inhaltsblock in den Artikel einsetzen. Es erscheint dann die Inhaltsmaske mit Feldern, die im Modul Input definiert wurde. Ein Block lässt sich vor oder hinter einem vorhandenen Block einfügen.

<a name="verschieben"></a>

### Slices verschieben

Die eingesetzten Modulblöcke kann man bei Bedarf über die Pfeile nach oben oder unten verschieben und dadurch in ihrer Reihenfolge verändern.

<a name="beispiele"></a>

## Beispiele

<a name="textmodul"></a>

### Einfaches Textmodul

**Eingabe**:

```html
<label>Überschrift</label>
<input type="text" name="REX_INPUT_VALUE[1]" value="REX_VALUE[1]">

<label>Introtext</label>
<textarea rows="6" name="REX_INPUT_VALUE[2]">REX_VALUE[2]</textarea>
```

Auch wenn die Eingabe der Inhalte so bereits funktioniert, so sieht das noch nicht so hübsch aus. Um die Optik auch für den Redakteur etwas ansehnlicher zu gestalten, könnte man die Bootstrap-CSS-Klassen für das Styling verwenden:

**Optisch gestylte Eingabe**:

```html
<fieldset class="form-horizontal">
    <div class="form-group">
        <label class="col-sm-2 control-label">Überschrift</label>
        <div class="col-sm-10">
            <input class="form-control" type="text" name="REX_INPUT_VALUE[1]" value="REX_VALUE[1]">
        </div>
    </div>

    <div class="form-group">
        <label class="col-sm-2 control-label">Introtext</label>
        <div class="col-sm-10">
            <textarea class="form-control" rows="6" name="REX_INPUT_VALUE[2]">REX_VALUE[2]</textarea>
        </div>
    </div>
</fieldset>
```

Der Code zur Ausgabe ist noch einfacher – zumindest wenn man REDAXO-Variablen nutzt. Über den Prefix und Suffix kann man die umschließenden HTML-Tags für die beiden Felder definieren.

**Ausgabe:**

```html
<div class="jumbotron">
    REX_VALUE[id='1' prefix='<h1>' suffix='</h1>']
    REX_VALUE[id='2' prefix='<p>' suffix='</p>']
</div>
```

<a name="bildmodul"></a>

### Bildmodul

**Eingabe**:

```html
<label>Bild 1</label>
REX_MEDIA[id="1" widget="1"]

<label>Bild 2</label>
REX_MEDIA[id="2" widget="1"]

<label>Galerie</label>
REX_MEDIALIST[id="1" widget="1"]

```

Auch dieses Modul lassen sich die Felder noch etwas hübscher darstellen.

**Optisch gestylte Eingabe**:

```html
<fieldset class="form-horizontal">
    <div class="form-group">
        <label class="col-sm-2 control-label">Bild 1</label>
        <div class="col-sm-10">
            REX_MEDIA[id="1" widget="1"]
        </div>
    </div>

    <div class="form-group">
        <label class="col-sm-2 control-label">Bild 2</label>
        <div class="col-sm-10">
            REX_MEDIA[id="2" widget="1"]
        </div>
    </div>

    <div class="form-group">
        <label class="col-sm-2 control-label">Galerie</label>
        <div class="col-sm-10">
            REX_MEDIALIST[id="1" widget="1"]
        </div>
    </div>
</fieldset>
```

Nun fehlt noch die Ausgabe. Für die Ausgabe der Bilder sollte man prüfen, ob wirklich ein Bild hinterlegt wurde und nur dann das Bildelement ausgeben.

**Ausgabe**

```php
<div class="row">
    <div class="col-lg-6">
        <?php
        if ("REX_MEDIA[1]" != '')
        {
            echo '<img class="img-responsive" src="'.rex_url::base('media/REX_MEDIA[1]').'">';
        }
        ?>
    </div>

    <div class="col-lg-6">
        <?php
        if ("REX_MEDIA[2]" != '')
        {
            echo '<img class="img-responsive" src="'.rex_url::base('media/REX_MEDIA[2]').'">';
        }
        ?>
    </div>
</div>

<div class="row">
    <?php
    foreach (explode(',', "REX_MEDIALIST[1]") as $img)
    {
        echo '<div class="col-lg-4">';
            echo '<img class="img-responsive" src="'.rex_url::base('media/'.$img).'">';
        echo '</div>';
    }
    ?>

</div>
```

<a name="teaser"></a>

### Inhaltsübersicht für Artikel

Dieses Modul listet alle Artikel innerhalb einer Kategorie auf, die den Status `online` haben und nicht der Startartikel sind.
Die Einträge werden in der Überschrift verlinkt, als Beschreibung wird der Text ausgegeben, der in den Metadaten des Artikels im Feld `Beschreibung` eingetragen ist.
Dieser Code kann als Basis für Artikelteaser verwendet werden.

**Eingabe**

nicht erforderlich

**Ausgabe**

```php
<?php
$articles = rex_category::getCurrent()->getArticles(true);

echo '<ul>';
    foreach ($articles as $art) {
        if ($art->isStartArticle()) {
            continue;
        }
        echo '<li>';
            echo '<h3><a href="'.rex_getUrl($art->getId()).'">'.$art->getName().'</a></h3>';
            echo '<p>'.$art->art_description.'</p>';
        echo '</li>';
    }
echo '</ul>';
?>
```

<a name="linkliste"></a>

### Interne Linkliste mit `REX_LINKLIST`

Einzelne Artikel können durch den Redakteur ausgewählt werden und so als Liste ausgegeben werden. Das Modul erstellt ein Bootstrap-Panel mit einer Artikelliste.

#### Moduleingabe

```html
<fieldset class="form-horizontal">
 <div class="form-group">
  <label class="col-sm-2 control-label">Interne Links</label>
  <div class="col-sm-10">
   REX_LINKLIST[id="1" widget="1"]
  </div>
 </div>
</fieldset>
```

In der REX_Linklist werden die Werte (Artikel-IDs) kommasepariert gespeichert.

<a name="modulausgabe"></a>

##### Modulausgabe

In der Modulausgabe werden die Werte mitels explode (<http://php.net/manual/de/function.explode.php)> in einer foreach-Schleife ausgelesen. Anhand der ID holt man sich den Datensatz des Artikels. Wenn nur ein Link erzeugt werden soll, bietet sich die direkte Umwandlung des Datensatzes in einen Link mittels `->toLink()` an.

```php
<?php
if ("REX_LINKIST[1]" != "") {
  $menu = array();
  foreach(explode(',', 'REX_LINKLIST[1]') as $articleId) {

    // Artikeldatensatz auslesen
    $article = rex_article::get($articleId);
    if ($article) {

      // Erstelle Link aus aktuellem Artikel
      $menu[$articleId] = $article->toLink();
    }
  }

  // Ausgabe mit implode: http://php.net/manual/de/function.implode.php
  if (! empty($menu)) {
    echo '<ul><li>', implode('</li><li>', $menu), '</li></ul>';
  }
}

```

<a name="checkbox"></a>

### Beispiel für die Verwendung einer Checkbox in der Moduleingabe

Dieses Modul Beinhaltet eine Checkbox als Modul.

#### Moduleingabe

```html
<input type="hidden" name="REX_INPUT_VALUE[1]" value="0">
<input type="checkbox" name="REX_INPUT_VALUE[1]" value="1" REX_VALUE[id=1 instead=checked]>
```

<a name="modulausgabe"></a>

#### Modulausgabe

```php
<?php 

if(REX_VALUE[1])
    {
      echo "checked...";
    }
?>
```

<a name="php-alternativen"></a>

## PHP-Alternativen für REDAXO-Variablen

REDAXO-Variablen sind praktische Shortcuts, aber manchmal ist es notwendig oder vorteilhaft, die entsprechenden PHP-Methoden direkt zu verwenden. Hier sind die wichtigsten Entsprechungen:

### Slice-Daten auslesen

**REDAXO-Variable vs. PHP-Schreibweise:**

```php
// REDAXO-Variable
REX_VALUE[1]

// PHP-Alternative
$slice = $this->getCurrentSlice();
echo $slice->getValue(1);
```

```php
// REDAXO-Variable für Media
REX_MEDIA[1]

// PHP-Alternative
$slice = $this->getCurrentSlice();
echo $slice->getMedia(1);
```

```php
// REDAXO-Variable für Media-URL
// (in REDAXO-Variable würde man: /media/REX_MEDIA[1] verwenden)

// PHP-Alternative
$slice = $this->getCurrentSlice();
echo $slice->getMediaUrl(1);
```

```php
// REDAXO-Variable für Linklist
REX_LINKLIST[1]

// PHP-Alternative
$slice = $this->getCurrentSlice();
echo $slice->getLinklist(1);
```

```php
// REDAXO-Variable für Link-URL
REX_LINK[id=1 output=url]

// PHP-Alternative
$slice = $this->getCurrentSlice();
echo $slice->getLinkUrl(1);
```

### Arrays aus REDAXO-Variablen

**REDAXO-Variable vs. PHP-Schreibweise:**

```php
// REDAXO-Variable (Array-Zugriff)
$value1 = rex_var::toArray("REX_VALUE[1]");

// PHP-Alternative
$slice = $this->getCurrentSlice();
$value1 = $slice->getValueArray(1);
```

```php
// Medialist als Array
// REDAXO-Variable
foreach (explode(',', 'REX_MEDIALIST[1]') as $media) {
    // ...
}

// PHP-Alternative
$slice = $this->getCurrentSlice();
foreach ($slice->getMediaListArray(1) as $media) {
    // ...
}
```

```php
// Linklist als Array
// REDAXO-Variable
foreach (explode(',', 'REX_LINKLIST[1]') as $articleId) {
    // ...
}

// PHP-Alternative
$slice = $this->getCurrentSlice();
foreach ($slice->getLinkListArray(1) as $articleId) {
    // ...
}
```

### System-Informationen

**REDAXO-Variable vs. PHP-Schreibweise:**

```php
// REDAXO-Variable
REX_ARTICLE_ID

// PHP-Alternative
echo rex_article::getCurrentId();
```

```php
// REDAXO-Variable
REX_CATEGORY_ID

// PHP-Alternative
echo rex_category::getCurrentId();
```

```php
// REDAXO-Variable
REX_CLANG_ID

// PHP-Alternative
echo rex_clang::getCurrentId();
```

```php
// REDAXO-Variable
REX_USER_ID

// PHP-Alternative
echo rex::getUser() ? rex::getUser()->getId() : '';
```

```php
// REDAXO-Variable
REX_CONFIG[namespace=core key=server]

// PHP-Alternative
echo rex_config::get('core', 'server');
```

### Artikel- und Kategorie-Daten

**REDAXO-Variable vs. PHP-Schreibweise:**

```php
// REDAXO-Variable
REX_ARTICLE[id=5 field=name]

// PHP-Alternative
$article = rex_article::get(5);
echo $article ? htmlspecialchars($article->getValue('name')) : '';
```

```php
// REDAXO-Variable
REX_CATEGORY[id=3 field=name]

// PHP-Alternative
$category = rex_category::get(3);
echo $category ? htmlspecialchars($category->getValue('name')) : '';
```

### Template- und Modul-Informationen

```php
// REDAXO-Variable
REX_TEMPLATE_ID

// PHP-Alternative
echo rex_template::getCurrentId();
```

```php
// REDAXO-Variable
REX_MODULE_ID

// PHP-Alternative
echo rex_module::getCurrentId();
```

```php
// REDAXO-Variable
REX_SLICE_ID

// PHP-Alternative
$slice = $this->getCurrentSlice();
echo $slice->getId();
```

### Prüfungen und Validierung

```php
// REDAXO-Variable mit isset-Parameter
REX_VALUE[id=1 isset=1]

// PHP-Alternative
$slice = $this->getCurrentSlice();
echo $slice->getValue(1) !== '' ? 'true' : 'false';
```

```php
// REDAXO-Variable mit Callback
REX_VALUE[id=1 callback="htmlspecialchars"]

// PHP-Alternative
$slice = $this->getCurrentSlice();
echo htmlspecialchars($slice->getValue(1));
```

### Metadaten-Zugriff mit REDAXO-Variablen

REDAXO-Variablen können auch auf Metadatenfelder zugreifen:

```php
// Media-Metadaten abrufen
REX_MEDIA[id=1 field=title]           // Titel des Mediums
REX_MEDIA[id=1 field=med_description] // Beschreibung
REX_MEDIA[id=1 field=width]           // Bildbreite
REX_MEDIA[id=1 field=height]          // Bildhöhe
REX_MEDIA[id=1 field=filesize]        // Dateigröße
REX_MEDIA[id=1 field=filetype]        // Dateityp

// Artikel-Metadaten
REX_ARTICLE[id=5 field=name]          // Artikelname
REX_ARTICLE[id=5 field=description]   // Meta-Description
REX_ARTICLE[id=5 field=keywords]      // Meta-Keywords
REX_ARTICLE[id=5 field=updatedate]    // Änderungsdatum

// Kategorie-Metadaten
REX_CATEGORY[id=3 field=catname]      // Kategoriename
REX_CATEGORY[id=3 field=description]  // Kategorie-Beschreibung
```

**PHP-Alternativen für Metadaten:**

```php
// Media-Metadaten per PHP
$slice = $this->getCurrentSlice();
$media = $slice->getMedia(1);
if ($media) {
    $mediaObj = rex_media::get($media);
    if ($mediaObj) {
        echo $mediaObj->getTitle();           // Titel
        echo $mediaObj->getValue('med_description'); // Beschreibung
        echo $mediaObj->getWidth();           // Breite
        echo $mediaObj->getHeight();          // Höhe
        echo $mediaObj->getFilesize();        // Dateigröße
        echo $mediaObj->getExtension();       // Dateierweiterung
    }
}

// Artikel-Metadaten per PHP
$article = rex_article::get(5);
if ($article) {
    echo $article->getName();                    // Name
    echo $article->getValue('art_description');  // Description
    echo $article->getValue('art_keywords');     // Keywords
    echo $article->getUpdateDate();              // Änderungsdatum
}
```

### Erweiterte Beispiele

**Sichere Media-Ausgabe:**

```php
// REDAXO-Variable (einfache Implementierung)
if ("REX_MEDIA[1]" != '') {
    echo '<img src="/media/REX_MEDIA[1]">';
}

// Verbesserte REDAXO-Variable (mit Metadaten)
REX_MEDIA[id=1 prefix='<img src="/media/' suffix='" alt="REX_MEDIA[id=1 field=title]">' ifempty='']

// Oder noch besser mit verschiedenen Metadatenfeldern:
<img src="/media/REX_MEDIA[1]" 
     alt="REX_MEDIA[id=1 field=title]" 
     title="REX_MEDIA[id=1 field=med_description]"
     width="REX_MEDIA[id=1 field=width]" 
     height="REX_MEDIA[id=1 field=height]">

// PHP-Alternative (mit umfassender Fehlerbehandlung)
$slice = $this->getCurrentSlice();
$media = $slice->getMedia(1);
if ($media) {
    $mediaObj = rex_media::get($media);
    if ($mediaObj) {
        echo '<img src="' . $slice->getMediaUrl(1) . '" alt="' . htmlspecialchars($mediaObj->getTitle()) . '">';
    }
}
```

**Erweiterte Linklist-Verarbeitung:**

```php
// PHP-Alternative mit Fehlerbehandlung
$slice = $this->getCurrentSlice();
$links = $slice->getLinkListArray(1);

if (!empty($links)) {
    echo '<ul>';
    foreach ($links as $articleId) {
        $article = rex_article::get($articleId);
        if ($article && $article->isOnline()) {
            echo '<li><a href="' . rex_getUrl($articleId) . '">' . htmlspecialchars($article->getName()) . '</a></li>';
        }
    }
    echo '</ul>';
}
```

### Vorteile der PHP-Schreibweise

- **Mehr Kontrolle**: Direkter Zugriff auf alle Methoden der Objekte
- **Fehlerbehandlung**: Bessere Möglichkeiten für try-catch und Null-Checks
- **Performance**: Keine zusätzliche Parsing-Schicht
- **IDE-Support**: Bessere Code-Completion und Typsicherheit
- **Debugging**: Einfacheres Debugging mit Breakpoints
- **Typsicherheit**: Explizite Objekttypen statt String-basierte Variablen

### Wann welche Schreibweise verwenden?

**REDAXO-Variablen verwenden wenn:**
- Einfache, direkte Ausgabe gewünscht
- Keine komplexe Logik erforderlich
- Parameter wie `prefix`, `suffix`, `callback` nützlich sind
- Schnelle Prototyping-Phase

**PHP-Schreibweise verwenden wenn:**
- Komplexe Datenverarbeitung erforderlich
- Fehlerbehandlung wichtig ist
- Performance kritisch ist
- Mit anderen PHP-Objekten interagiert werden muss
- Code in einer IDE entwickelt wird
- Unit-Tests geschrieben werden sollen

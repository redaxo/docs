# Module

## Einführung

Jede Inhaltsseite in einer REDAXO Website ist aus einem oder mehreren Modulen zusammengesetzt. Module bilden die Inhaltscontainer und werden als Blöcke im Backend auf einer Seite platziert.

Jedes Modul hat einen Eingabeteil, der mit verschiedensten Eingabeelementen versehen werden kann. Der Eingabeteil kann auch entfallen, wenn keine redaktionellen Inhalte erfasst werden sollen.

Eingabeelemente können zum Beispiel sein:

- ein oder mehrere Textfelder
- Elemente für die Auswahl von Dateien aus dem Medienpool
- Elemente für die Auswahl von Links
- Auswahlelemente (Selectfelder)

In einen Artikel eingesetzte Modulblöcke bilden die Slices, aus denen sich der gesamte Inhalt einer Seite zusammensetzt.

Ein Slice hat einen vordefinierten Satz an Variablen, der für die Benutzerelemente zur Verfügung stehen. Diese Variablen werden über eine eigene Syntax angesprochen. Variablen werden ausführlich im Kapitel [[[redaxo-variablen]]] beschrieben.


## Modulerstellung für Entwickler

Ein Modul wird im Backend im Bereich `Module` erstellt. Die Benennung des Modules kann frei gewählt werden. Da die Reihenfolge der Module in der Auswahlliste nach Namen sortiert wird, sind die Namen für eine gewisse Struktur relevant.

### Input

Im Eingabeteil werden die Felder definiert, die der Redakteur bei der Eingabe der Inhalte sieht. Der Eingabeteil kann individuell gestaltet werden und mit beliebigem HTML Code formatiert werden. Der Eingabeteil kann aus PHP Code und HTML bestehen. Alle Klassen des Frameworks (Core, AddOns) stehen zur Verfügung.

### Output

Der Ausgabecode wird von REDAXO ausgeführt und im Frontend ausgegeben. Auch hier stehen alle Klassen und Funktionen des Frameworks zur Verfügung.

PHP Variablen, die in einem Modul definiert wurden, stehen in den folgenden Slices zur Verfügung. So kann beispielsweise die Anzahl der Module auf einer Seite gezählt werden.

### Aktionen

Siehe Kapitel [[[aktionen]]]

## Verwaltung von Modulen für Administratoren und Redakteure

### Beschränkung von Modulen für Templates und C-Types

Der Administrator kann die Verwendung von Modulen für Benutzergruppen und Templates einschränken. In jedem Template lässt sich einstellen, ob bestimmte Module für bestimmte C-Types (Spalten) zur Verfügung stehen oder nicht. Auch für Benutzergruppen (Rollen) lässt sich einstellen, ob alle Module verfügbar sein sollen oder nur ausgewählte Module. Dadurch lässt sich die Übersicht bei der Modulauswahl verbessern. Auch lässt sich durch eine definierte Verfügbarkeit die fälschliche Verwendung von Inhaltsmodulen vermeiden. Wenn ein Modul erstellt wurde, welches nur in der Seitenspalte einer Seite verwendet werden soll, so kann es bei korrekter Einstellung nicht in der Hauptspalte eingesetzt werden.

### Ein Modul als Inhaltsblock einsetzen

REDAXO Artikel sind, wenn sie erstellt werden, zunächst leer. Über die Dropdownliste `Block hinzufügen` lässt sich ein neuer Inhaltsblock in den Artikel einsetzen. Es erscheint dann die Inhaltsmaske, die im Modul Input definiert wurde. Ein Block lässt sich vor oder hinter einem vorhandenen Block einfügen.

### Einen Slice verschieben

Die eingesetzten Modulblöcke lassen sich bei Bedarf über die Pfeile nach oben oder unten verschieben und dadurch in ihrer Reihenfolge verändern.

## Beispiele

### Einaches Textmodul

**Eingabe**:

```
<label>Überschrift</label>
<input type="text" name="REX_INPUT_VALUE[1]" value="REX_VALUE[1]">

<label>Introtext</label>
<textarea rows="6" name="REX_INPUT_VALUE[2]">REX_VALUE[2]</textarea>
```

Auch wenn die Eingabe der Inhalte so bereits funktioniert, so sieht das noch nicht so hübsch aus. Um die Optik auch für den Redakteur etwas ansehnlicher zu gestalten, könnte man die Bootstrap-CSS-Klassen für das Styling verwenden:

**Optisch gestylte Eingabe**:

```
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

```
<div class="jumbotron">
    REX_VALUE[id='1' prefix='<h1>' suffix='</h1>']
    REX_VALUE[id='2' prefix='<p>' suffix='</p>']
</div>
```

### Bildmodul

**Eingabe**:

```
<label>Bild 1</label>
REX_MEDIA[id="1" widget="1"]

<label>Bild 2</label>
REX_MEDIA[id="2" widget="1"]

<label>Galerie</label>
REX_MEDIALIST[id="1" widget="1"]

```

Auch dieses Modul lassen sich die Felder noch etwas hübscher darstellen.

**Optisch gestylte Eingabe**:

```
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

```
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
    <?php
    foreach (explode(',', "REX_MEDIALIST[1]") as $img)
    {
        echo '<div class="col-lg-6">';
        echo '<img class="img-responsive" src="'.rex_url::base('media/'.$img).'">';
        echo '</div>';
    }
    ?>

</div>
```

### Inhaltsübersicht für Artikel

Dieses Modul listet alle Artikel innerhalb einer Kategorie auf, die den Status `online` haben und nicht der Startartikel sind.
Die Einträge werden in der Überschrift verlinkt, als Beschreibung wird der Text ausgegeben, der in den Metadaten des Artikels im Feld `Beschreibung` eingetragen ist.
Dieser Code kann als Basis für Artikelteaser verwendet werden.

**Eingabe**

-- keine --

**Ausgabe**
```
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

## Hinweise

Wenn ein Modulblock in einem Artikel neu hinzugefügt wird, so ist die Slice Id noch nicht vergeben. Daher können dem Slice beim einfügen auch keine Aktionen zugewiesen werden.
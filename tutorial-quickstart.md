# Quickstart: Website in 15 Minuten

- [Voraussetzung](#voraussetzung)
- [Template](#template)
- [Basis](#basis)
- [Navigation](#navigation)
- [Ausgabe der Inhalte vorbereiten](#ausgabe)
- [Module](#module)
    - [Intro-Modul](#intro-modul)
    - [Zwei-Spalten-Modul](#zwei-spalten-modul)

<a name="voraussetzung"></a>
## Vorausetzung

REDAXO muss bereits [installiert](/{{path}}/{{version}}/installation) sein.

<a name="template"></a>
## Template

Dieses Tutorial zeigt das Zusammenspiel von Templates und Modulen, und wie daraus in wenigen Minuten eine einfache Mini-Website entsteht. Eine detaillierte Erläuterung der verwendeten Funktionen findet sich in späteren Kapiteln der Dokumentation. Hier soll nur gezeigt werden, wie rasch man eine minimale Website erstellen kann.

Zum Einsatz kommt ein einfaches Grundgerüst des Bootstrap-Frameworks. Das Basis HTML-Gerüst sieht zunächst so aus:

```
<!DOCTYPE html>
<html lang="de">
<head>
	<meta charset="utf-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1">

	<title>Einfaches Basis-Template</title>

	<!-- Load Bootstrap core CSS & Jumbotron Example -->
	<link href="https://getbootstrap.com/dist/css/bootstrap.min.css" rel="stylesheet">
	<link href="https://getbootstrap.com/examples/jumbotron-narrow/jumbotron-narrow.css" rel="stylesheet">
</head>

<body>

	<div class="container">
    Hier kommt dann der Inhalt ...

    <footer class="footer">
        <p>&copy; 2016 Company, Inc.</p>
    </footer>

	</div> <!-- /container -->

</body>
</html>
```

Die CSS-Datei wird in diesem Beispiel direkt von der Bootstrap-Website geladen, wird jedoch im Normalfall auf dem eigenen Server liegen. Noch gibt es im Template keine dynamischen, von REDAXO gesteuerten Inhalte.

<a name="basis"></a>
## Basis-Einstellungen

Im ersten Schritt wird also der Artikelname dynamisch als Title-tag gesetzt. Hier kommen PHP und REDAXO-eigene Aufrufe ins Spiel; diese werden wie gesagt in der Dokumentation alle ausführlich erläutert.
Am besten verwendet man den Artikelnamen als Title-Tag und wandelt Sonderzeichen in entsprechende HTML-Codes um:

```
<title><?php echo htmlspecialchars($this->getValue('name')); ?></title>
```

Nun soll noch im Footer der Website-Name integriert werden, den im REDAXO-Menü `System' hinterlegten  mit der aktuellen Jahreszahl anzeigen:

```
<footer class="footer">
	<p>&copy; <?php echo date("Y").' '.rex::getServerName(); ?></p>
</footer>
```

<a name="navigation"></a>
## Navigation

Die Standard-Navigation von Bootstrap sieht so aus:

```
<div class="header clearfix">
    <nav>
        <ul class="nav nav-pills pull-right">
            <li><a href="">Menüpunkt</a></li>
            <li><a href="">Menüpunkt</a></li>
        </ul>
    </nav>
    <h3 class="text-muted">Website-Name</h3>
</div>
```

Es gilt also, die Navigation dynamisch auszulesen und den Website-Namen dynamisch einzusetzen. Am Code müssen dafür nur wenige Zeilen ergänzt werden:

```
<div class="header clearfix">
    <nav>
        <ul class="nav nav-pills pull-right">
            <?php
            foreach (rex_category::getRootCategories(true) as $item) {
                echo '
                <li><a href="'.$item->getUrl().'">'.htmlspecialchars($item->getValue('name')).'</a>';
}
            ?>
        </ul>
    </nav>
    <h3 class="text-muted"><?php echo rex::getServerName(); ?></h3>
</div>
```

<a name="ausgabe"></a>
## Ausgabe der Inhalte vorbereiten

Bevor nun im nächsten Schritt zwei einfache Module erstellt werden, muss man im Template noch den Aufruf einfügen, damit der Inhalt der Module auch ausgegeben wird:

```
REX_ARTICLE[]
```
Das ist alles :-)

Das komplette Template sieht also nun so aus:

```
<!DOCTYPE html>
<html lang="de">
<head>
	<meta charset="utf-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1">

	<title><?php echo htmlspecialchars($this->getValue('name')); ?></title>

	<!-- Load Bootstrap core CSS -->
	<link href="https://getbootstrap.com/dist/css/bootstrap.min.css" rel="stylesheet">
</head>

<body>

    <div class="container">

    <div class="header clearfix">
        <nav>
            <ul class="nav nav-pills pull-right">
                <?php
                foreach (rex_category::getRootCategories(true) as $item) {
                    echo '<li><a href="'.$item->getUrl().'">'.htmlspecialchars($item->getValue('name')).'</a></li>';
                }
                ?>
            </ul>
        </nav>
        <h3 class="text-muted"><?php echo rex::getServerName(); ?></h3>
    </div>

    REX_ARTICLE[]

    <footer class="footer">
        <p>&copy; <?php echo date("Y").' '.rex::getServerName(); ?></p>
    </footer>

	</div> <!-- /container -->

</body>
</html>
```

Nun wird dieser Code in das bei der Installation standardmäßig angelegte Template eingefügt: Menüpunkt `Templates` anklicken, dann das Template `Default`, den Code hinein kopieren und das Template speichern.

<a name="module"></a>
## Module

Wenn man nun Kategorien in Redaxo neu hinzufügt, sehen diese durch das Basis-Template schon ganz ansehnlich aus. Es fehlen noch Inhalte. Die werden durch Module eingepflegt, die man in jedem Artikel in beliebiger Anzahl aneinander reihen kann.

<a name="intro-modul"></a>
### Intro-Modul

Als Erstes wird ein Intro-Modul mit einer großen Überschrift und einem Absatz erstellt. Beim Menüpunkt "Module" kann dieses erste Modul neu angelegt werden. 

Im Eingabe-Code - das ist das, was der Redakteur in REDAXO sieht - benötigt man also zwei Felder, ein Textfeld und ein Textarea-Feld für mehrzeiligen Text. Jedes Feld muss eine eigene Value-ID besitzen.

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

Damit ist das erste Modul erstellt und einsatzbereit.

<a name="zwei-spalten-modul"></a>
### Zwei-Spalten-Modul

Ein zweites Modul dient zur Anzeige von Bildern und Texten in zwei Spalten.

**Eingabe**:

```
<h2>Spalte 1</h2>

<label>Überschrift</label>
<input type="text" name="REX_INPUT_VALUE[1]" value="REX_VALUE[1]">

<label>Bild</label>
REX_MEDIA[id="1" widget="1"]

<label>Introtext</label>
<textarea rows="6" name="REX_INPUT_VALUE[2]">REX_VALUE[2]</textarea>

<h2>Spalte 2</h2>

<label>Bild</label>
REX_MEDIA[id="2" widget="1"]

<label>Überschrift</label>
<input type="text" name="REX_INPUT_VALUE[3]" value="REX_VALUE[3]">

<label>Introtext</label>
<textarea rows="6" name="REX_INPUT_VALUE[4]">REX_VALUE[4]</textarea>
```

Auch dieses Modul lassen sich die Felder noch etwas hübscher darstellen.

**Optisch gestylte Eingabe**:

```
<fieldset class="form-horizontal">
    <legend>Spalte 1</legend>

    <div class="form-group">
        <label class="col-sm-2 control-label">Bild</label>
        <div class="col-sm-10">
            REX_MEDIA[id="1" widget="1"]
        </div>
    </div>

    <div class="form-group">
        <label class="col-sm-2 control-label">Überschrift</label>
        <div class="col-sm-10">
            <input class="form-control" type="text" name="REX_INPUT_VALUE[1]" value="REX_VALUE[1]" />
        </div>
    </div>

    <div class="form-group">
        <label class="col-sm-2 control-label">Text</label>
        <div class="col-sm-10">
            <textarea rows="6" class="form-control" name="REX_INPUT_VALUE[2]">REX_VALUE[2]</textarea>
        </div>
    </div>
</fieldset>

<fieldset class="form-horizontal">
    <legend>Spalte 2</legend>

    <div class="form-group">
        <label class="col-sm-2 control-label">Bild</label>
        <div class="col-sm-10">
            REX_MEDIA[id="2" widget="1"]
        </div>
    </div>

    <div class="form-group">
        <label class="col-sm-2 control-label">Überschrift</label>
        <div class="col-sm-10">
            <input class="form-control" type="text" name="REX_INPUT_VALUE[3]" value="REX_VALUE[3]" />
        </div>
    </div>

    <div class="form-group">
        <label class="col-sm-2 control-label">Text</label>
        <div class="col-sm-10">
            <textarea rows="6" class="form-control" name="REX_INPUT_VALUE[4]">REX_VALUE[4]</textarea>
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
        REX_VALUE[id='1' prefix='<h1>' suffix='</h1>']
        REX_VALUE[id='2' prefix='<p>' suffix='</p>']
    </div>

    <div class="col-lg-6">
        <?php
        if ("REX_MEDIA[2]" != '')
        {
            echo '<img class="img-responsive" src="'.rex_url::base('media/REX_MEDIA[2]').'">';
        }
        ?>
        REX_VALUE[id='3' prefix='<h1>' suffix='</h1>']
        REX_VALUE[id='4' prefix='<p>' suffix='</p>']
    </div>
</div>
```

Damit ist die kleine Mini-Website fertig gestellt. Wir haben eine mobiltaugliches Layout, die Navigation funktioniert, und Texte und Bilder können eingepflegt werden. Natürlich lässt sich die Website noch an vielen Stellen ergänzen und optimieren: Die Navigation könnte für mehrere Ebenen erweitert werden, man könnte weitere Inhalts-Module erstellen oder dank zahlreicher AddOns die Funktionen von REDAXO stark erweitern.


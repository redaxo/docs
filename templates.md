# Templates

- [Templates erstellen](#templates_erstellen)
- [Templates verwalten](#templates_verwalten)
- [Navigation](#navigation)
- [Mehrere Artikel einbinden](#artikel_einbinden)
- [Includes](#includes)
- [Metadaten / Sonstiges](#metadaten_sonstiges)

<a name="templates_erstellen"></a>
## Templates erstellen

In diesem Kapitel finden Sie eine Anleitung, wie man ein Template erstellen kann. Im einfachsten Fall besteht ein Template aus einer leeren html-Seite und einer Referenz auf den aktuellen Artikel.

Im folgenden Beispiel sind bereits REDAXO-spezifische Elemente eingebaut, so zum Beispiel zum Einfügen artikelspezifischer Metadaten. Dies wird in den folgenden Kapiteln noch näher erläutert.

Dieses Beispiel kann beliebig variiert werden. Das Layout wird in einem Template üblicherweise detaillierter definiert. So können hier unterschiedliche Seitenbereiche, zum Beispiel Kopf- und Fußzeilen, oder mehrere Spalten formatiert und die Navigation eingebunden werden.

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"	"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="de" lang="de">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1"/>
<title><?php print $REX['SERVERNAME'].' | '.htmlspecialchars($this->getValue("name")); ?></title>
<meta name="keywords" content="<?php print htmlspecialchars($this->getValue("art_keywords")); ?>" />
<meta name="description" content="<?php print htmlspecialchars($this->getValue("art_description")); ?>" />

<link rel="stylesheet" type="text/css" href="<?php echo $REX['HTDOCS_PATH'] ?>files/main.css" media="screen" />

</head>
<body >
<?php 
/* hier wird der artikelspezifische Inhalt eingebunden;
$this verweist dabei auf den jeweils aktuellen Artikel */

echo $this->getArticle(); 
?>
</body>
</html>
```


Der artikelspezifische Inhalt wird in einem beliebigen Bereich/Container eingefügt. Es ist auch möglich, die Inhalte mehrerer Artikel in einem Template anzuzeigen. Ebenso ist es möglich, mehrere Spalten im Template anzugeben. So kann neben dem Hauptinhalt zum Beispiel eine weitere Spalte für wichtige Informationen bereitgestellt werden.


<a name="templates_verwalten"></a>
## Templates verwalten

Die Templates werden im REDAXO-Backend unter der Rubrik “Templates” gespeichert.

Hier können neben dem default-Template auch weitere Templates für Navigation und Inhalt angelegt werden. Mit einem Klick auf das Icon mit dem + links im Header der Tabelle wird ein neues Template erstellt. Es wird eine leere Eingabemaske geöffnet.

Beim Klick auf ein vorhandenes Template öffnet sich eine Eingabemaske, um das Template zu editieren.


**Feld "Name"**

Beim Editieren des Templates sollte als erstes die Bezeichnung für das Template im Feld Name eingetragen werden.


**Feld "Aktiv"**


Im Feld “Aktiv” hat man die Möglichkeit, das Template mit dem Status “Aktiv” zu versehen.

Bei aktiviertem Status erscheint das Template in der Templateauswahl bei den Artikeln.


**Feld "Template"**

Im Feld “Template” wird der eigentliche Quellcode für das Template eingetragen.

**Feld "Spalten [ctypes]"**

Spalten ersetzen die CTYPES der Version 3 und machen das Definieren und Bearbeiten unterschiedlicher Inhaltsbereiche einfacher. Sie werden direkt einem Template zugewiesen.

**Template - Spalten**

Unter “Spalten” hat man die Möglichkeit, neben dem Hauptinhalt weitere Spalten für das Platzieren von Inhalten zu erzeugen.

Die Spalten werden ins Template mit ```$ this->getArticles(ID);```eingebunden.
ID ist hier die ID der Spalte.

```
<div class="Container-fuer-den-Hauptinhalt">
<?php print $this->getArticle(1); ?>
</div>

......

<div class="Container-fuer-die-linke-Spalte">
<?php print $this->getArticle(2); ?>
</div>

```
Jedem Artikel kann in den Spalten dieses Templates eigener Inhalt zugewiesen werden. Man findet den Zugriff auf die Spalten im Editiermodus eines Artikels.

Die Inhalte der unterschiedlichen Bereiche werden für diesen Artikel mit der Spalten-ID des jeweiligen Bereiches gespeichert. Beim Aufruf des Artikels werden die Bereiche “Hauptinhalt” und “Linke Spalte” mit den artikelspezifischen Inhalten angezeigt.

***Speichern/Übernehmen***

Mit den Buttons Template Speichern und Template übernehmen werden die Änderungen gepspeichert. Bei “Template speichern” wird das Template gespeichert und die Eingabemaske schließt sich. Bei “Template übernehmen” wird gespeichert und die Eingabemaske bleibt offen.

<a name="navigation"></a>
## Navigation

Es gibt unterschiedliche Möglichkeiten, eine Navigation festzulegen.

**In Templates**

Links auf externe Seiten werden in einem Template in der folgenden Form festgelegt:

```<a href="http://www.redaxo.de">zur REDAXO Hompage</a>```

**In Modulen**

In den Modulen hängt die Schreibweise für einen externen Link davon ab, wie die Ein- und Ausgabe definiert sind, welche REDAXO-Variablen verwendet werden und ob eine automatische Umwandlung bestimmter Signalwörter vorgesehen ist. Hier muss berücksichtigt werden, mit welchem Modul man aktuell arbeitet.

**Interne Links, manuell definiert**

Soll in einem Template auf interne Seiten verlinkt werden, wird die gewünschte Artikel-ID als Parameter übergeben.

```<a href="<?php echo rex_getUrl(22) ?>">Interner Link Artikel 22</a>```

Mit dieser Schreibweise funktionieren die Links auch, wenn RexRewrite aktiv ist. Für erweiterte Mod-Rewrite-Features steht das Url-Rewrite Addon zur Verfügung.

**Interne Links, dynamisch erzeugt**

Statt einer manuell erzeugten Navigation kann man diese auch dynamisch erstellen lassen. Dazu bieten sich mehrere Möglichkeiten an. Man kann sowohl das OO-Konzept von Redaxo nutzen als auch die Struktur mit Hilfe von SQL-Befehlen ermitteln und darstellen.

Im Downloadbereich findet man bei den Templates einige Beispiele für Navigationen. Diese Navigationen werden als neues Template angelegt und im default-Template eingefügt. Am Anfang des default-Templates wird die Template-ID der Navigation festgelegt.

```
// Allgemeine Navigation
$navTemplateId = "3";
```

Neben einer Navigation kann man auch zwei oder mehrere Navigationen einbinden.

Beispiel für diese Nutzung wäre, dass auf der Startseite eine horizontale Navigation angezeigt wird und auf den Inhaltsseiten eine Doppelnavigation. Wobei die Hauptnavigation horizontal und die Subnavigation vertikal verteilt wird.

```
// Navigation Startseite im vertikalen Block

if ($REX['START_ARTICLE_ID'] == $this->getValue("article_id")) {
$navTemplateId = "3";
} // Navigation Inhaltsseiten horizontal / vertikale	
else {
$navTemplateId = "2";
}
```
Das Einfügen (includen) des Navigation Template geschieht wie folgt.

```
$navTemplate = new rex_template($navTemplateId);	
include $navTemplate->getFile();
```

Oder mittels REDAXO-Variable:

```
REX_TEMPLATE[2]
```

Ab dieser Stelle hat man die Möglichkeit, auf die Variablen des Navigation Templates zuzugreifen.
Beispiel für das Einbinden der Variablen $ navLeftCol. In dieser wird im Navigationstemplate die Navigation reingeschrieben.

```
<?php print $navLeftCol; ?>
```

Das Template sieht an dieser Stelle dann wie folgt aus:

```
<?php
// Notices ausschalten
// error_reporting(E_ALL ^ E_NOTICE); 

// Allgemeine Navigation

$navTemplateId = "3";
//	Code

$article = OOArticle::getArticleById($REX['START_ARTICLE_ID'], $REX['CUR_CLANG']);
$articleK = $article->getValue("_keywords");
$articleD = $article->getDescription();

// Einbinden des Navigation Template
$navTemplate = new rex_template($navTemplateId);	
include $navTemplate->getFile();

if($this->getValue("description") != "") {
$meta_beschreibung = htmlspecialchars($this->getValue("description"));
} else {
$meta_beschreibung = htmlspecialchars($articleD);
}
if($this->getValue("keywords")!= "") {
$meta_suchbegriffe = htmlspecialchars($this->getValue("keywords"));
} else {
$meta_suchbegriffe = htmlspecialchars($articleK);
} 
?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="de" lang="de">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1"/>
<title><?php print $REX['SERVERNAME'].' | '.$this->getValue("name"); ?></title>
<meta name="keywords" content="<?php print $meta_suchbegriffe; ?>" />
<meta name="description" content="<?php print $meta_beschreibung; ?>" />

<link rel="stylesheet" type="text/css" href="<?php echo $REX['HTDOCS_PATH'] ?>files/main.css" media="screen" />
?>
</head>
<body >
<div id="site-content">
<div id="content">
<div id="main-content">
<div id="nav">
<?
/* hier wird die Navigation eingebunden; */
print $navLeftCol;
?>
</div>
<div id="main">
<? print $this->getArticle(1); ?>
</div>
</div>
</div>
</body>
</html>
```

**Sitemap, dynamisch generieren**

Nach dem gleichen Prinzip kann man eine Sitemap dynamisch generieren lassen. Das hat den Vorteil, dass die Sitemap bei Änderungen an der Kategorie- oder Artikelstruktur automatisch aktualisiert wird.


<a name="artikel_einbinden"></a>
## Mehrere Artikel einbinden

**Ab Version 4.2**

Der Inhalt des aktuell aufgerufenen Artikels wird durch Aufruf Redaxo-Konstante Variable REX_ARTICLE[] eingefügt.

Es können darüber hinaus Inhalte beliebiger weiterer Artikel eingefügt werden. Dies geschieht, indem ein neuer Artikel deklariert und diesem eine bestimmte Artikel-ID zugewiesen wird. Die ID gehört zu dem Artikel, dessen Inhalt hier angezeigt werden soll. Er muss in der Struktur definiert sein. In diesem Artikel können Inhalte gespeichert werden, die auf mehreren Seiten angezeigt werden sollen, zum Beispiel die Navigation oder eine News-Liste.

Der Inhalt wird ebenfalls durch Aufruf der Konstanten REX_ARTICLE[] eingefügt.

Es ist möglich, einen zusätzlichen Artikel mehrfach in eine Seite einzubinden oder mehrere unterschiedliche Artikel innerhalb einer Seite einzubinden.

Das folgende Listing soll das das Prinzip erläutern.

```
<!-- einfügen des Inhalts des aktuellen Artikels -->

<div>REX_ARTICLE[]</div>

<!-- hier wird ein weiterer Artikel eingebunden -->

<div>REX_ARTICLE[id=2]</div>



<!-- weitere Möglichkeiten der Parameter-Übergabe -->

REX_ARTICLE[ctype=2]

REX_ARTICLE[id=1 ctype=2]

REX_ARTICLE[id=1 field="name"]
```

**Weitere Parameter ab Version 4.3**

Ab Version 4.3 kann auf die Parameter ifempty und instead zurückgegriffen werden. Diese ermöglichen es einen alternativen Artikel einzubinden, falls der ausgewählte bspw. nicht vorhanden ist.

```
REX_ARTICLE[id=1 field="name" ifempty="Leer"]

REX_ARTICLE[id=1 field="name" instead="Stattdessen das hier"]
```

**Vor Version 4.2**

Der Inhalt des aktuell aufgerufenen Artikels wird durch Aufruf der Funktion $this->getArticle() eingefügt.

Es besteht die Möglichkeit, einen zusätzlichen Artikel mehrfach in eine Seite einzubinden oder mehrere unterschiedliche Artikel innerhalb einer Seite einzubinden.

Der Inhalt wird ebenfalls durch Aufruf der Funktion $artikel_2->getArticle() eingefügt.

Das folgende Listing soll das das Prinzip erläutern.

```
<?php
/* hier wird der Inhalt eingefügt, der zu dem aktuellen Artikel gehört */

echo "<div>".$this->getArticle()."</div>";


/* hier wird ein weiterer Artikel eingebunden */

$artikel_2 = new rex_article;
$artikel_2->setCLang($REX['CUR_CLANG']);
$artikel_2->setArticleID(123);

echo "<div>".$artikel_2->getArticle()."</div>";

?>
```

<a name="includes"></a>
## Includes

**Einbinden von Templates**

Wie in der Demo gezeigt, ist es möglich, zusätzliche Templates, die Sie in REDAXO erstellt haben, in das default-Template oder auch innerhalb eines einzelnen Artikels einzulesen.

Ein Beispiel für den Einsatz ist das Auslagern einer Navigation in ein Template. Durch die separate Ablage des Codes wird das Template übersichtlicher. Das Layout kann dadurch leichter bearbeitet werden.

```
<?php
// innerhalb von PHP Tags
$navTemplate = new rex_template(2);
include $navTemplate->getFile();
?>


// ausserhalb von PHP Tags
REX_TEMPLATE[2]
```

**Einbinden von php-Code in einer Textdatei**

Es besteht auch die Möglichkeit, Programmcode in einer separaten Text-Datei auszulagern und diesen dann mittels include()-Befehl an einer bestimmten Stelle in ein Template einzufügen.

Die include-Datei kann beliebigen php-Code enthalten. Sinnvollerweise sollte sie in dem für includes vorgesehen Ordner redaxo/include gespeichert werden. Wenn sie in einem anderen Ordner abgelegt wird, muss bei dem include-Befehl die Pfadangabe entsprechen angepasst werden. Nach einer allgemeinen Übereinkunft werden include-Dateien mit der Endung .inc.php gespeichert.

Ein einfaches Beispiel:

```
<div>
<?php
// hier wird der ausgelagerte Code eingelesen\
include($REX['INCLUDE_PATH'].'/externerCode.inc.php');
?>
</div>


<div>
<?php
// hier wird der Seiten-Inhalt eingelesen
$this->getArticle();
?>
</div>
```

<a name="metadaten_sonstiges"></a>
## Metadaten / Sonstiges

**Allgemein**

REDAXO bietet die Möglichkeit, für jeden Artikel spezifische Meta-Angaben zu definieren und auszugeben. Dadurch können die Seiten zum Beispiel von Suchmaschinen gezielter gefunden werden oder man kann jeder Seite ein eigenes Bild und einen kurzen Text als Header zuweisen.

Die Festlegung dieser Meta-Informationen erfolgt in der Einzelansicht des Artikels. Der gewünschte Artikel wird ausgewählt und die Bearbeitungsmaske “Metadaten/Sonstiges” aufgerufen.

**Online vom - bis zum**

Es besteht die Möglichkeit, hier einen Zeitrahmen vorzugeben, innerhalb dessen der Artikel online sein soll.

**Seitenspezifische Metatags**

Die Felder “Name/Bezeichnung”, “Beschreibung” und “Suchbegriffe” können genutzt werden, um seitenspezifische Metatags in einen Artikel einzufügen. Diese Felder können aber genausogut für Ausgaben im Frontend genutzt werden.

Zum Aufrufen dieser Informationen werden in dem Template folgende Befehle eingefügt

```
// Titel
<title><?php echo $this->getValue("name"); ?></title>

// Beschreibung
<meta name="description" content="<?php echo $this->getValue("description"); ?>" />

// Suchworte
<meta name="keywords" content="<?php echo $this->getValue("keywords"); ?>" />
```

**Seitenspezifische Bilder**

Dem Artikel kann hier ein spezielles Bild zugewiesen werden.

Der Aufruf dieses Bildes zum Artikel erfolgt über den Befehl

```
$this->getValue("file")
```

So kann man das Bild in einem Template/Modul anzeigen lassen

```
<img src="files/<?php echo $this->getValue("file"); ?>" />
```

Hier wird angenommen, dass sich die Bilder im Medienpool, das heißt im Ordner files, befinden.

**Teaser**

Der Artikel kann durch Selektion des Feldes “Teaser” als Teaser gekennzeichnet werden. In der Datenbank wird in der Tabelle rex_article der Wert für die Spalte “Teaser” auf 1 gesetzt und kann so über ein entsprechendes Modul selektiert werden.

Den Wert erhält man über den Befehl

```
$var = $this->getValue("teaser");
```

**Artikeltyp**

Falls mehr als ein Artikeltyp definiert wurde, kann hier eine Auswahl und Zuweisung eines Typs zum Artikel erfolgen.

####Sonstige Funktionen

In Abhängigkeit von den Berechtigungen eines Benutzers, erhält dieser weitere Funktionen angezeigt. Hierzu muss man entweder als Admin eingeloggt sein oder man muss ein User sein, dem entsprechende Rechte bei der Rechtevergabe eingeräumt wurden.

**Artikel: Diese Kategorie in einen Artikel umwandeln**

Hierbei wird die Kategorie aufgelöst und aus dem Startartikel, wird auf der vorhergehenden Ebene, ein normaler Artikel. Die Kategorie existiert danach nicht mehr. Die Umwandlung ist nur möglich, wenn keine weiteren Artikel oder Kategorien in dieser Kategorie existieren.

**Kategorie: Diesen Artikel in eine Kategorie umwandeln**

Artikel, die keine Startartikel sind, können zu einer Kategorie umgewandelt werden. Hier wird dann statt“Diese Kategorie in einen Artikel umwandeln” die Option “Diesen Artikel in eine Kategorie umwandeln” angezeigt.


**Inhalte kopieren: Inhalte von einer Sprache in eine andere kopieren**

Hat der Benutzer die Berechtigung “copyContent” und sind mehrere Sprachen eingerichtet, so bekommt er hier die Möglichkeit angezeigt, Inhalte eines Artikels von einer Sprache in eine andere zu kopieren. Dies ist nützlich, wenn die Module eines Artikels zur Übersetzung in eine andere Sprache kopiert werden sollen.

**Artikel kopieren**

Benutzer mit der Berechtigung “copyArticle” haben hier die Möglichkeit, einen Artikel in eine andere Kategorie zu kopieren. Die Kategorien werden hier zur Auswahl angezeigt.

**moveCategory (nur Startartikel): Kategorie verschieben**

Benutzer mit der Berechtigung “moveCategory” können komplette Kategorien verschieben. Dies geschieht durch Verschieben des Startartikels dieser Kategorie. Die Kategorie wird dann mit allen Artikeln und Unterkategorien verschoben.

**moveArticle ("normale" Artikel): Artikel verschieben**

Artikel, die keine Startartikel sind, können einzeln in eine andere Kategorie verschoben werden. Hier wird dann statt “Kategorie verschieben” die Option “Artikel verschieben” angezeigt.




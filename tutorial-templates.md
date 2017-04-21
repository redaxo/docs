# Templates nutzen
In REDAXO sind selbstverständlich die Inhalte konsequent vom Layout getrennt. Dieses Tutorial nutzt die Standard-REDAXO-Demo dazu, das Templatesystem zu beleuchten und das vorgegebene Demo-Layout zu erweitern.

## Ziel des Tutorials

Um das Templatesystem besser zu verstehen, sollte man das Template der REDAXO-Demo analysieren und dann schrittweise modifizieren. Als Übung soll das Default-Template in drei Teile aufgeteilt werden (Header, Content und Footer). Danach wird ein neues Template angelegt, das diese drei Templateteile inkludiert. Das neue Template soll ein Zweispalten-Template werden, wobei man statt Spalten natürlich ebenso andere Contentbereiche wie Header, Footer, etc. steuern könnte. In REDAXO verwendet man Ctypes zur Verwaltung dieser Contentbereiche.

## Voraussetzung

Es muss ein funktionsfähiger Server zur Verfügung stehen, auf dem REDAXO fehlerfrei installiert und die Standard-Demo importiert wurde.

## Erste Schritte

Nach dem Import der Demo sollte man sich zunächst die Templates anschauen – dieses Tutorial betrachtet vor allem das Template “default”.
In der Basis Navigation findet sich an dritter Stelle der Punkt “Templates”. Dort existieren drei vorinstallierte Templates:

id=1	default	aktiv – ja
id=2	Navigation: Breadcrumb	aktiv – nein
id=3	Navigation: Links	aktiv – nein

## Default Template

Im Template sind alle wesentlichen HTML-Tags enthalten, begonnen vom der Doctype-Deklaration über die Meta-Daten bis zum schließenden body-Tag. Zu Beginn fällt vor allem der eingebettete PHP-Code auf, der verschiedene Zwecke erfüllt.


```<?php

// ------ DESCRIPTION/KEYWORDS
$OOStartArticle = OOArticle::getArticleById($REX['START_ARTICLE_ID'], $REX['CUR_CLANG']);
$meta_beschreibung = $OOStartArticle->getValue("art_description");
$meta_suchbegriffe = $OOStartArticle->getValue("art_keywords");

if($this->getValue("art_description") != "")
$meta_beschreibung = $this->getValue("art_description");

if($this->getValue("art_keywords") != "")
$meta_suchbegriffe = $this->getValue("art_keywords");


?>

```

OOArticle::getArticleById($REX['START_ARTICLE_ID'], $REX['CUR_CLANG']); steuert über das Objektorientierte Framework den Startartikel an – das Ziel ist, Metadaten wie “description” und “keywords” in den entsprechenden HTML-Metatags auszugeben.

Die nachfolgenden if-Anweisungen überschreiben die jeweilige Variable mit den Daten des aktuellen Artikels – sofern diese eingegeben wurden.

Im Header wird außerdem der Artikelname der jeweiligen Seite im <title>-Tag ausgegeben:


```<title><?php print $REX['SERVERNAME'].' | '.$this->getValue("name"); ?></title>
```

`$REX['SERVERNAME']` gibt den bei der Installation festgelegten Website-Namen aus, und `$this->getValue("name"); `liest den Artikelnamen des jeweiligen Artikel aus. Der Titel der Startseite könnte dann etwa wie folgt aussehen: “REDAXO | Startseite”

Man kann im Folgenden sehen, wie die oben definierten Variablen für description und keywords im HTML-Code eingesetzt werden.


```<meta name="keywords" content="<?php print htmlspecialchars($meta_suchbegriffe); ?>" />
<meta name="description" content="<?php print htmlspecialchars($meta_beschreibung); ?>" />
```

Beim weiteren Studium des Templates fallen einige interessante Zeilen auf – im DIV “Content” wird zunächst die Brotkrümelnavigation, dann die Hauptnavigation und die schließlich Artikelausgabe eingebunden.


```<div id="content">

<div id="main-content">

<div id="nav">
REX_TEMPLATE[2]
<p class="copy">&copy; by <a href="http://www.redaxo.de">REDAXO</a></p>
</div>

<div id="main">
<div id="main-block">
<div id="main-teaser">
Slogan: Einfach, flexibel, sinnvoll
</div>

<div id="main-content-block">
REX_TEMPLATE[3]
REX_ARTICLE[]
</div>
</div>
</div>
<br class="clear" />

</div>

</div>
```

Ähnlich wie Redaxo-Module bestimmte REX_VALUE[] ausgeben können ist es auch möglich, in Redaxo-Templates weitere Templates zu inkludieren. Im Beispiel-Code gibt REX_TEMPLATE[2] das Template mit der ID = 2 “Navigation: Breadcrumb” aus, REX_TEMPLATE[3] entsprechend das Template mit der ID = 3 “Navigation: Links” und REX_ARTICLE[] alle Blöcke aller Ctypes (Spalten) des Artikels.

## Auslagern von Header und Footer als wiederkehrende Elemente

Als nächsten Schritt könnte man ein neues Template anlegen mit dem Namen “header”. Damit dieses Template in der Template-Auswahl eines Artikels nicht erscheint (was sinnlos wäre, da es ja nur ein Subtemplate ist), darf man das Häkchen bei “Aktiv” nicht setzen. Den Quelltext vom Anfang bis zur Zeile <div id="main"> schneidet man nun aus und setzt ihn in das Header-Tempalte ein (Speichern nicht vergessen).

Nun muss man im Default-Template den ausgeschnittenen Code einfach durch REX_TEMPLATE[4] ersetzen: REDAXO gibt dann an dieser Stelle den Header aus. Wichtig: darauf achten, dass die Template-ID mit der Zahl in den Klammern übereinstimmt.

--BILD 1--

Nachdem der Header ausgelagert ist, könnte man nochmals ein neues Template mit dem Namen “footer” anlegen. Auch dieses Template sollte man nicht “aktiv” setzen, damit es in der Template-Auswahl beim Anlegen eines Artikels nicht erscheint. Den Quelltext nach der Zeile <br class="clear" /> bis zum Ende verschiebt man ins Footer-Template. Ähnlich wie auch beim Header wird dann das neue Template mit REX_TEMPLATE[5] inkludiert.

## Zweispalter Template

Wie in der Zielsetzung beschrieben legt man nun das zusätzliche Zweispalter-Template an. Es soll über zwei Spalten verfügen und ebenso wie das Default-Template mit Header und Footer ausgerüstet werden. Dazu muss man nochmals ein neues Template einfügen mit dem Namen “Zweispalter”. Dieses Template muss “Aktiv” sein, damit Redakteure es nutzen können.

Natürlich muss man auch die Content-Spalten (ctypes) anlegen, indem man der ersten Ctype-Spalte einen Namen gibt – zum Beispiel “Hauptspalte” – und das Template abspeichert. Danach existiert ein weiteres Feld, in dem man den Namen für die zweite Spalte eingeben kann – zum Beispiel “Seitenleiste”.

Es bleibt nur noch, die Spalten im Template anzusprechen und deren Inhalt auszugeben. Dies gelingt mit `REX_ARTICLE[ctype=1]` für den Haupt-Spalte und `REX_ARTICLE[ctype=2]` für die Seitenleiste.
Das Zweispalter-Template sieht nun so aus:

BILD 2


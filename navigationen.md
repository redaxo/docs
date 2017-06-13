# Navigationen

- [Navigation-Factory oder eigene Navigationen?](#factory-custom)
- [Navigationen mit der Navigation-Factory](#factory)
    - [Einfache Navigation](#factory-einfach)
    - [Beispiel 2: Sitemap](#factory-sitemap)
    - [Beispiel 3: Breadcrumb](#factory-breadcrumb)
    - [Beispiel 4: Komplexe Navigation](#factory-komplex)
- [Eigene Navigationen](#custom)
    - [Dropdown-Navigation](#custom-dropdown)
        - [Erste Ebene](#custom-erste-ebene)
        - [Zwei oder mehr Ebenen](#custom-mehr-ebenen)
    - [Sidebar-Navigation](custom-sidebar)
    - [Breadcrumb](#custom-breadcrumb)
    - [Artikellisten](#custom-artikellisten)
        - [Artikel-Teaser für Unterkategorien](#custom-teaser)
        - [Alle Artikel in einer Kategorie auflisten](#custom-artikel-kategorie)
    - [Blätter-Navigation für Artikel](#custom-blaetter)
    - [Onepage-Navigation](#custom-onepage)
        - [Onepage-Navigation mit Artikeln](#custom-onepage-artikel)
        - [Onepage-Navigation mit Modulen](#custom-onepage-module)

<a name="factory-custom"></a>
## Navigation-Factory oder eigene Navigationen?

REDAXO bietet mit der `rex_navigation::factory()` die Möglichkeit, verschiedenste Seitennavigationen zu erstellen. Sie ist dafür gedacht, mit sehr wenigen Code-Zeilen Navigationen zu erstellen, hat deswegen aber natürlich gewisse Grenzen. Indem man alle zur Verfügung stehende Methoden nutzt oder die `rex_navigation::factory()` mit eigenen Funktionen erweitert, kann man die allermeisten Navigationen damit umsetzen. Um aber wirklich individuelle Navigationen zu erzeugen oder den HTML-Output vollständig zu kontrollieren, kann man auch komplett eigene Navigationen programmieren.

<a name="factory"></a>
## Navigationen mit der Navigation-Factory

Die Navigation-Factory ist Teil des Structure-Addons und befindet sich in `redaxo/src/addons/structure/lib/navigation.php`. Der Code ist gut dokumentiert, so dass es sinnvoll ist, dort nachzuschauen, wenn z. B. Parameter nicht bekannt sind oder man die Funktionalität näher betrachten möchte.

Das [Beispiel 4](#factory-komplex) verwendet alle aktuell verfügbaren Methoden der Factory, um eine sehr umfangreiche Navigation zu erstellen. Beachte die Kommentare im Code, sie erklären die einzelnen Methoden und ihre Parameter.

<a name="factory-einfach"></a>
### Einfache Navigation

```php
$nav = rex_navigation::factory();
$nav->show();
```

Werden keine Parameter angegeben, startet die Navigation mit der Wurzelkategorie, durchläuft bis zu 3 Ebenen, zeigt nur den aktuellen Zweig geöffnet und berücksichtigt auch Offline-Artikel. Die möglichen Parameter werden im nächsten Sitemap-Beispiel erklärt, können aber natürlich ebenso in der "normalen" Navigation genutzt werden.

<a name="factory-sitemap"></a>
### Sitemap

```php
$nav = rex_navigation::factory();
$nav->show(0, -1, TRUE, TRUE);
```

Mit dem ersten Parameter – hier “0” – definiert man, an welcher Stelle die Navigation startet. Man kann hier die ID der gewünschten Kategorie eintragen; mit "0" beginnt die Navigation in der obersten Ebene.
Der zweite Parameter legt die Anzahl der Ebenen fest: "-1" bedeutet, dass alle Ebenen ausgegeben werden. Ansonsten wird hier die Anzahl der gewünschten Ebenen eingetragen. Ein häufiger Wert ist 2 oder 3.
Mit dem dritten Parameter legt man fest, ob alle oder nur die aktiven Kategorien ausgegeben werden. "FALSE" erzeugt quasi eine Sitemap mit allen Kategorien, "TRUE" eine "normale" Navigation: Unterkategorien werden dann nur angezeigt, wenn man sich in der jeweiligen Hauptkategorie befindet.
Der vierte Parameter definiert, ob nur Artikel angezeigt werden, die online sind ("TRUE”") oder auch Offline-Artikel ("FALSE").

Um eine Sitemap zu erzeugen, müssen alle Ebenen durchlaufen (2. Parameter: `-1`) und alle Zweige geöffnet angezeigt werden (3. Parameter: `TRUE`). In diesem Beispiel werden Offline-Artikel nicht angezeigt (4. Parameter: `TRUE`).
 
<a name="factory-breadcrumb"></a>
### Breadcrumbs

Für die Ausgabe von Breadcrumbs gibt es die separate Methode `showBreadcrumb`.

```php
$nav = rex_navigation::factory();
$nav->showBreadcrumb();
```

Auch hier gibt es wieder Parameter, um die Ausgabe zu beeinflussen.

```php
$nav = rex_navigation::factory();
$nav->showBreadcrumb(true, true, 3);
```

Der erste Parameter bestimmt, ob die Startseite auch im Breadcrumb erscheinen soll. Der zweite Parameter steuert, ob der aktuelle Artikel auch im Breadcrumb berücksichtig wird, dies kommt vor allem bei Artikeln zum Tragen, die kein Startartikel sind. Über den letzten Parameter kann gezielt man die Artikel-ID definieren, wo der Breadcrumb starten soll.


<a name="factory-komplex"></a>
### Komplexe Navigation

Man beachte die Kommentare im Code, sie erklären die einzelnen Methoden und ihre Parameter.

```php
$nav = rex_navigation::factory();

// Füge eigene Klassen den Listenelementen (<li>) hinzu
$nav->setClasses(array('level-1', 'level-2', 'level-3'));

// Füge eigene Klassen den Links (<a>) hinzu
$nav->setLinkClasses(array('link-1', 'link-2', 'link-3'));

// Filter: Schließe einzelne Artikel oder Kategorien von der Navigation aus
$nav->addFilter('id', 6, '!=', '');
$nav->addFilter('id', 13, '!=', '');

// Filter: Schließe einzelne Artikel oder Kategorien von der Navigation aus (mittels RegExp)
$ignoreArticles = array(6, 13, 16, 127);
$nav->addFilter('id', '/^(?!(' . implode('|', $ignoreArticles) . ')$)\d+/', 'regex', '');

// Beispiele für Callbacks
$nav->addCallback(function (rex_category $category, $depth, &$li, &$a) {

    // Ergänze eigene Klasse, wenn ein Listenelement über Kindelemente verfügt
    if ($category->getChildren(true)) {
        $li['class'][] = 'item-has-children';
    }

    // Ergänze data-Attribute für <li> und <a>
    $li['data-foo'][] = 'foo';
    $a['data-bar'][] = 'bar';

    return true;
});
    
// Generiere Navigation
// Parameter:
// 1. ID der Wurzelkategorie (Standard: 0)
// 2. Anzahl der Ebenen die angezeigt werden sollen (Standard: 3. -1 bedeutet beliebig viele Ebenen.)
// 3. Zeige den gesamten Baum (Standard: FALSE, zeige also nur den aktiven Zweig)
// 4. Zeige Offline-Elemente (Standard: FALSE, Offline-Elemente werden also angezeigt)
$navHtml = $nav->get(0, -1, TRUE, TRUE);

// Ersetze REDAXO-Klassen durch eigene
$navHtml = str_replace(
    array('rex-current', 'rex-active'),
    array('my-current', 'my-active'),
    $navHtml);

// Gebe die Navigation aus
echo $navHtml;
```

<a name="custom"></a>
## Eigene Navigationen

Benötigt man Navigationsvarianten, die Navigation Factory nicht darstellen kann (und ist doch dort der Fall) oder will man z.B. ein spezielles HTML-Markup, sollte man eigene Navigation erstellen. Letztlich sind auf diesem Weg alle Navigationsvarianten, und nach einer kurzen Eingewöhnungszeit wird man diese Herangehensweise nicht mehr als schwer empfinden.

<a name="custom-dropdown"></a>
### Dropdown-Navigation

Eine Hauptnavigation – sei es nur die erste Ebene oder eine Dropdown-Navigation mit mehrfachen Ebenen – benötigt eigentlich jede Website.

<a name="custom-erste-ebene"></a>
#### Erste Ebene

Zum Schreiben eigener Navigationen ist der Wert im path-Feld eines Artikels von elementarer Bedeutung. Dort findet man über Pipe-Symbole getrennt die IDs der Eltern-Kategorien. Nehmen wir an, ein Artikel befindet sich in der dritten Kategorie-Ebene. Nehmen wir weiterhin an, die Eltern-Kategorie in der ersten Ebene hat eine 2, die Eltern-Kategorie in der zweiten Ebene hat eine 4. So hat unsere Unterkategorie in der dritten Ebene im path-Feld den Eintrag `2|4`. Mit diesem Wert lässt sich nun immer bestimmen, wo in der Struktur sich der aktuelle Artikel befindet.

```
<?php
// Indem an den path-Wert des aktuellen Artikels noch die eigene ID angehängt wird,
// entsteht ein Array mit allen IDs der Kategorien für den aktuellen Artikel 
$path = explode("|",$this->getValue("path").$this->getValue("article_id")."|");

// Für eine Navigation mit nur einer Ebene wird nur das erste Element des Arrays benötigt,
// also die ID der obersten Elternkategorie.
$path1 = ((!empty($path[1])) ? $path[1] : '');

echo '<ul>';

// Mit der Methode `getRootCategories` werden alle Kategorien im Hauptverzeichnis durchlaufen
foreach (rex_category::getRootCategories() as $lev1) {

	// Es werden nur Kategorien mit dem Status `online` berücksichtigt.
	if ($lev1->isOnline(true)) {
		
        // Sofern die in der Schleife durchlaufene Kategorie mit der eigenen Elternkategorie identisch ist,
        // wird eine CSS-Klasse angehängt, um den Navigationspunkt als aktiv kennzeichnen zu können. */
        if ($lev1->getId() == $path1) {
            echo '<li class="active"><a href="'.$lev1->getUrl().'">'.htmlspecialchars($lev1->getValue('name')).'</a></li>';
        } else {
            echo '<li><a href="'.$lev1->getUrl().'">'.htmlspecialchars($lev1->getValue('name')).'</a></li>';
        }
	 
    }
}

echo '<ul>';
?>
```

<a name="custom-mehr-ebenen"></a>
#### Zwei oder mehr Ebenen

Nach dem gleichen Schema wie in der ersten Ebene können weitere Ebenen durchlaufen werden. Das Beispiel zeigt eine Navigation mit zwei Ebenen. Eine dritte und vierte Ebene kann dem Schema folgend rasch implementiert werden. Diese Navigation eignet sich übrigens auch zum Erstellen einer Sitemap.

```
<?php
$path = explode("|",$this->getValue("path").$this->getValue("article_id")."|");
$path1 = ((!empty($path[1])) ? $path[1] : '');
$path2 = ((!empty($path[2])) ? $path[2] : '');

echo '<ul>';

    foreach (rex_category::getRootCategories() as $lev1) {
        if ($lev1->isOnline(true)) {
    
            $active = ($lev1->getId() == $path1) ? ' class="active"' : '';
            $nav_main .= '<li'.$active.'><a href="'.$lev1->getUrl().'">'.htmlspecialchars($lev1->getValue('name')).'</a>';
    
            // START zweite Ebene
            $lev1Size = sizeof($lev1->getChildren());    

            // Soll nur der jeweils aktive Kategoriebaum erscheinen?
            // Dann die folgende Zeile auskommentieren:
            // if ($lev1->getId() == $path1) {

            if ($lev1Size != "0") {
    
                echo '<ul>';
    
                    foreach ($lev1->getChildren() as $lev2) {
                        if ($lev2->isOnline(true)) {
    
                            $active = ($lev2->getId() == $path2) ? ' class="active"' : '';
                            echo '<li'.$active.'><a href="'.$lev2->getUrl().'">'.htmlspecialchars($lev2->getValue('name')).'</a></li>';
                        }
                    }
    
                echo '</ul>';

            }

            // Soll nur der jeweils aktive Kategoriebaum erscheinen?
            // Dann die folgende Zeile auskommentieren:
            // }

            echo '</li>';
        }
    }

echo '</ul>';
?>
```

<a name="custom-sidebar"></a>
### Sidebar-Navigation

Oftmals möchte man in der Seitenspalte als Navigation die Unterkategorien der gerade aktiven Hauptkategorie ausgeben. dazu könnte man beispielsweise die rex_category-Klasse nutzen.

```
<?php
$thisCat = rex_category::get($this->getValue('article_id'));
$children = $thisCat->getChildren();
echo '<ul>';
if (is_array($children)) {
	foreach ($children as $child) {
	   // Nur wenn Kategorie online
	   if ($child->isOnline()) {
		  echo '<li><a href="'.rex_getUrl($child->getId()).'">'.$child->getName().'</a></li>';
	   }
	}
}
echo '</ul>';
```

In der ersten Zeile erfolgt der Zugriff auf die rex_category-Klasse, wobei gefiltert wird nach der ID der aktuellen Seite. Die rex_category-Klasse stellt dabei den Zugriff auf die in der Strukturverwaltung angelegten Kategorien her. Danach wird das Array der Unterkategorien mit dem Status `online` durchlaufen und als Linkliste ausgegeben. Die Funktion `rex_getUrl(ID)` dient dazu, den Link zu erzeugen.

<a name="custom-breadcrumb"></a>
### Breadcrumb

Für einen Brotkrumenpfad benötigt man nicht alle Kategorien, sondern nur den linear in die Tiefen gehenden Kategoriebaum des gerade aktiven Artikels. Dafür kann man `getParentTree()` nutzen, das ein Array aller Elternkategorien zurückgibt.

```
<?php
// Aktuellen Artikel ermitteln
$article = rex_article::get($this->article_id);
// Array der Elternkategorien
$parent = $article->getParentTree();

$breadcrumb = '<ul>';

    // Startartikel als Erstes anzeigen
    $breadcrumb = '<li><a href="'.rex_getUrl(rex_article::getSiteStartArticle()).'">Start</a></li>';
    
    // rekursiv den Kategoriebaum der gerade aktiven Kategorien durchlaufen
    foreach($parent as $cat) {
        $breadcrumb .= '<li><a href="'.$cat->getUrl().'">'.$cat->getName().'</a></li>';
    }

$breadcrumb .= '<ul>';
?>
```

<a name="custom-artikellisten"></a>
### Artikellisten

Oftmals will man neben den klassischen Navigationen noch verschiedene Artikel-Auflistungen einsetzen. Diese häufig genutzten verlinkten Listen werden mit jeweils einem Beispiel erläutert.

<a name="custom-teaser"></a>
#### Artikel-Teaser für Unterkategorien

Eine gern genutzte Funktion für Hauptkategorie-Seiten ist das "Anteasern" der Unterkategorien, z.B. in einem Kasten mit zusätzlichem Bild und einem Kurztext. Das Bild und der Kurztext wird mit Artikel-Metafeldern `category_pic` und `category_desc` realisiert, die natürlich vorher angelegt werden müssen.

```
<?php
$cats = rex_category::get($this->getValue('article_id'));
// Array mit allen Unterkategorien, die den Status online haben (Parameter true)
$children = $cats->getChildren(true);

if (is_array($children)) {

    echo '
    <ul>';

    foreach ($children as $child) {

        $media = $child->getValue('art_category_pic');
        $title = $child->getValue('name');
        $desc = $child->getValue('art_category_desc');
   
        // Bild und Kurztext sind Pflichtfelder
        if ($media != '' && $desc != '') {
    
            // Das Bild wird mit mit einem Media Manager-Effekt namens "thumbnail" bearbeitet
            echo '
            <li>
                <a href="'.rex_getUrl($child->getValue('id')).'">
                    <img src="index.php?rex_media_type=thumbnail&rex_media_file='.$media.'" alt="'.$desc.'">
                    <h3>'.$title.'</h3>
                    <p>'.$desc.'</p>
                </a>
            </li>';
    			
        }
    }
    echo '
    </ul>';

}
```

<a name="custom-artikel-kategorie"></a>
#### Alle Artikel in einer Kategorie auflisten

Man will nicht immer mit Unterkategorien arbeiten. Manchmal legt man auch mehrere Artikel innerhalb einer Kategorie an – ein typischer Anwendungsfall könnte ein Text sein, der auf mehrere Artikel aufgeteilt wird und für den man eine Navigation anbieten will. Das Code-Beispiel listet alle Artikel in der aktuellen Kategorie auf.

```
<?php
$current_cat = rex_category::get(REX_ARTICLE_ID);
// Array aller Artikel in der aktuellen Kategorie
$articles = $current_cat->getArticles(true);

if (is_array($articles) && count($articles) > 0) {
	echo '<ul>';

	foreach ($articles as $article) {

		// Der aktuelle Artikel soll nicht in der Liste auftauchen
		if ($article->getId() == REX_ARTICLE_ID) continue;
		// Der Startartikel soll ebenfalls nicht in der Liste auftauchen
		if ($article->isStartArticle()) continue;

		echo '
		<li><a href="'.$article->getUrl().'">'.$article->getName().'</a></li>';

	}
	echo '
	</ul>';
} 
?>
```

<a name="custom-blaetter"></a>
### Blätter-Navigation für Artikel

Diese Navigation ähnelt der obigen, aber sie zeigt nicht alle Artikel, sondern verlinkt nur den vorhergehenden und den nachfolgenden in der Reihenfolge der Artikelpriorität.

```
<?php
$predecessor = '';
$successor = '';
$article_stack[] = array();
	
// Objekt der aktuellen Kategorie laden
$cat = rex_category::get($this->getValue("category_id"));

// aktuellen Artikel ermitteln
$current_id = $this->getValue("article_id");
$current_article = rex_article::get($current_id);

// alle Artikel aus der aktuellen Kategorie laden
$article = $cat->getArticles(true);

if (is_array($article)) {
    // Artikelreihenfolge in eine Array schreiben
    foreach ($article as $var) {		
        // Startartikel werden ignoriert
        if ($var->isStartArticle()) continue;
        $article_stack[] = $var->getId();
    }

    $i = 0;
    // Zahl der Artikel ermitteln
    $catcount = count($article_stack);
    foreach ($article_stack as $var) {	
        if($var == $current_id) {
            if($i+1 < $catcount ) {
                // ID des nachfolgenden Artikels ermitteln
                $next_id = $article_stack[$i+1];

                // Artikel-Objekt holen, um den Namen des vorhergehenden Artikels zu ermitteln,
                // danach Link schreiben
                $article = rex_article::get($next_id);
                $successor = '
                <li class="next">
                    <a href="'.rex_getUrl($next_id).'">
                        weiter ('.$article->getName().')
                    </a>
                </li>'; 
            }

            // und das Ganze nochmal für den vorhergehenden Artikel
            if($i-1 > -1) {
                $prev_id = $article_stack[$i-1];			

                if($i < $catcount ) {

                    $article = rex_article::get($prev_id);
                    $predecessor = '
                    <li class="prev">
                        <a href="'.rex_getUrl($prev_id).'">
                            zurück ('.$article->getName().')
                        </a>
                    </li>';
                }
            }
        }		
        $i++;
    }
}

// Startartikel-Objekt holen, um den Namen des Startartikels zu ermitteln,
// danach die Linkzeile schreiben
$start_article = $cat->getStartArticle();
echo '
<ul>
    '.$predecessor.'
    <li class="top">
        <a href="'.rex_getUrl($start_article->getValue('id')).'">
            Übersicht ('.$start_article->getValue('name').')
        </a>
    </li> 
    '.$successor.'
</ul>';
?>
```

<a name="custom-onepage"></a>
### Onepage-Navigation

Es gibt bei einer Onepage-Website – wie so oft bei REDAXO – verschiedene Möglichkeiten, das Ziel zu erreichen.
Ein Weg wäre, die einzelnen Sektionen der Seite Artikeln oder Unterkategorien aufzubauen. Jeder Artikel würde eine Sektion abbilden mit dazugehörigem Navigationspunkt und Sprunganker.

Eine andere Lösung wäre, die Navigation und Sprunganker mit einem Modul umzusetzen, alles innerhalb einer Seite. Im Folgenden werden beide Ansätze vorgestellt, beide haben gleichermaßen ihre Berechtigung.

<a name="custom-onepage-artikel"></a>
#### Onepage-Navigation mit Artikeln

Die Erklärungen finden sich als Kommentare im Code.

```
<?php
// Variable definieren für den Content
$content = '';

// Zunächst werden für die ID des aktuellen Artikels alle Artikel ermittelt,
// die in der gleichen Kategorie liegen.
// Der Parameter `true` bewirkt, dass nur Artikel mit Status `online` berücksichtigt werden.
$cat = rex_category::get($this->article_id);
$articles = $cat->getArticles(true);

// Sofern sich Elemente in dem Array befinden,
// es also überhaupt Artikel gibt, wird die ul-Liste geöffnet.
if (is_array($articles) && count($articles) > 0) {
    echo '<ul>';
							
    // Alle Artikel werden durchlaufen
    foreach ($articles as $article) {

        // Der aktuelle Artikel der Seite selbst soll nicht berücksichtigt werden
        if ($article->getId() == $this->getValue('article_id')) continue;
        // Auch der Startartikel der Kategorie, meistens die Seite selbst,
        // soll nicht berücksichtigt werden
        if ($article->isStartArticle()) continue;
			
			// Als Ankernamen werden Artikelnamen benutzt,
			// Sonderzeichen werden durch die REDAXO-Funktion `normalize()` umschrieben.
			// Die Syntax lautet `normalize($string, $replaceChar = '_', $allowedChars = '')`
        echo '
        <li><a href="#'.rex_string::normalize($article->getName()).'">'.$article->getName().'</a></li>';				
							
        // Hier wird der Content des jeweiligen Artikels geholt
        $article_content = new rex_article_content($article->getId());
        // Der Content wird jeweils an die content-Variable angehängt
        $content .= $article_content->getArticle();

    }
    echo '</ul>';
} 

// Endlich: Der Content wird ausgegeben
echo $content;
```

<a name="custom-onepage-module"></a>
#### Onepage-Navigation mit Modulen

Hier erzeugt ein Modul "Navigations-Anker" sowohl die Sprunganker als auch die Navigation. Die Website kann also aus einem einzigen Artikel bestehen.

Im Eingabe-Code kann man den Navigationstitel und den Anker manuell setzen. Für den Anker könnte man auch den Titel nehmen und wie im Beispiel oben die Sonderzeichen mit `normalize()` entfernen.

```
<!-- *******************************************************
NAVIGATIONS-ANKER INPUT
******************************************************** -->

<fieldset class="form-horizontal">
    <legend>Navigations-Anker</legend>
		<div class="form-group">
		<label class="col-sm-2 control-label" for="title">Navigationstitel</label>
		<div class="col-sm-10">
			<input class="form-control" id="title" type="text" name="REX_INPUT_VALUE[1]" value="REX_VALUE[1]" />
		</div>
	</div>
	<div class="form-group">
		<label class="col-sm-2 control-label" for="anchor">Anker (keine Sonderzeichen, Leerzeichen, etc.)</label>
		<div class="col-sm-10">
			<input class="form-control" id="anchor" type="text" name="REX_INPUT_VALUE[2]" value="REX_VALUE[2]" />
		</div>
	</div>
</fieldset>
```

Der Ausgabe-Code setzt immer den Sprunganker an die Stelle, wo sich das Modul befindet. Um die Navigation aufzubauen, müssen die Werte gesammelt werden, um sie an der passenden Stelle im Template auszugeben. Dafür werden die Methoden `rex::getProperty()` und `rex::setProperty` verwendet, die im Kapitel [Eigenschaften (rex::)](/{{path}}/{{version}}/eigenschaften) näher erläutert werden.

```
<!-- *******************************************************
NAVIGATIONS-ANKER OUTPUT
******************************************************** -->

<?php
if ("REX_VALUE[1]" != '' && "REX_VALUE[2]" != '') {
	echo '
	<div id="REX_VALUE[2]"></div>';

	if (!isset($counter)) {
		$counter = 0;
	}
	$counter++;

	// Daten für das Frontend in ein Array schreiben, aber sie nicht anzeigen
	if (!rex::isBackend()) {
		$items = array();
		$items = ['anchor' => 'REX_VALUE[2]', 'title' => 'REX_VALUE[1]'];
		rex::getProperty('anchors')->append($items);
	} else {
		// Im Backend wird der Inhalt nur als Info für den Redakteur angezeigt
		if ('REX_VALUE[id=1 isset=1]') {
		    echo '<h1 style="background: #000; padding: 20px 40px; color: #fff;">REX_VALUE[1]</h1>';
		}
	}
}

```

Im Template wird ganz zu Beginn das Array `anchors` definiert. dann wird der Inhalt geparst, um das Array mit Inhalten zu füllen – was in der Modulausgabe passiert.
Anschließend stehen die Daten zur Verfügung, um daraus die Navigation, bestehend aus Anker und Navigationstitel zu bauen. Anschließend an die Navigation wird der bereits geparste Content ausgegeben.

```
<?php
rex::setProperty('anchors', new ArrayIterator());

// Parse Content
$content = $this->getArticle('1');
?>

<?php
// Anker-Links der Module einlesen
$items = rex::getProperty('anchors')->getArrayCopy();
				
if (count($items) > 0) {
					
    echo '
    <ul>';
						
        foreach ($items as $item) {
            echo '
            <li><a href="#'.$item['anchor'].'">'.$item['title'].'</a></li>';				}

    echo '
    </ul>';
}

echo $content;
```



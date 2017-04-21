# Erstellen einer Navigation

Eine Webseite braucht verschiedene Arten von Navigationen – z.B. eine Navigation mit Unterebenen oder einfache Navigationen oder eventuell Kombinationen daraus. Auch ein Pfad oder eine Sitemap ist eine spezielle Art einer Navigation.

In REDAXO gibt es mehrere Möglichkeiten, dies umzusetzen. Für einfache Varianten existiert eine Klasse rex_navigation. Damit sollten die meisten Navigationsvarianten auch mit nur sehr wenig PHP-Kenntnissen umsetzbar sein.

Es empfiehlt sich, ein eigenes Template für die Navigation zu nutzen und dieses im Haupttemplate einzubauen.

Eine einfache Navigation könnte so aussehen:


```php <?php 
$nav = rex_navigation::factory();

echo '<div id="navi">';
echo $nav->get(0,-1,FALSE,TRUE);
echo '</div>';
?>
```

Wichtig ist vor allem folgende Zeile:
`$nav->get(0,-1,FALSE,TRUE);`
da diese definiert, wie die Navigation ausgegeben wird.

Mit dem ersten Parameter – hier “0” – definiert man, an welcher Stelle die Navigation startet. Mit “0” beginnt die Navigation in der obersten Ebene.
Der zweite Parameter legt die Anzahl der Ebenen fest: “-1” bedeutet, dass alle Ebenen ausgegeben werden. Ansonsten wird hier die Anzahl der Ebenen eingetragen. Häufiger Wert hier ist 3.
Mit dem dritten Parameter wird definiert, ob alle Kategorien oder nur die Aktiven ausgegeben werden. “FALSE” erzeugt quasi eine Sitemap, “TRUE” eine “normale” Navigation.
Der vierte Parameter legt fest, ob nur Artikel die online sind (“TRUE”) angezeigt werden sollen oder auch Offline-Artikel (“FALSE”)
Die Navigation wird in diesem Fall mit einem vordefiniertem HTML-Code ausgegeben – in unserem Fall eine Liste. Mit folgendem Stylesheet lässt sich daraus eine einfache Formatierung erzeugen


```HTML
<style>

#navi ul {
border-top: 1px solid #D2D2D2;
}
#navi ul li {
background-color: #F6F6F6;
border-bottom: 1px solid #D2D2D2;
}
#navi ul li a {
display: block;
padding: 3px 5px;
color: #E30510;
font-weight: bold;
}
#navi ul li a:hover, 
#navi ul li a.rex-current {
background-color: #E30510;
color: #FFF;
}

</style>
```

Folgender Code gibt eine Sitemap aus, welche in der obersten Ebene startet und wegen der “-1” alle Ebenen durchläuft.

**Sitemap**

```PHP
<?php
$nav = rex_navigation::factory();

echo '<div id="sitemap">';
echo $nav->get(0,-1,TRUE,TRUE);
echo '</div>';
?>
```

Mit folgendem Code erzeugt man eine Breadcrumb-Navigation:

**Breadcrumb**


```PHP
<?php
$nav = rex_navigation::factory();

echo '<div id="breadcrumb">';
echo $nav->getBreadcrumb(TRUE,TRUE,0);
echo '</div>';
?>
```

## Eigene Navigation schreiben


```PHP
<?php

$PATH = explode("|",$this->getValue("path").$this->getValue("article_id")."|");

echo '<ul class="nav1">';
foreach (OOCategory::getRootCategories() as $lev1)
{
if($lev1->getId() == $PATH[1])
echo '<li class="active"><a href="'.$lev1->getUrl().'">'.$lev1->getName().'</a>';
else
echo '<li><a href="'.$lev1->getUrl().'">'.$lev1->getName().'</a>';

if(count($lev1->getChildren())>0)
{
echo '<ul class="nav2">';
foreach ($lev1->getChildren() as $lev2)
{
if($lev2->getId() == $PATH[1])
echo '<li class="active"><a href="'.$lev2->getUrl().'">'.$lev2->getName().'</a>';
else
echo '<li><a href="'.$lev2->getUrl().'">'.$lev2->getName().'</a>';
}
echo '</ul>';
} 
echo '</li>';
}
echo '</ul>';

?>
```



# Kategorien Eigenschaften (Meta-Infos Addon)

## Einleitung / Problemstellung
Ein sehr hilfreiches REDAXO-Feature, das noch wenig bekannt ist und eine weitreichende Erweiterung für den Redakteur bieten kann, ist das Meta-Daten AddOn.

Eines von vielen Anwendungsbeispielen:
Eine Webseite hat eine Hauptnavigation, in der alle Root-Kategorien der Strukturverwaltung angezeigt werden sollen (online/offline). Daneben sollen andere Root-Kategorien in der einer zweiten Navigation angezeigt werden.

Der Redakteur soll Kategorien den verschiedenen Navigationen zuordnen können.

## Lösung
Klickt man bei einer Kategorie auf “ändern”, so sieht man neben der Eingabe des Kategorienamens keine weiteren Möglichkeiten. Um hier weitere Felder selbst anzulegen, wechselt man in das AddOn Meta-Infos. Dort findet man drei Reiter, um für die Bereiche “Artikel”, “Kategorie” und “Medien” weitere Felder zu erstellen. Wechseln wir in Kategorien und erstellen eine neue Meta-Info.

Neben dem Namen der Info kann der Spaltenname und die Reihenfolge bei mehreren Infos definiert werden.
Für den Zugriff auf diese Info ist der Spaltenname entscheidend.

Um die Kategorie den zwei Navigationstypen zuweisen zu können, wählen wir für dieses Beispiel den Spaltennamen typ. Für die Auswahl der Typen wählen wie als Feldtyp “select” und definieren zwei Werte und Bezeichnungen:


```1:Hauptnavigation|2:Unternavigation
```

![Feld bearbeiten](/assets/4-x-tutorial-meta-01.jpg)

Als Standdard-Wert tragen wir den Wert 1 für die Hauptnavigation ein.
Über Speichern wird diese Info für alle Kategorien erstellt.

Wechselt man nun zurück in die Strukurverwaltung und ändert dort wieder die Kategorie erscheint, dort eine zusätzliches +-Symbol, über das man die eben erstellten Meta-Infos erreicht.

Hier erscheint nun die von uns angelegte Select-Box, in der der Redakteur nun die der Kategorie einer der beiden Navigationen zuweisen kann.

![Metapflege in der Struktur](/assets/4-x-tutorial-meta-02.jpg)

## Template

Nun fehlt im Template noch die Auswirkung dieser Zuweisung.
Ein Beispiel für ein Navigationstemplate “Ausgabe aller Kategorien (online) im Root-Verzeichnis” könnte so aussehen:

```PHP
<?php
$nav1 .= '<ul>';

foreach (OOCategory::getRootCategories() as $lev1) {
if ($lev1->isOnline(true)) $nav1 .= '<li><a href="'.$lev1->getUrl().'">'.$lev1->getName().'</a>';
}
$nav1 .= '</ul>';
?> 
```

Der zugewiesene Navigations-Typ in der der Meta-Info einer Kategorie (Spaltenname typ) kann so ausgelesen werden:

```PHP
$cat_typ = $lev1->getValue("cat_typ");
```

Mit Berücksichtigung der Navigationszuweisung könnten nun die Ausgabe der beiden Navigationen so aussehen:


```PHP
<?php
$nav1 .= '<ul>';
$nav2 .= '<ul>';

foreach (OOCategory::getRootCategories() as $lev1) {
if ($lev1->isOnline(true)) {
$cat_typ = $lev1->getValue("cat_typ");

if ($cat_typ == 1) $nav1 .= '<li><a href="'.$lev1->getUrl().'">'.$lev1->getName().'</a>';

if ($cat_typ == 2) $nav2 .= '<li><a href="'.$lev1->getUrl().'">'.$lev1->getName().'</a>';
}
}

$nav1 .= '</ul>';
$nav2 .= '</ul>';
?>

```

Daneben kann man mit Meta-Infos natürlich auch sehr einfach Kategorie-Bilder oder Texte hinterlegen und auslesen.

In neueren Redaxo-Versionen (ab Version 4.2) ist es noch einfacher und völig ohne den Einsatz von PHP möglich, Meta-Infos auszugeben. So könnte man beispielsweise eine Meta-Info (Spaltenname: “info”) für Texteingaben definieren:


```
<span class="cat_info">REX_CATEGORY[field="info"]</span>
```

In diesem Tutorial wurde der Einsatz von Meta-Infos bei Kategorien erklärt. Darüber hinaus gibt es aber auch noch bei Artikeln und im Mediapool Meta-Infos. Typische Einsatzbereiche wären:

* Mit Artikel-Meta-Infos könnte man steuern, ob Top-Anker oder Druck-Links erscheinen, aber auch individuelle CSS-Stylesheets zuweisen – der Fantasie sind keine Grenzen gesetzt.
* Im Medienpool wird man Meta-Infos meist nutzen, um Bildbeschreibungen oder Fotograf-Credits zu veralten.

Wenn man jedoch nachzudenken beginnt, was man die Meta-Infos alles anstellen könnte, eröffnen sich nahezu unbegrenzte Möglichkeiten.



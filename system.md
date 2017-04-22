# System

- [Einstellungen](#einstellungen)
- [Sprachen](#sprachen)
- [mod_rewrite](#mod_rewrite)

<a name="einstellungen"></a>
## Einstellungen


### Cache löschen und Setup

Die Ansicht Einstellungen bietet die Features Cache löschen und Setup. Außerdem werden allgemeine Systemeinstellungen gelistet, die teilweise hier auch editiert werden können.

**Cache löschen**

Informationen zu Kategorien und Artikeln werden bei Redaxo nicht über SQL-Anfragen ermittelt, sondern aus generierten Dateien gelesen. Die Informationen werden in REDAXO automatisch angelegt und für eine schnelle Ausgabe bereitgestellt. Die Dateien werden in den Ordnern “articles”, “files” und “templates” im Ordner “redaxo/include/generated/” gespeichert. REDAXO nutzt bei der Ausgabe von Webseiten diese Informationen für eine schnelle und datenbankunabhängige Darstellung.

Über die Funktion “Cache löschen” werden die Informationen zu Artikeln, Dateien und Templates neu erstellt. Dazu werden die gecachten Dateien gelöscht.

**Setup**

Hier können Sie das Setup neu starten.

**Einstellungen (rechte Spalte)**

Es wird eine Liste allgemeiner Systemeinstellungen angezeigt.

Sie sehen zunächst Angaben zur installierten Redaxo-Version und zu der Datenbank.

Ein paar der Angaben können Sie in dieser Maske ändern.

**$REX['START_ARTICLE_ID']**

Der Startartikel ist der Artikel, der beim Aufruf einer Webpräsentation als erster angezeigt wird. Hier kann dieser durch die Auswahl über die Linkmap (linker Button; s.Abb. unten) festgelegt werden. Standardmäßig ist hier “Home” (=ArtikelID=1) voreingestellt.

**$REX['NOTFOUND_ARTICLE_ID']**

Sollte ein Seite nicht mehr existieren oder ein fehlerhaft verlinkter Artikel aufgerufen werden, kann hier angegeben werden, welcher Artikel stattdessen angezeigt werden soll, um mögliche Besucher nicht ins Leere laufen zu lassen.

**$REX['LANG']**

Sie können die Backend-Sprache wählen. Aktuell können Sie zwischen Deutsch, Englisch, Deutsch (utf-8) & Englisch (utf-8) wählen. Weitere Sprachen finden Sie im Downloadbereich unter dem Punkt Sprachpakete und können nach der Installation hier ausgewählt werden.

**$REX['MOD_REWRITE']**

Wollen Sie “sprechende Links”, die die entsprechenden Artikelnamen und nicht nur die Artikel_IDs in der URL anzeigen, müssen Sie für diese Variable “TRUE” einstellen.


<a name="sprachen"></a>
## Sprachen

Mit Redaxo können Sie mehrsprachige Webauftritte bequem umsetzen. Unter der Rubrik “Sprachen” können beliebig viele Sprachen angelegt werden.

Das System ist sehr flexibel. Die Sprachen können vor der Festlegung der Kategorien und Artikel angelegt werden. Es ist aber auch möglich, nach Festlegung der Seitenstruktur und der Inhalte noch Sprachen zu ergänzen. Dabei wird immer die aktuelle Struktur für jede angelegte Sprache gespiegelt. D.h. die Kategorien und Artikel sind in jedem Land identisch angelegt. Die Bezeichnungen der Kategorien und Artikel werden zunächst in allen Sprachen übernommen. Sie können dann entsprechend angepaßt werden. Wenn ein Artikel in einer Sprache neu angelegt wird, geschieht dies automatisch auch in allen anderen Sprachen. Die gespiegelten Artikel sind jedoch ohne Inhalte und müssen in er jeweiligen Sprache mit Inhalten versehen werden.

Neu angelegte Kategorien und Artikel sind standardmäßig „offline“ gesetzt. Es ist möglich, diese Einstellung in jedem Land separat zu ändern. D. h. eine Seite, die in einer Sprache keine Relevanz hat, muß in dieser Sprache nicht mit Inhalten gefüllt und angezeigt werden.

**Neue Sprache anlegen**

Zum Anlegen einer Sprache klickt man auf das + Symbol, gibt den Namen der Sprache an und legt eine ID fest. Jede Sprache erhält eine eindeutige ID, über die die Navigation gesteuert wird. Die aktuelle Sprach-ID ist in der Redaxo-Variablen $REX['LANG'] gespeichert.

**Sprachen verlinken**

In der Navigation erfolgt der Wechsel zwischen den Sprachen, indem man auf die gewünschte Sprach-ID verlinkt.

Als Beispiel hier der Link zum Artikel mit der Artikel_ID 20 und der Sprach_ID 1:

Innerhalb eines PHP-Codes:

```
echo "<a href=".rex_getUrl(20, 1).">Ein Linktext</a>";
```

Innerhalb eines html-Codes:

```
<a href="<?php echo rex_getUrl(20, 1); ?>">Noch'n Linktext</a>
```

**Sprachen löschen**

Einzelne Sprachen können jederzeit gelöscht werden. Diese Funktion sollte man mit Vorsicht genießen, da hier „Tabula rasa“ gemacht wird. Mühselig eingepflegte Inhalte kann man dabei mit einem Knopfdruck ins Nirwana schicken.

**UTF-8-Codierung**

Redaxo unterstützt auch die Erstelung von Webseiten, die UTF-8-Codierung erfordern. Wollen Sie diese Möglichkeit nutzen, so beachten Sie bitte, dass Frontend und Backend dieselben Einstellungen haben müssen. ISO und UTF-8 im Mix geht nicht. Die Festlegung für das Backend erfolgt unter System/Einstellungen. Sobald man im Template als charset utf-8 angibt, muss man auch im Backend eine UTF-8-Spracheinstellung auswählen.

**htmlspecialchars()**

Wenn eine Seite UTF-8 konform sein soll, dann darf nur noch im Bedarfsfall htmlspecialchars() verwendet werden! htmlentities() ist nicht zulässig.


<a name="mod_rewrite"></a>
## mod_rewrite

In der Url-Zeile Ihres Browsers werden die einzelnen Artikel über die Seite index.php mit
dem Parameter article_id aufgerufen.

http://www.redaxo.de/index.php?article_id=1

Moderne Suchmaschinen sind zwar in der Lage dynamisch erzeugte Seiten (z. B. “index.php?seite=12&inhalt=3&foo=bar”) zu indizieren und in den Index aufzunehmen, jedoch haben auch sie Schwierigkeiten wenn die Anzahl der übergebenen Parameter zu gross wird. Um die Url suchmaschinenfreundlicher zu gestalten, steht auch in REDAXO ein ModRewrite zur Verfügung.

mod_rewrite ist ein Apache Modul für die URL Manipulation. Mit der RewriteEngine des Apache-Webservers ist es möglich die angeforderte URL anhand von Regeln “umzuschreiben”. Basierend auf einem Parser für Reguläre Ausdrücke kann die angeforderte URL manipuliert werden.

In den REDAXO 4.* zips befindet sich in der obersten Ebene eine _.htaccess-Datei mit folgendem Inhalt:

```
RewriteEngine On

# RewriteBase /
RewriteRule ^([0-9]*)-([0-9]*)- index.php?article_id=$1&clang=$2&%{QUERY_STRING}
RewriteRule ^([0-9]*)- index.php?article_id=$1&%{QUERY_STRING}
```

Diese muss in .htaccess umbenannt werden! Ab 4.3 muss die Datei nicht umbenannt werden, da sie schon direkt als “.htaccess” vorliegt.

In Redaxo muß unter System der MOD_REWRITE-Modus eingeschaltet werden (Auf true stellen).

Nun werden alle URLs, die über die Funktion

```
rex_getUrl($articleId, $sprachId, $parameterArray);
```

angesprochen werden, umgewandelt in eine lesende URL, die htaccess dann interpretiert.

**Konfiguration der htaccess**

Bei diesem Eintrag gehen wir davon aus, das die Dateien im ROOT-Verzeichnis geladen sind. Sollte die Webseite mit den Dateien in einem Unterordner geladen sein, dann sollte der Eintrag in der 3. Zeile (RewriteBase) angepasst werden.

Webseite im Ordner “xyz”:

```
RewriteBase /xyz
```

**Urls erstellen**

Um in REDAXO Urls zu erstellen sollte mit der rex_getUrl Funktion gearbeitet werden.

Wechseln zwischen Sprachen: (Wechselt von der aktuellen Sprache auf die Sprache mit der Id 3)

```
<?php
echo '<a href="'. rex_getUrl(1, 3) .'">linktext</a>';
?>
```

**Parameter übergeben**

URLs, die Parameter enthalten, sollte wie folgt erstellt werden:

Dieses Beispiel beschreibt den Wechsel auf den Artikel mit der Id=1, die aktuelle Sprache wird beibehalten, und es wird ein Parameter übergeben.

```
<?php
echo '<a href="'. rex_getUrl(1, '', array('name' => 'wert')) .'">linktext</a>';
?>
```




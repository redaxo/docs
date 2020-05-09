# Kategorien & Artikel

* [Die Strukturverwaltung](#strukturverwaltung)
* [Kategorien erstellen die Struktur](#kategorien)
* [Artikel geben die Inhalte aus](#artikel)
* [Module/Blöcke liefern die einzelnen Inhaltsblöcke](#module)
* [Content-Bereiche (C-Types)](#ctypes)
* [Metainformationen](#metainfos)
* [Code-Beispiele](#code-beispiele)
  + [Zentrale Artikel in den Website-Einstellungen](#zentrale-artikel)
  + [Daten des aktuellen Artikels](#aktueller-artikel)
  + [Zugriff auf Kategorie-Daten](#kategorie-daten)

<a name="strukturverwaltung"></a>

## Die Strukturverwaltung

In der Strukturverwaltung von REDAXO gibt es Kategorien und Artikel. Aus Datenbanksicht gibt es nahezu keinen Unterschied; sowohl Kategorien als auch Artikel werden in der Tabelle `rex_article` gespeichert. Im Prinzip ist es nur ein "Flag" in der Datenbank-Spalte `startarticle` , die den Datensatz kennzeichnet: `true` als Kategorie, `false` als Artikel.

Wozu braucht man also den Unterschied zwischen Kategorie und Artikel? **Kategorien** bilden die **Struktur**, **Artikel** speichern die **Inhalte**.

<a name="kategorien"></a>

## Kategorien erstellen die Struktur

Kategorien dienen vor allem zum Aufbau einer Navigation. Es gibt zwar in REDAXO durch die Flexibilität des Systems meist mehrere Wege, das gewünschte Ziel zu erreichen, aber man erstellt üblicherweise die Navigations-Struktur mit Kategorien. Weil Kategorien in beliebiger Tiefe Unterkategorien enthalten können, sind der Komplexität von Navigationen keine Grenzen gesetzt. Um eine neue Kategorie anzulegen, klickt man auf den Ordner mit dem Pluszeichen; um eine bestehende Kategorie zu bearbeiten auf "Ändern".

Dort kann man auch die Priorität, also die Reihenfolge festlegen. "Online/Offline" schließlich vergibt einen Kategoriestatus – das heißt aber nicht, dass diese Kategorie nicht zu sehen ist. (Das entscheidet der Entwickler, wie mit Offline-Artikel verfahren wird.)

Jede Kategorie hat einen Startartikel. Startartikel sind Einstiegsseiten einer Kategorie. Diese Startartikel kann man nicht löschen, man muss dann die Kategorie selbst löschen. Wie oben schon erwähnt ist es der "Startartikel-Status", der einen Artikel als Kategorie markiert.

<a name="artikel"></a>

## Artikel geben die Inhalte aus

Ein Artikel ist der Bereich, der Inhalte mithilfe der eingepflegten (Inhalts-)Blöcke auf einer Seite der Webpräsenz ausgibt. Eine Kategorie hat immer mindestens einen Artikel (den Startartikel), kann aber weitere Artikel (und Unterkategorien) haben. Diese Logik kann man z. B. so nutzen:

* Der Startartikel liefert die Übersicht, z. B. von Neuigkeiten
* Die weiteren Artikel sind die einzelnen Neuigkeiten, die Detailseiten

Ein Artikel muss ein Template haben. Templates enthalten im Normalfall das HTML-Grundgerüst und werden in einem eigenen Kapitel [Templates ausführlich erläutert](/{{path}}/{{version}}/templates).

<a name="module"></a>

## Module/Blöcke liefern die einzelnen Inhaltsblöcke

Ein Artikel enthält verschiedene Inhaltssegmente. Es gibt normalerweise immer mindestens Inhaltsblöcke für Überschriften, Texte, Bilder etc.
Blöcke kann man beliebig oft in einem Artikel verwenden. So kann man z. B. verschiedene Absätze wie auch Bilder nach Belieben anlegen und einen einzelnen Artikel immer mehr erweitern.

Module werden im Normalfall vom Entwickler individuell für jede Website erstellt, sodass man die entsprechenden Besonderheiten einer Website gut abbilden kann.

Module bestehen aus Eingabe- und Ausgabebereichen. Ein Redakteur gibt bestimmte Inhalte ein (gesteuert durch den Eingabe-Code), und diese werden dann auf der Webseite ausgegeben (gesteuert durch den Ausgabe-Code). Im Modul definiert der Entwickler also, welche Felder die Eingaben speichern und wie diese Inhalte in Form von Texten, Bilder etc. ausgegeben werden.

Auch Module werden in in einem eigenen Kapitel [Module ausführlich behandelt](/{{path}}/{{version}}/module).

<a name="ctypes"></a>

## Content-Bereiche (C-Types)

Modulinhalte müssen nicht auf einen Content-Bereich (auch Spalte oder C-Type gennant) limitiert sein. Der Entwickler kann bei den Templates beliebig  viele Inhaltsbereiche festlegen und diese benennen, z. B. Hauptspalte, Seitenspalte, Headerbereich etc. In den Templates wird dann definiert, wo an welcher Stelle die Ausgabe dieses Content-Bereichs erfolgt.

In der Rechteverwaltung kann festgelegt werden, welche Module in welcher Spalte verwendet werden dürfen und von welchem Redakteur.

Die C-Types werden ebenfalls im Kapitel [Templates dokumentiert](/{{path}}/{{version}}/templates).

<a name="metainfos"></a>

## Metainformationen

Metadaten sind zum Speichern von "Rahmeninformationen" eines Artikel gedacht – also bestimmte Informationen, die den Artikel näher beschreiben. Die Metainformationen werden auch oft für Inhalte oder Einstellungen genutzt, die außerhalb des Content-Bereichs liegen und so nicht über Module gepflegt werden können. Beispiele wären etwa verschiedene Seitenhintergründe oder ob der betreffende Artikel von der Navigation ausgeschlossen werden soll.

Metafelder, mit denen man Metainformationen pflegen kann, kann der Admin für Artikel, Kategorien, Medien und Sprachen anlegen.

Den Umgang mit Metainformationen behandelt ein eigenes Kapitel [Metainformationen ausführlich](/{{path}}/{{version}}/metainformationen).

<a name="code-beispiele"></a>

## Code-Beispiele

Nachfolgend als Einstieg einige erste Beispiele für den Umgang mit Artikel- und Kategorie-Daten. Detaillierter findet man dies ersten Ansätze "zum Reinschnuppern" in den Kapiteln [Konfiguration](/{{path}}/{{version}}/konfiguration) sowie [Navigationen](/{{path}}/{{version}}/navigationen) erklärt.

<a name="zentrale-artikel"></a>

### Zentrale Artikel in den Website-Einstellungen

```php
// Start-Artikel der Website
echo rex_article::getSiteStartArticle();

// 404-Artikel
echo rex_article::getNotfoundArticle();
```

<a name="aktueller-artikel"></a>

### Daten des aktuellen Artikels

```php
// Aktuelle Seiten-ID
echo rex_article::getCurrentId();
// Ebenfalls möglich:
echo $this->getValue('article_id');
// Ebenfalls möglich:
echo REX_ARTICLE_ID;

// Online/Offline-Status des aktuellen Artikels
echo rex_article::getCurrent()->isOnline();
// Ebenfalls möglich:
echo REX_ARTICLE[field='status'];
// Ebenfalls möglich:
echo $this->getValue("status");

// Nach gleichem Prinzip kann man auf Artikel-Metadaten zugreifen,
// sofern man das Metafeld vorher angelegt hat:
echo $this->getValue("art_headerbild");
// Nach gleichem Prinzip kann man auch auf Kategporie-Metadaten zugreifen,
// sofern man das Metafeld vorher angelegt hat:
echo $this->getValue("cat_navigation_type");
```

<a name="kategorie-daten"></a>

### Zugriff auf Kategorie-Daten

```php
// Alle Artikel in der aktuellen Kategorie zurückgeben
$cat = rex_category::get(REX_CATEGORY_ID);
$articles = $cat ? $cat->getArticles(true) : [];
dump($articles);

// Hinweis: Die Methoden zum Laden weiterer Kategorien besitzen meist
// auch einen Parameter zum Ignorieren von Offline-Inhalten: (true).

// Werte der aktuellen Kategorie
$cat = rex_category::getCurrent();
// Ebenfalls möglich:
$cat = rex_category::get(REX_CATEGORY_ID);
// Kategorie mit der ID 3
$cat = rex_category::get(3);
dump($cat);

// Rootkategorien in der obersten Ebene
$root_categories = rex_category::getRootCategories();
dump($root_categories);

// Unterkategorien der aktuellen Kategorie
$subcategories = rex_category::getCurrent()->getChildren();
dump($subcategories);
```

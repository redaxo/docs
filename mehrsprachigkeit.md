# Mehrsprachigkeit

- [Sprachen verwalten](#sprachen-verwalten)
- [Neue Sprachen anlegen](#neue-sprachen-anlegen)
- [Links](#links)
  - [Gleicher Artikel, andere Sprache](#gleicher-artikel-andere-sprache)
  - [Gleiche Sprache, anderer Artikel](#gleiche-sprache-anderer-artikel)
- [Sprach-Metafelder](#sprach-metafelder)
- [Beispiel einer einfachen Sprachnavigation](#beispiel-sprachnavigation)
- [Beispiel Sprachnavigation zeigt nur aktive Sprachen](#beispiel-nuronline)
- [Hilfreiche AddOns](#hilfreiche-addons)
 
<a name="sprachen-verwalten"></a>

## Sprachen verwalten

Mehrsprachige Websites sind mit REDAXO sehr einfach umsetzbar. Unter dem Menüpunkt `System` gibt es den Unterpunkt `Sprachen`. In jeder neuen REDAXO-Installation existiert bereits eine aktive Sprache, diese ist nicht löschbar. Standardmäßig hat diese Sprache den Code `de` und den Namen `deutsch`; dies kann aber geändert werden. Der Status kann auf `offline` gestellt werden – das hat aber wie bei den Artikeln und Kategorien zunächst keine Auswirkung auf das Frontend, kann aber selbstverständlich in der Frontend-Ausgabe genutzt werden.

<a name="neue-sprache-anlegen"></a>

## Neue Sprache anlegen

Eine neue Sprache wird über das Pluszeichen angelegt. Nach diesem Schritt – also wenn mindestens zwei Sprachen vorhanden sind – findet man in der Strukturansicht Links zum Wechsel in die anderen Sprachen.

Was ist durch diesen Schritt datenbanktechnisch passiert? Alle Artikel, also  alle Datensätze der Tabelle `rex_article`, wurden dupliziert und als leere Artikel mit der neuen Sprach-ID 2 gespeichert. Die ursprüngliche Sprache hat die ID 1, die zweite Sprache die ID 2, usw.

> **Hinweis:** In alten REDAXO-Version (4 und älter) fingen die Sprach-IDs mit der 0 an.

Da also jeder Artikel jeder Sprache in der Datenbank als eigener Datensatz vorliegt, können die Artikel in den Sprachen individuell umbenannt und sortiert werden.

> **Achtung:** Beim Löschen eines Artikels oder einer Kategorie werden aber automatisch alle Sprachversionen dieses Artikels oder dieser Kategorie gelöscht. Unterschiedliche Navigationen realisiert man am besten, indem man die Kategorien in den jeweiligen Sprachen auf online oder offline setzt.

<a name="links"></a>

## Links

Sobald es mehrere Sprachen gibt, ändert sich auch die Form der Links. REX-Variablen wie REX_LINK erzeugen ab sofort andere Links, die die Sprachkennung enthalten, z.B. `index.php?article_id=2&clang=2`. Der Parameter `clang` sorgt dabei für den Aufruf der Sprache mit ID 2.

Man kann Links aber natürlich auch manuell über PHP erstellen, mit `rex_getUrl`, wie hier im Beispiel ein Link auf den Artikel mit der ID 5 und der Sprache mit der ID 2:

```php
<a href="<?php echo rex_getUrl(5, 2); ?>">Link</a>
```

<a name="gleicher-artikel-andere-sprache"></a>

### Gleicher Artikel, andere Sprache

Um im gleichen Artikel zu bleiben und nur auf eine andere Sprache umzuschalten, könnte die Syntax wie folgt aussehen:

```php
<a href="<?php echo rex_getUrl($this->getValue('article_id'), 2); ?>">Link</a>
```

Alternativ kann man die Artikel-ID auch leer lassen:

```php
<a href="<?php echo rex_getUrl("", 2); ?>">Link</a>
```

<a name="gleiche-sprache-anderer-artikel"></a>

### Gleiche Sprache, anderer Artikel

Wenn man in der gleichen Sprache, jedoch auf einen anderen Artikel
verlinken möchte, kann man dies so realisieren:

```php
<a href="<?php echo rex_getUrl(5, rex_clang::getCurrentId()); ?>">Link</a>
```

Es reicht aber auch aus, nur die Artikel-ID zu übergeben. Die aktuelle Sprache wird von REDAXO automatisch erkannt.

```php
<a href="<?php echo rex_getUrl(5); ?>">Link</a>
```

<a name="sprach-metafelder"></a>

## Sprach-Metafelder

Außer für Kategorien und Medien bietet REDAXO auch für Sprachen Metafelder. Denkbar wäre, Sprach-Metafelder anzulegen für einen alternativen Navigations-Sprachnamen, z.B. DE oder EN.

Das standardmäßig vorhandene Sprach-Metafeld `Code` kann sinnvoll genutzt werden, z.B. zum Verwalten des Sprachattributs im html-Tag:

```php
<html lang="<?php echo rex_clang::getCurrent()->getCode(); ?>">
```

Oder man könnte ein neues Sprach-Metafeld `setlocale` anlegen und damit in PHP die Lokalisierung definieren, um regional individuelle Datumsangaben und Dezimaltrennzeichen zu erhalten:

```php
setlocale (LC_ALL, rex_clang::getCurrent()->getValue('clang_setlocale'));
```

<a name="beispiel-sprachnavigation"></a>

## Beispiel einer einfachen Sprachnavigation

Das folgende Beispiel zeigt einen automatisch generierten Sprachumschalter.

Bei nur zwei Sprachen wird nur ein Link zur anderen Sprache angezeigt. Als Linktext wird das Meta-Sprachfeld `Name` verwendet. Bei mehr als zwei Sprachen werden Links zu allen Sprachen angezeigt, wobei die aktuelle Sprache nicht verlinkt wird.

```php
<?php
    // auskommentieren, um das Sprach-Array anzuzeigen
    // dump(rex_clang::getAll());


    // zwei Sprachen online -> nur den Link zur anderen Sprache anzeigen
    if (count(rex_clang::getAll(true)) == 2) {

    foreach (rex_clang::getAll(true) as $lang) {
    // falls die Sprache nicht die aktuelle Sprache ist
    if (rex_clang::getCurrentId() != $lang->getValue('id')) {
    echo '<a href="'.rex_getUrl($this->getValue('article_id'), $lang->getValue('id')).'">'.$lang->getValue('code').'</a>';
    }
    }

    // mehr als zwei Sprachen online
    } elseif (count(rex_clang::getAll(true)) > 2) {
    
    foreach (rex_clang::getAll(true) as $lang) {
    // aktuelle Sprachenicht klickbar
    if (rex_clang::getCurrentId() == $lang->getValue('id')) {
    echo '<a href="#">'.$lang->getValue('name').'</a>';
    // alle anderen klickbar
    } else {
    echo '<a href="'.rex_getUrl($this->getValue('article_id'), $lang->getValue('id')).'">'.$lang->getValue('name').'</a>';
    }
    }

    }
?>
```

<a name="beispiel-nuronline"></a>

## Beispiel Sprachnavigation zeigt nur aktive Sprachen

```php
<?php
    // aktuelle Sprache ermitteln
    $current_lang = rex_clang::getCurrent();
    // Sprachcode ermitteln
    $langcode     = $current_lang->getCode();
    // gibt es mehr als eine Sprache?

    if (count(rex_clang::getAll(true)) > 1) {
        if (count(rex_clang::getAll(true))) {
            // Sprachen auslesen
            foreach (rex_clang::getAll(true) as $lang) {
                // aktuelle Sprache soll nicht klickbar sein
                if (rex_clang::getCurrentId() == $lang->getValue('id')) {
                    echo '<strong>' . $lang->getCode() . '</strong>';
                    // alle anderen klickbar
                } else {
            // ermittle Artikel-Infos der ermittelten Sprache
                    $art = rex_article::get($this->getValue('article_id'), $lang->getValue('id'));
                    // prüfen ob Artikel online, wenn ja anzeigen.
                    if ($art->isOnline()) {
                        echo '<a href="' . rex_getUrl($this->getValue('article_id'), $lang->getValue('id')) . '">' . $lang->getCode() . '</a>';
                    }
                }
            }
        }
    }
?>
```

<a name="hilfreiche-addons"></a>

## Hilfreiche AddOns

Das AddOn **Sprog** leistet bei der Arbeit mit mehrsprachigen Websites unschätzbare Dienste. Mittels Platzhalter können sprachabhängige Ersetzungen realisiert werden. Auch kann eine Sprache die Ersetzungen einer anderen Sprache verwenden.

Sprog kann außerdem Artikelnamen und Kategoriename innerhalb derselben Sprache sowie die Metadaten oder das Template zwischen den Sprachen synchronisieren. Und: Inhalte lassen sich rasch von einer Sprache zur anderen Sprache kopieren.

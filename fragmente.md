# Fragmente

- [Prinzip der Fragmente](#prinzip)
- [Variablen in Fragmenten](#variablen)
- [REDAXO-Fragmente nutzen](#fragmente-nutzen)
- [Subfragmente](#subfragmente)
- [Beispiel Paginierung](#paginierung)
    - [Modulausgabe für die Paginierung](#ausgabe-paginierung)
- [REDAXO-Fragmente überschreiben](#fragmente-ueberschreiben)
  - [Beispiel: Eigene Fehlerseiten erstellen](#fehlerseiten)
  - [Beispiel: Anmeldeseite (Login) individualisieren](#login)
  - [Artikel-Blockauswahl anpassen](#block)

<a name="prinzip"></a>

## Prinzip der Fragmente

Fragmente werden in REDAXO eingesetzt, um wiederkehrende Code-Schnipsel übersichtlich zu verwalten. Fragmente sind PHP-Dateien und werden bei der Ausgabe geparst, sodass Variablen ausgegeben und verarbeitet werden können. In REDAXO selbst werden zahlreiche Fragmente für die Ausgabe des Backends verwendet. Diese Fragmente können auch als Ausgangsbasis für eigene Fragmente genutzt werden. Grundsätzlich wird ein Fragment in dieser Form angesprochen und ausgegeben:

```php
$fragment = new rex_fragment();
echo $fragment->parse('meinfragment.php');
```

Fragmente, die in AddOns im Verzeichnis `fragments` abgelegt werden, werden ohne Pfadangabe gefunden.

<a name="variablen"></a>

## Variablen in Fragmenten

Fragmente können Variablen ausgeben, die zuvor dem Fragment per `setVar` zugewiesen wurden.

```php
$fragment->setVar('meinevar','Ich bin der Inhalt',false);
```

Folgende Variablenbezeichner sind reserviert und können nicht für eigene Definitionen verwendet werden:

- filename
- vars
- decorator
- fragmentDirs

Das Auslesen der Variablen erfolgt per

```php
$this->meinevar;
```

alternativ:

```php
$this->getVar('meinevar');
```

Wenn eine Variable vom Typ `Array` übergeben wird, so kann dieses Array durchlaufen werden:

    $fragment->setVar('monate',['Januar','Februar','März','April','Mai','Juni','Juli','August','September','...']);

Ausgabe im Fragment:

```php
    <ul>
    <?php foreach ($this->monate as $monat) : ?>
      <li><?= $monat ?></li>
    <?php endforeach ?>
    </ul>
```

<a name="fragmente-nutzen"></a>

## REDAXO-Fragmente nutzen

Die in REDAXO vorliegenden Fragmente können für die eigene Ausgabe im Frontend oder im Backend genutzt werden.

<a name="subfragmente"></a>

## Subfragmente 

`getSubfragment('path/to/file.php')`

Ein Fragment kann ebenfalls Fragmente aufrufen und die sich darin befindlichen Parameter an die Subfragmente übergeben. 
Dies hat den Vorteil, dass man im Fragment auf Logik zur Übergabe verzichten kann. Ein Beispiel dafür ist das Fragment für die [Artikel-Blockauswahl]. 
Hier gibt es ein Zwischenfragment, welches alle Informationen an ein Subfragment übergibt. So kann dieses Zwischenfragment durch z.B. AddOns überschrieben werden, um die Daten darin zu verändern und ggf. wieder an die eigentliche Ausgabe des Subfragments übergeben. 

**Beispiel***
```php 
$this->subfragment('/core/dropdowns/dropdown.php');
```

<a name="paginierung"></a>

### Beispiel Paginierung

Bei der Ausgabe von Datensätzen oder längeren Listen wird häufig eine Paginierung verwendet. Eine Paginierung steht in REDAXO bereits zur Verfügung. Diese Paginierung kann für eigene Zwecke verwendet und angepasst werden.

<a name="ausgabe-paginierung"></a>

#### Modulausgabe für die Paginierung

```php
// Anzahl Datensätze pro Seite
    $rows_per_page = 15;

    if ("REX_VALUE[1]") {
       $sql = rex_sql::factory();

       // Select für alle anzuzeigenden Datensätze
       $qry = "SELECT name, shorttext, id FROM rex_meinetabelle";
       $sql->setQuery($qry);

       // Anzahl Zeilen insgesamt (
       $rows = $sql->getRows();

       // Query erweitern um Anzahl der Datensätze pro Seite
       $qry .= ' LIMIT '.$rows_per_page;

       // Wenn nicht die erste Seite angezeigt wird, Offset an Query anhängen
       if (rex_get('start','int',0)) {
          $qry .= ' OFFSET '.rex_get('start','int',0);
       }

       // $res wird später für die Anzeige der Liste durchlaufen
       $sql->setQuery($qry);
       $res = $sql->getArray();
    }

    // Neues Paginierungsobjekt erstellen
    $pager = new rex_pager($rows_per_page);

    // Gesamtanzahl der Zeilen zuweisen
    $pager->setRowCount($rows);

    // Neues Fragment Objekt erstellen
    $fragment = new rex_fragment();

    // pager Objekt an Fragment übergeben
    $fragment->setVar('pager', $pager, false);

    // urlprovider definieren
    $fragment->setVar('urlprovider', rex_article::getCurrent());

    // Paginierung ausgeben
    echo $fragment->parse('core/navigations/pagination.php');

```

Hierbei wird das Fragment `/core/fragments/core/navigations/pagination.php` für die Ausgabe verwendet. Dieses Fragment kann auch in ein eigenes AddOn in das Verzeichnis `fragments/core` kopiert und geändert werden. Wenn es dort unter dem Namen `mypagination.php` abgelegt wird, so kann es ohne Pfadangabe aufgerufen werden:

```php
echo $fragment->parse('mypagination.php');
```

<a name="fragmente-ueberschreiben"></a>

## REDAXO-Fragmente überschreiben

REDAXO Fragmente können auch überschrieben werden. Es genügt hierbei eine Fragment-Datei mit gleichem Namen in das Fragment-Verzeichnis des eigenen AddOns zu legen. REDAXO lädt bzw. überschreibt die Fragmente in der Reihenfolge, in der AddOns geladen werden. Daher wird das Project-AddOn mit `load late` geladen.

<a name="fehlerseiten"></a>

### Beispiel: Eigene Fehlerseiten erstellen

Seit R5.7 ist es möglich, dass man die "Oooops Fehlerseiten" im Frontend als auch Backend individualisiert.

Die beiden Fehlerseiten sind als Core-Fragment im System enthalten und können z.b. via `fragments` Ordner im Project-AddOn (oder in einem beliebigen anderen AddOn) überschrieben werden.

Es gibt insgesamt 3 Fehlerseiten in REDAXO, davon sind aktuell zwei änderbar:

- Whooops Fehlerseite, die man nur sieht wenn man als Admin im Backend eingeloggt ist. Diese enthält Debugging-Informationen und taucht sowohl im Front- und Backend auf. Sie ist nicht änderbar.

- die ***Oooops Fehlerseite*** im REDAXO-Backend (als Fragment `core/be_ooops.php` überschreibbar), wenn man nicht als Admin user im Backend eingeloggt ist

![Ooops](/assets/v5.7.0-fragmente_ooops.png)

- Die ***Oooops Fehlerseite im Frontend*** (als Fragment `core/fe_ooops.php` überschreibbar), wenn man nicht als Admin-User im Backend eingeloggt ist

![Ooops Frontend ](/assets/v5.7.0-fragmente_ooops_fe.png)

> Eine Fehlerseite sollte eine vollständige HTML-Seite sein (inkl. html, head, body,..), die keine externen Abhängigkeiten enthält (keine externen css-, js- Dateien, Bilder oder Fonts etc).

<a name="login"></a>

### Beispiel: Anmeldeseite (Login) individualisieren

Seit REDAXO 5.12 ist es möglich, die Anmeldeseite mittels Fragmenten zu individualisieren, um beispielsweise ein Hintergrundbild einzubringen oder ein eigenes Logo zu verwenden.

Die Anmeldeseite enthält zwei Core-Fragmente, die innerhalb eines `fragments`-Ordners im Project-AddOn (oder in einem beliebigen anderen AddOn) überschrieben werden können, also etwa so:

**Beispiel Project-AddOn**

* `redaxo/src/addons/project/fragments/core/login_background.php`
* `redaxo/src/addons/project/fragments/core/login_branding.php`

**Beispiel Theme-AddOn**

* `theme/private/fragments/core/login_background.php`
* `theme/private/fragments/core/login_branding.php`

Um hier Anpassungen vorzunehmen, bietet sich an, nicht mit leeren Fragmenten zu beginnen, sondern zunächst die originalen Core-Fragmente aus `/redaxo/src/core/fragments/core` an die richtige Stelle zu kopieren, um auf dessen HTML-Struktur aufzubauen.

Das Background-Fragment enthält das Hintergrundbild und den Footer für die Anmeldeseite. Der Footer ist vor allem deshalb enthalten, um auf die Bildquelle hinweisen zu können (Credits).

Das Branding-Fragment enthält das REDAXO-Logo. Dies kann bei Bedarf ausgetauscht oder um ein weiteres Logo ergänzt werden.

<a name="block"></a>
### Artikel-Blockauswahl anpassen

Die Blockauswahl in der Artikelpflege kann den eigenen Wünschen entsprechend angepasst werden. Hierzu kann man das Fragment `/redaxo/src/addons/structure/plugins/content/fragments/module_select.php`
anpassen. 

Die Blockauswahl nutzt ein das Fragment `module_select.php`, welches Default zum Core-Fragment für Dropdowns durchgeschleift wird.

Möchte man die Blockauswahl im Dropdown verändern oder z.B. eine Info einschleusen, kann man das Fragment anpassen. 

Im `$items` Array werden alle nötigen Informationen zum Aufbau der Blockauswahl geliefert und die Blöcke können so beliebig manipuliert werden. 
Möchte man auf das Standard-Select vom Core verzichten und stattdessen eine eigene Variante erstellen z.B. zur Darstellung von Icons. Entfernt man das Subfragment und erzeugt eine eigene Logik. 

#### Inhalt der module_select.php

```php
/**
 * Discussion Issue #1174
 * Manipulate this fragment to influence the selection of modules on the slice.
 * By default the core fragment is used.
 *
 * @var bool $block
 * @var string $button_label
 * @var array $items           array contains all modules
 *                  [0]          the index of array
 *                      [id]     the module id
 *                      [title]  the module name
 *                      [href]   the module url
 */

$this->subfragment('/core/dropdowns/dropdown.php');
```

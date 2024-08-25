# REDAXO-Variablen

* [Einführung](#einführung)
* [Allgemeine Parameter](#allgemeine-parameter)
* [Modul Ein- und Ausgabe-Variablen](#ein-ausgabe-variablen)
  + [REX_LINK und REX_LINKLIST](#rex-link)
  + [REX_MEDIA und REX_MEDIALIST](#rex-media)
  + [REX_VALUE](#rex-value)
  + [Auslesen der Werte via PHP](#viaphp)
* [Ausgabe-Variablen](#ausgabe-variablen)
  + [REX_ARTICLE](#rex-article)
  + [REX_ARTICLE_ID](#rex-article-id)
  + [REX_CATEGORY](#rex-category)
  + [REX_CATEGORY_ID](#rex-category-id)
  + [REX_CLANG](#rex-clang)
  + [REX_CLANG_ID](#rex-clang-id)
  + [REX_CONFIG](#rex-config)
  + [REX_CTYPE_ID](#rex-ctype-id)
  + [REX_MODULE_ID](#rex-module-id)
  + [REX_MODULE_KEY](#rex-module-key)
  + [REX_PROPERTY](#rex-property)
  + [REX_SLICE_ID](#rex-slice-id)
  + [REX_TEMPLATE](#rex-template)
  + [REX_TEMPLATE_ID](#rex-template-id)
  + [REX_TEMPLATE_KEY](#rex-template-key)
  + [REX_USER_ID](#rex-user-id)
  + [REX_USER_LOGIN](#rex-user-login)
* [Verschachtelte Variablen](#verschachtelung)
* [Callback](#callback)
* [Eigene Variablen](#eigene-variablen)

<a name="einführung"></a>

## Einführung

Um das Einbinden von dynamischen Daten innerhalb von Modulen und Templates zu erleichtern, bietet REDAXO spezielle Elemente an. Über diese **REDAXO-Variablen** genannten Elemente wird der Zugriff auf vom CMS bereitgestellte Daten und die im Backend eingegebenen Inhalte organisiert.

* Mithilfe von REDAXO-Variablen ist es möglich, einfache Templates und Module ohne PHP-Kenntnisse zu erstellen.
* REDAXO-Variablen können vom Core und von AddOns zur Verfügung gestellt werden.
* Viele REDAXO-Variablen erlauben die Angabe von Parametern, um den Datenzugriff und die Ausgabe zu steuern. Diese Daten werden in eckigen Klammern an die Variablen angehängt. Parameter müssen im Format `name=wert` angegeben werden.

**Es gibt zwei Typen von Variablen:**

1. Ein- und Ausgabe-Variablen. Sie bestehen jeweils aus zwei Komponenten: der Eingabe-Variable, mit der die Daten im Eingabebereich eines Moduls angenommen werden und der Ausgabe-Variable, die im Ein- und im Ausgabebereich der Module die gespeicherten Inhalte zurückgibt.
2. Reine Ausgabe-Variablen, mit denen Daten des CMS im Ein- und Augabebereich ausgegeben werden können.

----
**Hinweis:** Da REDAXO Variablen vom CMS vor der Laufzeit in PHP kompiliert werden, wirken sie auf PHP wie Platzhalter. Obwohl die Syntax an ein Array erinnert, ist es daher z. B. nicht möglich, mehrere Variablen über eine for-next-Schleife abzurufen:

``` php
// Falsch:
for ($i = 1; $i <= 5; $i++) {
echo '<p>REX_VALUE['.$i.']</p>';
}

// Richtig
$values = [
    REX_VALUE[1],
    REX_VALUE[2],
    REX_VALUE[3],
    REX_VALUE[4],
    REX_VALUE[5]
        ];
for ($i = 1; $i <= 5; $i++) {
     echo '<p>'.$values[$i].'</p>';
}
```

<a name="allgemeine-parameter"></a>

## Allgemeine Parameter

Allen REDAXO-Variablen, die Parameter akzeptieren (erkennbar den den eckigen Klammern `[]` ), kann einer der folgenden Parameter optional übergeben werden:

| Parameter      | Beschreibung                                                                                                                          |
|----------------|---------------------------------------------------------------------------------------------------------------------------------------|
| `callback=xyz` | Der Variableninhalt wird an eine PHP-Funktion `xyz` übergeben, durch die der Variableninhalt vor der Ausgabe manipuliert werden kann. |
| `prefix=xyz` | Erlaubt zusätzliche Ausgaben vor der Variable.                                                                                        |
| `suffix=xyz` | Erlaubt zusätzliche Ausgaben nach der Variable.                                                                                       |
| `instead=xyz` | Der Inhalt `xyz` wird statt der Variable ausgegeben, wenn diese nicht leer ist.                                                       |
| `ifempty=xyz` | Der Inhalt `xyz` wird ausgegeben, wenn die Variable leer ist.                                                                         |

An die Parameter können auch weitere Variablen übergeben werden. Somit ist eine [Verschachtelung](#verschachtelung) möglich. 
Darüber hinaus können auch eigene Parameter übergeben werden, die über einen [Callback](#callback) verarbeitet werden können. 


<a name="ein-ausgabe-variablen"></a>

## 1. Eingabe- und Ausgabe-Variablen

Über diese Variablen wird der wesentliche Teil aller redaktionellen Inhalte in REDAXO verwaltet.
Im Eingabebereich eines Moduls nehmen sie Inhalte auf, die in die Datenbank geschrieben werden. Im Ausgabebereich stellen sie diese Inhalte zur Weiterverarbeitung und Ausgabe zur Verfügung.

<a name="rex-link"></a>

### REX_LINK und REX_LINKLIST

`REX_LINK` und `REX_LINKLIST` ermöglichen das Einfügen von Links zu REDAXO-Artikeln über ein eine *Linkmap*.

Mit `REX_LINK` wird ein einzelner Artikel-Link eingefügt, `REX_LINKLIST` erlaubt das Einfügen mehrerer Artikel-Links.

**Hinweis:** Wird vom AddOn `structure` bereitgestellt.

### REX_LINK als Eingabe-Variable

Gibt im Backend ein Eingabe-Widget aus, über das die Linkmap aufgerufen wird.

``` php
// Kurze Schreibweise
REX_LINK[id=i widget=1]
// Ausführliche Schreibweise
REX_LINK[id=i widget=1 category=i]
```

| Parameter    | Beschreibung                                                                    |
|--------------|---------------------------------------------------------------------------------|
| `id=i` , `i` | Die ID der Variable. Es sind Werte von 1 bis 10 erlaubt.                        |
| `widget=1` | Erzeugt das Eingabe-Widget.                                                     |
| `category=i` | ID der Kategorie, die beim Öffnen der Linkmap angezeigt werden soll (optional). |

### REX_LINK als Ausgabe-Variable

Gibt die ID oder die URL des gewählten Artikels zurück. Es ist eine gekürzte Schreibweise erlaubt.

    // Kurze Schreibweise
    REX_LINK[i]
    // Ausführliche Schreibweise
    REX_LINK[id=i output=xyz] 
    REX_LINK[id=i isset=1] 

| Parameter    | Beschreibung                                                                                                                     |
|--------------|----------------------------------------------------------------------------------------------------------------------------------|
| `id=i` , `i` | Die ID der Variable. Es sind Werte von 1 bis 10 für `i` erlaubt.                                                                 |
| `isset=1` | Fragt ab, ob die REDAXO-Variable gesetzt ist (optional). Ist sie gesetzt, wird `true` zruückgegeben, sonst `false` .              |
| `output=xyz` | Bestimmt die Art des Rückgabewerts (optional). `output=url` bestimmt die URL des Artikels als Rückgabewert, `output=id` die ID. |

**Beispiel in der Modul-Eingabe**

``` html
REX_LINK[id=1 widget=1]
```

**Beispiel in der Modul-Ausgabe**

``` html
<a href="REX_LINK[id=1 output=url]">zum Artikel mit der ID REX_LINK[id=1]</a>
```

#### REX_LINKLIST als Eingabe-Variable

Gibt im Backend ein Eingabe-Widget aus, über das die Linkmap aufgerufen wird.

``` html
// Ausführliche Schreibweise
REX_LINKLIST[id=i widget=1]
REX_LINKLIST[id=i widget=1 category=i]
```

| Parameter    | Beschreibung                                                                    |
|--------------|---------------------------------------------------------------------------------|
| `id=i` , `i` | Die ID der Variable. Es sind Werte von 1 bis 10 erlaubt.                        |
| `widget=1` | Erzeugt das Eingabewidget.                                                      |
| `category=i` | ID der Kategorie, die beim Öffnen der Linkmap angezeigt werden soll (optional). |

**Beispiel in der Modul-Eingabe**

``` 
REX_LINKLIST[id=1 widget=1]
```

**Beispiel in der Modul-Ausgabe**

``` php
<?php foreach (explode(',', 'REX_LINKLIST[id=1]') as $article_id): ?>
<a href="<?=rex_getUrl($article_id);?>">zum Artikel mit der ID <?=$article_id;?></a>
<?php endforeach;?>
```

#### REX_LINKLIST als Ausgabe-Variable

Gibt die IDs der gewählten Artikel als kommagetrennten String zurück. Es ist eine gekürzte Schreibweise erlaubt.

``` html
// Kurze Schreibweise
REX_LINKLIST[i]
// Ausführliche Schreibweise
REX_LINKLIST[id=i isset=1]
```

| Parameter    | Beschreibung                                                                                                        |
|--------------|---------------------------------------------------------------------------------------------------------------------|
| `id=i` , `i` | Die ID der Variable. Es sind Werte von 1 bis 10 erlaubt.                                                            |
| `isset=1` | Fragt ab, ob die REDAXO-Variable gesetzt ist (optional). Ist sie gesetzt, wird `true` zruückgegeben, sonst `false` . |

<a name="rex-media"></a>

### REX_MEDIA und REX_MEDIALIST

Mit `REX_MEDIA` und `REX_MEDIALIST` können im Eingabebereich über ein Widget Medien aus dem Medienpool ausgewählt werden. So ist es möglich, z. B. Bilder oder Links zu Dokumenten in den Inhalt einzufügen.

Durch `REX_MEDIA` wird nur eine Datei eingefügt, durch `REX_MEDIALIST` ist das Einfügen einer beliebigen Zahl von Dateien möglich.

*Wird vom AddOn `mediapool` bereitgestellt.*

#### REX_MEDIA als Eingabe-Variable

Gibt im Backend ein Eingabe-Widget aus.

``` html
// Kurze Schreibweise
REX_MEDIA[id=i widget=1]
// Ausführliche Schreibweise
REX_MEDIA[id=i widget=1 category=xyz types=xyz preview=1]
```

| Parameter    | Beschreibung                                                                                                                                                                                |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `id=i` , `i` | Die ID der Variable. Es sind Werte von 1 bis 10 erlaubt.                                                                                                                                    |
| `widget=1` | Erzeugt das Eingabewidget.                                                                                                                                                                  |
| `preview=1` | Aktiviert eine Voransicht im Widget (optional).                                                                                                                                             |
| `category=i` | Beschränkt die Auswahl auf die Medienkategorie `i` (optional).                                                                                                                              |
| `types=xyz` | Beschränkt die Auswahl auf bestimmte Dateitypen (optional). Es können mehrere Typen kommagetrennt übergeben werden *(Achtung: es dürfen keine Leerzeichen in der Übergabe enthalten sein)*. |

#### REX_MEDIA als Ausgabe-Variable

Gibt den Dateinamen eines Mediums zurück. Wird nur die ID angegeben, ist eine gekürzte Schreibweise erlaubt.

``` html
// Kurze Schreibweise
REX_MEDIA[i]
// Ausführliche Schreibweise
REX_MEDIA[id=i]
REX_MEDIA[id=i field=xyz]
REX_MEDIA[id=i output=mimetype]
```

| Parameter         | Beschreibung                                                                                                             |
|-------------------|--------------------------------------------------------------------------------------------------------------------------|
| `id=i` , `i` | Die ID der Variable. Es sind Werte von 1 bis 10 erlaubt.                                                                 |
| `field=xyz` | Abrufen eines Metadatenfeldes `xyz` (optional). Statt des Dateinamens wird der Inhalt des Metadatenfeldes zurückgegeben. |
| `output=mimetype` | Statt des Dateinamens wird der Medientyp der Datei zurückgegeben (optional).                                             |

**Beispiel in der Modul-Eingabe**

``` html
REX_MEDIA[id=1 widget=1]
```

**Beispiel in der Modul-Ausgabe**

``` html
<img src="/media/REX_MEDIA[id=1]" alt="Bild" />
```

#### REX_MEDIALIST als Eingabe-Variable

Gibt im Backend ein Eingabe-Widget aus.

``` html
// Ausführliche Schreibweise
REX_MEDIALIST[id=i widget=1]
REX_MEDIALIST[id=i widget=1 category=xyz types=xyz preview=1]
```

| Parameter    | Beschreibung |
|--------------|--------------|
| `id=i` , `i` | Die ID der Variable. Es sind Werte von 1 bis 10 erlaubt. |
| `widget=1` | Erzeugt das Eingabewidget. |
| `preview=1` | Aktiviert eine Voransicht im Widget (optional). |
| `category=i` | Beschränkt die Auswahl auf die Medienkategorie `i` (optional). |
| `types=xyz` | Beschränkt die Auswahl auf bestimmte Dateitypen (optional). Es können mehrere Typen kommagetrennt übergeben werden *(Achtung: es dürfen keine Leerzeichen in der Übergabe enthalten sein)*. |

#### REX_MEDIALIST als Ausgabe-Variable

Gibt die Dateinamen der gespeicherten Medien als kommagetrennten String zurück. Es ist eine gekürzte Schreibweise erlaubt.

```txt
// Kurze Schreibweise
REX_MEDIALIST[i]
// Ausführliche Schreibweise
REX_MEDIALIST[id=i] 
```

| Parameter    | Beschreibung                                             |
|--------------|----------------------------------------------------------|
| `id=i` , `i` | Die ID der Variable. Es sind Werte von 1 bis 10 erlaubt. |

**Beispiel in der Modul-Eingabe**

``` html
REX_MEDIALIST[id=1 widget=1]
```

**Beispiel in der Modul-Ausgabe**

``` php
<?php foreach (explode(',', REX_MEDIALIST[id=1]) as $image): ?>
    <img src ="/media/<?=$image;?>" alt="Bild" />
<?php endforeach;?>
```

<a name="rex-value"></a>

### REX_VALUE

In `REX_VALUE` können alle möglichen Inhalte gespeichert werden. Sie ist daher die am häufigsten eingesetzte REDAXO-Variable.
Inhalte werden mit `REX_INPUT_VALUE` aus üblichen HTML-Formularen übernommen. Mit `REX_VALUE` werden diese Inhalte abgerufen und könnne mit PHP weiterverarbeitet oder über HTML direkt ausgegeben werden.

**Hinweis:** Wird vom `structure` -Plugin `content` bereitgestellt.*

#### REX_VALUE als Eingabe-Variable

Übernimmt den Inhalt eines Formularelements und weist ihn der Variable mit der ID `i` zu. Um mehrere Werte in einer Variable zu speichern, kann die Array-Schreibweise genutzt werden.

``` html
// Kurze Schreibweise
REX_INPUT_VALUE[i]
// Array-Schreibweise
REX_INPUT_VALUE[i][ii][..]
```

| Parameter | Beschreibung                                                                                                                                   |
|-----------|------------------------------------------------------------------------------------------------------------------------------------------------|
| `i` | Die ID der Variable. Es sind Werte von 1 bis 20 erlaubt. Mit der Array-Schreibweise ist es möglich, mehrere Werte in einer Variable abzulegen. |

#### REX_VALUE als Ausgabe-Variable

Gibt den Inhalt einer Variable zurück. Wird nur die ID angegeben, ist eine gekürzte Schreibweise erlaubt.

``` html
// Kurze Schreibweise
REX_VALUE[i]
// Ausführliche Schreibweise
REX_VALUE[id=i]
REX_VALUE[id=i output=xyz]
// Prüfmodus
REX_VALUE[id=i isset=1]
```

Neben den oben angegeben Parametern sind folgende erlaubt:

| Parameter    | Beschreibung                                                                                                                                                                                                                                                                                                                         |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `id=i` , `i` | Die ID der Variable. Es sind Werte von 1 bis 20 erlaubt. Wird nur die ID angegeben ist es erlaubt `id=i` zu `i` abzukürzen.                                                                                                                                                                                                          |
| `output=xyz` | Das Ausgabeformat (optional). Wird der Parameter weggelassen, werden Steuerzeichen im Inhalt gefiltert. Mit dem Wert `html` wird der Inhalt als HTML interpretiert und zurückgegeben. Mit dem Wert `php` wird der Inhalt als PHP interpretiert. Im Backend wird er als formatierter Quelltext zurückgegeben, im Frontend ausgeführt. |
| `isset=1` | Aktiviert den Prüfmodus. Die Rückgabe ist "true", wenn Inhalt vorhanden ist und "false", wenn die Variable leer validiert, also bisher nicht gesetzt wurde, einen leeren String, "0" oder "null" enthält.                                                                                                                            |

**Beispiel in der Modul-Eingabe**

``` html
<input type="text" name="REX_INPUT_VALUE[1]" value="REX_VALUE[1]" />
```

**Beispiel in der Modul-Ausgabe**

```html
<p>REX_VALUE[1]</p>
```

### Mehrere Werte in einem Feld: Arrays zurückwandeln

Die Zahl der in einem Modul verwendbaren Values ist limitiert, im Falle von REX_VALUE sind es 20 Stück. In sehr seltenen Fällen könnte man noch mehr Felder in einem Modul benötigen. Man erreicht dies, indem man mehrere Werte in einer Variable und diese Variable dann in der Datenbank speichert speichert.

**Modul-Eingabe**

``` html
<input type="text" name="REX_INPUT_VALUE[1][text1]" value="" />
<input type="text" name="REX_INPUT_VALUE[1][text2]" value="" />
```

**Modul-Ausgabe**

``` php
$value1 = rex_var::toArray("REX_VALUE[1]");

echo $value1['text1'];  
echo $value1['text2'];
```

<a name="viaphp"></a>
### Auslesen der Werte via PHP

Die Slice-Values können auch per PHP ausgelesen und verarbeitet werden. 

```php
// Holt das aktuelle Slice-Objekt
$slice = $this->getCurrentSlice();

// Mit folgenden Methoden können die Werte ausgelesen werden

$slice->getValue(1);
$slice->getMedia(1);
$slice->getMediaUrl(1);
$slice->getLinklist(1);
$slice->getLinklist(1);
$slice->getLinkUrl(1);
$slice->getMedialist(1); 
$slice->getValueArray(1); // Alternative für rex_var::toArray('REX_VALUE[1]')
$slice->getMediaListArray(1); // Medialist als Array
$slice->getLinkListArray(1); // Linklist als Array
```
// etc.


<a name="ausgabe-variablen"></a>

## 2. Ausgabe-Variablen

Ausgabe-Variablen bieten nur Lesezugriff. Mit ihrer Hilfe können Daten des CMS im Ein- und Ausgabebereich abgerufen werden.
Einige sind Shortcuts für vorhandene PHP-Befehle.

<a name="rex-article"></a>

### REX_ARTICLE

Mit `REX_ARTICLE` werden die Inhalte eines Artikels abgerufen.
Die Feldabfragen sind Shortcuts für `rex_article::getCurrent()->getValue($field)` und `rex_article::getId($id)->getValue($field)` . Die Ausgabe wird dabei stets durch `htmlspecialchars` gefiltert.
Die Inhaltsabfragen sind Shortcuts für den Zugriff auf `rex_article_content` .

**Hinweis:** Wird vom AddOn `structure` bereitgestellt.

#### Syntax

```html
// Kurze Schreibweise
REX_ARTICLE[]
REX_ARTICLE[i]
// Ausführliche Schreibweise
REX_ARTICLE[id=i]
REX_ARTICLE[id=i ctype=i clang=i]
REX_ARTICLE[id=i field=xyz clang=i]
```

| Parameter    | Beschreibung                                                                                                                                                                     |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `id=i` , `i` | Die ID des Artikels (optional). Wird nur die ID angegeben ist es erlaubt `id=i` zu `i` abzukürzen. Wird die ID weggelassen, wird der aktuelle Artikel abgerufen.                 |
| `ctype=i` | Durch die Angabe der ID einer Spalte `ctype` kann die Ausgabe auf den Inhalt dieser Spalte begrenzt werden (optional). Ohne diesen Parameter wird der gesamte Artikel abgerufen. |
| `clang=i` | Ruft den Inhalt oder eines Metadaten-Felds der Sprache `i` ab (optional). Ohne diesen Parameter wird der Inhalt / ein Metadaten-Feld der aktiven Sprache abgerufen.              |
| `field=xyz` | Statt des Artikelinhalts wird der Inhalt des Metadaten-Feldes `xyz` zurückgegeben (optional).                                                                                    |

**Beispiel**

```html
// Spalte 1 von Artikel 5 in Sprache 2 abrufen
REX_ARTICLE[id=5 clang=2 ctype=1]
```

<a name="rex-article-id"></a>

### REX_ARTICLE_ID

Liefert die ID des aktiven Artikels. Es sind keine Parameter erforderlich.
Shortcut für `rex_article::getCurrentId()` .

**Hinweis:** Wird vom `structure` -Plugin `content` bereitgestellt.*

Wird innerhalb eines Artikels ein anderer Artikel über `rex_article_content` eingebunden, unterscheidet sich die Rückgabe von `rex_article::getCurrentId()` und `REX_ARTICLE_ID` :

* `rex_article::getCurrentId()` gibt stets die ID des einbindenden Artikels zurück, auch beim Aufruf im eingebundenen Artikel
* `REX_ARTICLE_ID` gibt jeweils die ID des Artikels zurück, in dem es aufgerufen wird

#### Syntax

```html
REX_ARTICLE_ID
```

<a name="rex-category"></a>

### REX_CATEGORY

Mit `REX_CATEGORY` werden die Inhalte einer Kategorie abgerufen.
Shortcut für `rex_category::getCurrent()->getValue($field)` und `rex_category::getId($id)->getValue($field)` . Die Ausgabe wird dabei stets durch `htmlspecialchars` gefiltert.

**Hinweis:** Wird vom AddOn `structure` bereitgestellt.*

#### Syntax

```html
// Kurze Schreibweise
REX_CATEGORY[xyz]
// Ausführliche Schreibweise
REX_CATEGORY[id=i field=xyz]
REX_CATEGORY[id=i field=xyz clang=i]
```

| Parameter    | Beschreibung                                                                                                                        |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------|
| `field=xyz` | Gibt den Inhalt des Metadaten-Feldes `xyz` zurück.                                                                                  |
| `id=i` , `i` | Die ID der Kategorie (optional). Wird die ID weggelassen, wird die aktuelle Kategorie abgerufen.                                    |
| `clang=i` | Ruft ein Metadaten-Feld der Sprache `i` ab (optional). Ohne diesen Parameter wird ein Metadaten-Feld der aktiven Sprache abgerufen. |

**Beispiel**

```html
// Feld 'title' der Kategorie 5 abrufen
REX_CATEGORY[id=5 field=title]
```

<a name="rex-category-id"></a>

### REX_CATEGORY_ID

Liefert die ID der aktiven Kategorie. Es sind keine Parameter erforderlich.
Shortcut für `rex_category::getCurrentId()` .

**Hinweis:** Wird vom `structure` -Plugin `content` bereitgestellt.*

#### Syntax

```text
REX_CATEGORY_ID
```

<a name="rex-clang"></a>

### REX_CLANG

Ermöglicht den Zugriff auf die Metadaten-Felder der Ausgabe-Sprachen im Frontend.
Shortcut für `rex_clang::getCurrent()->getValue($field)` und `rex_clang::getId($id)->getValue($field)` . Die Ausgabe wird dabei stets durch `htmlspecialchars` gefiltert.

**Hinweis:** Wird vom REDAXO-Core bereitgestellt.*

#### Syntax

```html
REX_CLANG[id=i field=xzy]
```

| Parameter   | Beschreibung                                |
|-------------|---------------------------------------------|
| `id=i` | die ID der Sprache, die Angabe ist optional |
| `field=xyz` | Das auszugebende Metadaten-Feld             |

<a name="rex-clang-id"></a>

### REX_CLANG_ID

Liefert die ID der aktiven Frontend-Sprache. Es sind keine Parameter erforderlich.
Shortcut für `rex_clang::getCurrentId()` .

**Hinweis:** Wird vom `structure` -Plugin `content` bereitgestellt. Die erste Sprache ist die Id 1.

#### Syntax

``` 
REX_CLANG_ID
```

<a name="rex-config"></a>

### REX_CONFIG

Erlaubt den Zugriff auf Datenfelder der REDAXO-Konfigurationstabelle.
Shortcut für `rex_config::get($namespace, $key)` . Die Ausgabe wird dabei stets durch `htmlspecialchars` gefiltert.

**Hinweis:** Wird vom REDAXO-Core bereitgestellt.

#### Syntax

```html
REX_CONFIG[namespace=xyz key=xyz]
```

| Parameter       | Beschreibung                                                                                            |
|-----------------|---------------------------------------------------------------------------------------------------------|
| `namespace=xyz` | der Namespace der Konfiguration, meistens der Name des AddOns oder `namespace=core` für den REDAXO-Core |
| `key=xyz` | das abzurufende Datenfeld                                                                               |

<a name="rex-ctype-id"></a>

### REX_CTYPE_ID

Liefert die ID der aktiven Artikel-Spalte. Es sind keine Parameter erforderlich. Ist nur innerhalb von Modulen verfügbar.

**Hinweis:** Wird vom `structure` -Plugin `content` bereitgestellt.

#### Syntax

``` 
REX_CTYPE_ID
```

<a name="rex-module-id"></a>

### REX_MODULE_ID

Liefert die ID des aktiven Moduls. Es sind keine Parameter erforderlich und es ist nur innerhalb von Modulen verfügbar.

**Hinweis:** Wird vom `structure` -Plugin `content` bereitgestellt.

#### Syntax

``` 
REX_MODULE_ID
```

<a name="rex-module-key"></a>

### REX_MODULE_KEY

Liefert den Key des aktiven Moduls. Es sind keine Parameter erforderlich und es ist nur innerhalb von Modulen verfügbar.

**Hinweis:** Wird vom `structure` -Plugin `content` bereitgestellt.

#### Syntax

``` 
REX_MODULE_KEY
```

<a name="rex-property"></a>

### REX_PROPERTY

Bietet Zugriff auf die in den `package.yml` der AddOns und in der `config.yml` des Cores definierten Datenfelder.
Shortcut für `rex_package::get($namespace)->getProperty($key)` und `rex::getProperty($key)` . Die Ausgabe wird dabei stets durch `htmlspecialchars` gefiltert.

**Hinweis:** Wird vom REDAXO-Core bereitgestellt.

#### Syntax

```html
REX_PROPERTY[namespace=xyz key=xyz]
```

| Parameter       | Beschreibung                                                                                         |
|-----------------|------------------------------------------------------------------------------------------------------|
| `namespace=xyz` | der Name des AddOns – wird kein Namespace angegeben, wird auf die Daten des REDAXO-Core zugegriffen. |
| `key=xyz` | das abzurufende Datenfeld                                                                            |

<a name="rex-slice-id"></a>

### REX_SLICE_ID

Liefert die ID des aktiven Blocks (Slice). Es sind keine Parameter erforderlich. Ist nur innerhalb von Modulen verfügbar.

**Hinweis:** Wird vom `structure` -Plugin `content` bereitgestellt.

#### Syntax

``` 
REX_SLICE_ID
```

<a name="rex-template"></a>

### REX_TEMPLATE

Mit `REX_TEMPLATE` wird ein Template abgerufen. Shortcut für `$template = new rex_template($templateId); echo $template->getTemplate();` bzw. `$template = rex_template::forKey($templateKey); echo $template->getTemplate();` .

**Hinweis:** Wird vom `structure` -Plugin `content` bereitgestellt.

#### Syntax

**Bei Verwendung eines Keys**

``` php
REX_TEMPLATE[key=string]
```

der aktuell verwendete Key kann mittels

**Bei Verwendung der ID**

``` php
// Kurze Schreibweise
REX_TEMPLATE[i]
// Ausführliche Schreibweise
REX_TEMPLATE[id=i]
```

| Parameter               | Beschreibung          |
|-------------------------|-----------------------|
| `key=string` , `string` | Key des Templates     |
| `id=i` , `i` | Die ID des Templates. |

<a name="rex-template-id"></a>

### REX_TEMPLATE_ID

Liefert die ID des aktiven Templates. Es sind keine Parameter erforderlich.

**Hinweis:** Wird vom `structure` -Plugin `content` bereitgestellt.

<a name="rex-template-key"></a>

### REX_TEMPLATE_KEY

Liefert den Key des aktiven Templates. Es sind keine Parameter erforderlich.

**Hinweis:** Wird vom `structure` -Plugin `content` bereitgestellt.

#### Syntax

``` 
REX_TEMPLATE_ID
```

<a name="rex-user-id"></a>

### REX_USER_ID

Liefert die ID des eingeloggten Backend-Users. Wenn kein Backend-User eingeloggt ist, bleibt sie leer. Es sind keine Parameter erforderlich.
Shortcut für `rex::getUser()->getId()` .

**Hinweis:** Wird vom `structure` Plugin `content` bereitgestellt.

#### Syntax

``` 
REX_USER_ID
```

<a name="rex-user-login"></a>

### REX_USER_LOGIN

Liefert den Login-Namen des eingeloggten Backend-Users. Wenn kein Backend-User eingeloggt ist, bleibt sie leer. Es sind keine Parameter erforderlich.
Shortcut für `rex::getUser()->getLogin()` .

**Hinweis:** Wird vom `structure` Plugin `content` bereitgestellt.

#### Syntax

``` 
REX_USER_LOGIN
```


<a name="verschachtelung"></a>

## Verschachtelte Variablen

Variablen können ineinander verschachtelt werden. Dabei übergibt man den Parametern einer Variable weitere Variablen. 

Beispiel: 

```
REX_VALUE[prefix=<REX_VALUE[2]> id=1 suffix=</REX_VALUE[2]> ifempty=REX_ARTICLE[field=name]] 
```
Hier wird eine Überschrift generiert. Falls kein Inhalt für den Value 1 übergeben wurde, wird stattdessen der Artikelname genommen. 


<a name="callback"></a>

## Augabe der Variablen per Callback verarbeiten 

Der Variableninhalt wird an eine PHP-Funktion oder Class-Methode `xyz` übergeben, durch die der Variableninhalt vor der Ausgabe manipuliert werden kann.

### Beispiel:

PHP Class

```php
class var_info
{
 public static function getInfo($data)
    {
        return dump($data);
    }
}
```

Aufruf im Modul

```
REX_VALUE[id=1 callback="var_info::getInfo"  customparameter="foo"] 
```

Die Callback-Methode `getInfo` nimmt alle Inhalte und Parameter als Array der Variable auf. Hier auch den selbst kreierten customparameter. Es wird hier ein Dump ausgegen. 



<a name="eigene-variablen"></a>

## Eigene Variablen

Es ist sehr leicht möglich, eigene REDAXO-Variablen zu erstellen. Hierfür muss lediglich eine PHP-Klasse erstellt und im lib-Verzeichnis eines AddOns (z. B. im Project-AddOn) abgelegt werden. Die Klasse wird automatisch von REDAXO erkannt und eingebunden.
Damit die Klasse erkannt wird, muss sie mit `rex_var_` beginnen und die Basisklasse `rex_var` erweitern. Die Methode `getOutput` muss zwingend vorhanden sein.
Der erzeugten Variable stehen die [allgemeinen Parameter](#allgemeine-parameter) automatisch zur Verfügung. Weitere Parameter lassen sich sehr einfach hinzufügen.

Zur Erleichterung der Implementierung sollte der Debug-Modus aktiviert sein.

### Beispiel

``` php
<?php
/**
 *
 * Erstellt die Variable REX_WEBSITE_TITLE[]. Mit ihr kann der Website-Titel ausgegeben werden.
 * Optional ist es möglich die Ausgabe in Großbuchstaben oder Kleinbuchstaben umzuwandeln.
 *
 * Syntax:
 *     REX_WEBSITE_TITLE[] // Gibt den Titel aus
 *     REX_WEBSITE_TITLE[case=lower] // Gibt den Titel in Kleinbuchstaben aus
 *     REX_WEBSITE_TITLE[case=upper] // Gibt den Titel in Großbuchstaben aus
 */
class rex_var_website_title extends rex_var
{
   protected function getOutput()
   {
       // Website-Titel holen
       $title = rex::getServerName();

       // Prüfen, ob der Parameter 'case' vorhanden ist.
       // Durch ihn kann die Ausgabe manipuliert werden.
       if ($this->hasArg('case') && $this->getArg('case')) {
           switch ($this->getArg('case')) {
               // REX_WEBSITE_TITLE[case=upper]
               case 'upper':
                   $title = strtoupper($title);
                   break;

               // REX_WEBSITE_TITLE[case=lower]
               case 'lower':
                   $title = strtolower($title);
                   break;

               // REX_WEBSITE_TITLE[]
               default:
                   // keine Änderung
           }
       }

       // Reine Textausgaben müssen mit 'self::quote()' als String maskiert werden.
       return self::quote($title);
   }
}
```

**Hinweis:**
Je nachdem, welcher Art die Rückgabedaten sind, müssen sie anders vorbereitet werden:

* Soll ein Array für die direkte Weiterverarbeitung zurückgegeben werden, kann es mit [var_export](http://php.net/manual/de/function.var-export.php) zurückgegeben werden: `return var_export($array);` 
* Ein PHP-Befehl, der erst zur Laufzeit ausgeführt werden soll, muss als String zurückgegeben werden: `return 'strtolower($title)'; // Die Anführungszeichen nicht vergessen` 

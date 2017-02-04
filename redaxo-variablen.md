# REDAXO-Variablen

- [Einführung](#einführung)
- [Ein- und Ausgabe-Variablen](#ein-ausgabe-variablen)
    - [REX_VALUE](#rex-value)
    - [REX_MEDIA und REX_MEDIALIST](#rex-media)
    - [REX_LINK und REX_LINKLIST](#rex-link)
- [Ausgabe-Variablen](#ausgabe-variablen)
    - [REX_CLANG](#rex-clang)
    - [REX_CONFIG](#rex-config)
    - [REX_PROPERTY](#rex-propery)
    - [REX_ARTICLE_ID](#rex-article-id)
    - [REX_CATEGORY_ID](#rex-category-id)
    - [REX_CLANG_ID](#rex-clang-id) 
    - [REX_TEMPLATE_ID](#rex-template-id)
    - [REX_USER_ID](#rex-user-id)
    - [REX_SLICE_ID](#rex-slice-id)
    - [REX_MODULE_ID](#rex-module-id)
    - [REX_CTYPE_ID](#rex-ctype-id)
- [Eigene Variablen](#eigene-variablen)


<a name="einführung"></a>
## Einführung
Um das Einbinden von dynamische Daten innerhalb von Modulen und Templates zu erleichtern, bietet REDAXO spezielle Elemente an. Über diese REDAXO-Variablen genannten Elemente wird der Zugriff auf vom CMS bereitgestellte Daten und die im Backend eingegebenen Inhalte organisiert. 
Mithilfe von REDAXO-Variablen ist es möglich, einfache Templates und Module ohne PHP-Kenntnisse zu erstellen.

* REDAXO-Variablen können vom Core und von AddOns zur Verfügung gestellt werden.
* Viele REDAXO-Variablen erlauben die Angabe von Parametern, um den Datenzugriff und die Ausgabe zu steuern. Diese Daten werden in eckigen Klammern an die Variablen angehängt.
* Es gibt zwei Typen von Variablen: 
    1. Ein- und Augabe-Variablen. Sie bestehen jeweils aus zwei Komponenten: der Eingabe-Variable, mit der die Daten im Eingabebereich eines Moduls angenommen werden und der Ausgabe-Variable, die im Eingabe- und im Ausgabe-Bereich gespeicherte Inhalte zurückgibt. 
    2. Reine Ausgabe-Variablen, mit denen Daten des CMS im Ein- und Augabebereich ausgegeben werden können. 

----
> **Hinweis:** Da REDAXO Variablen vom CMS vor der Laufzeit in PHP kompiliert werden, wirken sie auf PHP wie Platzhalter. Obwohl die Syntax an ein Array erinnern ist es daher z.B. nicht möglich, mehrere Variablen über eine for-next-Schleife abzurufen:

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

<a name="ein-ausgabe-variablen"></a>
### 1. Ein- und Ausgabe-Variablen
Über diese Variablen wird der wesentliche Teil aller redaktionellen Inhalte in REDAXO verwaltet. 
Im Eingabebereich eines Moduls dienen sie zur Übernahme von redaktionellen Eingaben, die in die Datenbank geschrieben werden. Im Ausgabebereich stellen sie diese Daten zur Weiterverarbeitung und Ausgabe zur Verfügung.  

<a name="rex-value"></a>
#### `REX_VALUE`
In `REX_VALUE` können alle möglichen Inhalte gespeichert werden. Sie ist daher die am häufigsten eingesetzte REDAXO-Variable.
Inhalte werden mit `REX_INPUT_VALUE` aus üblichen HTML-Formularen übernommen. Mit `REX_VALUE` werden diese Inhalt abgerufen und könnnen mit PHP weiterverarbeitet  oder über HTML direkt ausgegeben werden.

*Wird vom `structure` Plugin `content` breitgestellt.*

##### Syntax

Ausgabe-Variable | Beschreibung  
--- | ---
`REX_VALUE[i]` | Kurze Schreibweise. Es wird der Inhalt mit der ID `i` zurückgegeben. `i` darf Werte von 1-20 annehmen.
`REX_VALUE[id=i output=xyz]` | Ausführliche Schreibweise. Es wird der Inhalt mit der ID `i` zurückgegeben. Der Parameter `output` ist optional. Ohne den Parameter `output` werden Steuerzeichen im Inhalt gefiltert. Mit dem Parameter `output=html` wird der Inhalt als HTML interpretiert und zurückgegeben. Mit dem Parameter `output=php` wird der Inhalt als PHP interpretiert. Im Backend wird er als formatierter Quelltext zurückgegeben, im Frontend ausgeführt.  
`REX_VALUE[isset=1]` | Abfrage, ob die Variable einen Inhalt hat. Die Rückgabe ist `true`, wenn Inhalt vorhanden ist und `false`, wenn die Variable leer validiert, also bisher nicht gesetzt wurde, einen leeren String, `0` oder `null` enthält. 

Eingabe-Variable | Beschreibung  
--- | ---
`REX_INPUT_VALUE[i]` | Übernimmt den Inhalt eines Formularelements und weist ihn der Variable mit der ID `i` zu.

#####Beispiele
    TODO

<a name="rex-media"></a>
#### `REX_MEDIA` und `REX_MEDIALIST`
Mit `REX_MEDIA` und `REX_MEDIALIST` können im Eingabebereich über ein Widget Medien aus dem Medienpool ausgewählt werden. So ist es möglich, z.B. Bilder oder Links zu Dokumenten in den Inhalt einzufügen. 

Durch `REX_MEDIA` wird nur eine Datei eingefügt, durch `REX_MEDIALIST` ist das Einfügen einer beliebigen Zahl von Dateien möglich.

*Wird vom AddOn `mediapool` bereitgestellt.*


##### Syntax

Ausgabe-Variable | Beschreibung  
--- | ---
`REX_MEDIA[i]` | Kurze Schreibweise. Es wird der Inhalt mit der ID `i` zurückgegeben. `i` darf Werte von 1-10 annehmen.
`REX_MEDIA[id=i]` | Ausführliche Schreibweise. Es wird der Inhalt mit der ID `i` zurückgegeben. `i` darf Werte von 1-20 annehmen. 
`REX_MEDIA[id=i field=xyz]` | Es wird der Inhalt des Metadatenfelds `xyz` des Inhalts mit der ID `i` zurückgegeben.
`REX_MEDIA[id=i output=mimetype]` | Es wird Medientyp des Inhalts mit der ID `i` zurückgegeben.

Eingabe-Variable | Beschreibung  
--- | ---
`REX_MEDIA[id=i widget=1 category=xyz types=xyz preview=1]` | Im Backend wird ein Eingabewidget mit der ID `i` angezeigt. Mit dem Parameter `category` ist optional und kann die Auswahl auf die Medienkategorie `xyz` beschränken. Der Parameter `types` ist ebenfalls optional und kann die Auswahl auf bestimmte Dateitypen beschränken. Es können mehrere Typen kommagetrennt übergeben werden *(Achtung: es dürfen keine Leerzeichen in der Übergabe enthalten sein)*. Mit dem Parameter `preview=1` wird eine Voransicht im Widget aktiviert.

##### Beispiele
    TODO

<a name="rex-link"></a>
#### `REX_LINK` und `REX_LINKLIST[...]`
TODO

<a name="ausgabe-variablen"></a>
### 2. Ausgabe-Variablen
Ausgabe-Variablen bieten nur Lesezugriff. Mit ihrer hilfe können Daten des CMS im Ein- und Augabebereich abgerufen werden.


<a name="rex-clang"></a>
#### `REX_CLANG`
Ermöglicht den Zugriff auf die Metadaten-Felder der Ausgabe-Sprachen im Frontend. 

*Wird vom REDAXO-Core breitgestellt.* 

**Syntax:** `REX_CLANG[id=i field=xzy]`

Parameter | Beschreibung  
--- | ---
`id` | die ID der Sprache, die Angabe ist optional 
`field` | Das auszugebende Metadaten-Feld 

**Shortcut** für `rex_clang::getCurrent()->getValue($field)` und `rex_clang::getId($id)->getValue($field)`. Die Ausgabe wird dabei stets durch `htmlspecialchars` gefiltert. 


<a name="rex-config"></a>
#### `REX_CONFIG`
Erlaubt den Zugriff auf Datenfelder der REDAXO-Konfigurationstabelle. 

*Wird vom REDAXO-Core breitgestellt.* 

**Syntax:** `REX_CONFIG[namespace=xyz key=xzy]`

Parameter | Beschreibung
--- | ---
`namespace` | der Namespace der Konfiguration, meistens der Name des Addons oder `core` für den REDAXO-Core 
`key` | das abzurufende Datenfeld

**Shortcut** für `rex_config::get($namespace, $key)`. Die Ausgabe wird dabei stets durch `htmlspecialchars` gefiltert. 


<a name="rex-property"></a>
#### `REX_PROPERTY`
Bietet Zugriff auf die in den `package.yml` der Addons und in der `config.yml` des Cores definierten Datenfelder. 

*Wird vom REDAXO-Core breitgestellt.* 

**Syntax:** `REX_PROPERTY[namespace=xyz key=xzy]`

Parameter | Beschreibung
--- | --- 
`namespace` | der Name des Addons, wird kein namespace angegeben wird auf die Daten des REDAXO-Core zugegriffen 
`key` | das abzurufende Datenfeld

**Shortcut** für `rex_package::get($namespace)->getProperty($key)` und `rex::getProperty($key)`. Die Ausgabe wird dabei stets durch `htmlspecialchars` gefiltert. 

<a name="rex-article-id"></a>
#### `REX_ARTICLE_ID`
Liefert die ID des aktiven Artikels. Es sind keine Parameter erforderlich.

*Wird vom `structure` Plugin `content` breitgestellt.*

<a name="rex-category-id"></a>
#### `REX_CATEGORY_ID`
Liefert die ID der aktiven Kategorie. Es sind keine Parameter erforderlich.

*Wird vom `structure` Plugin `content` breitgestellt.*

<a name="rex-clang-id"></a>
#### `REX_CLANG_ID`
Liefert die ID der aktiven Frontend-Sprache. Es sind keine Parameter erforderlich.

*Wird vom `structure` Plugin `content` breitgestellt.*

<a name="rex-template-id"></a>
#### `REX_TEMPLATE_ID`
Liefert die ID des aktiven Templates. Es sind keine Parameter erforderlich.

*Wird vom `structure` Plugin `content` breitgestellt.*

<a name="rex-user-id"></a>
#### `REX_USER_ID`
Liefert die ID des eingeloggten Backend-Users. Wenn kein Backend-User eingeloggt ist, bleibt sie leer. Es sind keine Parameter erforderlich.

*Wird vom `structure` Plugin `content` breitgestellt.*

<a name="rex-user-login"></a>
#### `REX_USER_LOGIN`
Liefert den Login-Namen des eingeloggten Backend-Users. Wenn kein Backend-User eingeloggt ist, bleibt sie leer. Es sind keine Parameter erforderlich.

*Wird vom `structure` Plugin `content` breitgestellt.*

<a name="rex-slice-id"></a>
#### `REX_SLICE_ID`
Liefert die ID des aktiven Blocks (Slice). Es sind keine Parameter erforderlich. Ist nur innerhalb von Modulen verfügbar.

*Wird vom `structure` Plugin `content` breitgestellt.*

<a name="rex-module-id"></a>
#### `REX_MODULE_ID`
Liefert die ID des aktiven Moduls. Es sind keine Parameter erforderlich. Ist nur innerhalb von Modulen verfügbar.

*Wird vom `structure` Plugin `content` breitgestellt.*

<a name="rex-ctype-id"></a>
#### `REX_CTYPE_ID`
Liefert die ID der aktiven Artikel-Spalte. Es sind keine Parameter erforderlich. Ist nur innerhalb von Modulen verfügbar.

*Wird vom `structure` Plugin `content` breitgestellt.*


<a name="eigene-variablen"></a>
## Eigene Variablen
Um eine Variable zu erstellen, benötigt Redaxo im lib-Verzeichnis des Addons oder Plugins eine Klasse deren Namen mit `rex_var_` beginnt und die von `rex_var` erbt.

### Beispiel
```
<?php

class rex_var_lorem extends rex_var {
  
  protected function getOutput() {
    return self::quote('Lorem Ipsum!');
  }
}
```

Mit dem oben gezeigten Code, können wir nun die Variable `REX_LOREM[]` verwenden. Die Methode `getOutput();` liefert uns schlussendlich den gewünschten Inhalt als ausführbaren Code. Um einfach nur Text bzw. HTML-Code auszugeben, muss dieser mit der vererbten Methode `self::quote();` als String maskiert werden.
Um ein nutzbares Array auszugeben, kann man das Array mit [var_export](http://php.net/manual/de/function.var-export.php) zurückgegeben werden.
# REDAXO Variablen

Im Quelltext gibt es zwei Möglichkeiten Daten aus einer Datenbank oder von einem Addon zu bekommen. Die eine ist mit PHP und entsprechenden Methoden die zur Verfügung stehen. Die zweite Möglichkeit ist der Einsatz von sogenannten `REX_VARS`. REX_VARS werden von Redaxo in Inhalte umgewandelt.
Neben einer Reihe vordefinierter Standardvariablen, kann jedes Addon weitere Variablen zur Verfügung stellen.

## Standard Variablen

Variable| Beschreibung
--- | ---
`REX_ARTICLE_ID` | Liefert die Artikel ID des aktuell geladenen Artikels.
`REX_SLICE_ID` | Liefert die Slice/Modul ID des aktuell gezeigten Slices/Ausgabe-Modules.
`REX_MODULE_ID` | Liefert die ID des Modules.
`REX_CLANG_ID` | Liefert die ID der aktuell ausgegebenen Sprache
`REX_CATEGORY_ID` | Liefert die Kategorie ID der angezeigten Seite.
`REX_TEMPLATE_ID` | Liefert die ID des Templates, welches für die aktuelle Ausgabe verwendet wird.

## Standard Variablen im Backend

Variable | Beschreibung
--- | ---
`REX_USER_ID` | Liefert die Benutzer ID des angemeldeten Benutzers.
`REX_USER_LOGIN` | Liefert den Login-Namen des angemeldeten Benutzers.


##Speichern & Lesen
In einem Modul kann man nicht direkt auf die Datenbank-Inhalte zugreifen, die Inhalte werden über sogenannte REX_VARS zugänglich.

###Speichern

In den Modlen gibt es zwei Funktionen die es oft zu unterscheiden gilt: Hinzufügen und Aktualisieren. Im Modus Hinzufügen gibt es noch keine Daten aus der Datenbank, um Notices zu verhindern, solltest du an dieser Stelle nicht versuchen Datenbank-Daten in eine PHP-Variable zu laden.

Auch wichtig ist, dass Daten nach dem Speichern nicht zwangsläufig durch SQL erreichbar sind. Ggf. muss an dieser Stelle mit den POST-Daten gearbeitet werden.

###Auslesen

Variable | Optionen | Beschreibung
--- | --- | ---
`REX_VALUE[1-20]` | id=1-20 output=php, html | Liefert die Informationen die mit REX_INPUT_VALUE[1-20] abgespeichert wurde.
`REX_MEDIA[1-10]` | id=1-10 widget=1 | Liefert die Informationen die mit REX_MEDIA[1-10] abgespeichert wurde.
`REX_LINK[1-10]` | id=1-10 widget=1 | Liefert die Informationen die mit REX_LINK[1-10] abgespeichert wurde.
`REX_MEDIALIST[1-10]` | id=1-10 widget=1  | Liefert die Informationen die mit REX_MEDIALIST[1-10] abgespeichert wurde.
`REX_LINKLIST[1-10]` | id=1-10 widget=1 | Liefert die Informationen die mit REX_LINKLIST[1-10] abgespeichert wurde.


## Eigene Variablen
Um eine Variable zu erstellen, benötigt Redaxo im lib-Verzeichnis des Addons oder Plugins eine Klasse deren Namen mit `rex_var_` beginnt und die von `rex_var` erbt.

### Beispiel-Code
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

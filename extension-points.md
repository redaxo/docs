# Extension Points

- [Einsatz eines Extension Points](#einsatz)
- [Eigene Extension Points definieren](#definieren)
- [Core](#core)

Extension Points sind Stellen im REDAXO Programmcode, an denen eigener Code eingeklinkt und ausgeführt werden kann. Dadurch lässt sich auch das Coresystem erweitert werden und anpassen, ohne den Core selbst zu verändern. Extension Points ermöglichen die Manipulation eines bestimmten Wertes, der von der Funktion zurückgegeben wird, die man am Extension Point ausführen lässt.

Die Funktion bekommt an der Stelle der Codeausführung relevante Parameter als Übergabewerte, die sich von Extenstion Point zu Extension Point unterscheiden.

<a name="einsatz"></a>
## Einsatz eines Extension Points

Zunächst sucht man sich den geeigneten Extension Point, der für den eigenen Einsatz geeignet erscheint. Dann ordnet man dem Extension Point den Aufruf für die eigene Erweiterung zu. Diese Zuordnung muss an einer Stelle im Code gemacht werden, an dem der Extension Point noch nicht durchlaufen wurde. Am einfachsten geschieht dies beispielsweise in der boot.php eines eigenen AddOns.
Beispiel:
`rex_extension::register('SLICE_SHOW', array('myclass', 'myfunction'), rex_extension::LATE);`

Dies löst am Extension Point `SLICE_SHOW` die Methode `myclass::myfunction` auf.

Die Funktion, die am Extension Point aufgerufen wird, bekommt in diesem Falle folgende Werte übergeben:

- den Namen des Extension Points
- das Subject, welches in den meisten Fällen verändert werden kann und als Rückgabewert der eigenen Funktion wieder in den weiteren Ablauf eingefügt werden kann
- als zusätzliche Parameter: article_id, clang, ctype, module_id, slice_id, function, function_slice_id

Die Registrierung eines Extenstion Points mit der Methode `rex_extension::register` kann mit dem Parameter `rex_extension::EARLY` (-1), `rex_extension::NORMAL` (0) oder `rex_extension::LATE` (1)aufgerufen werden. Standard ist NORMAL (0). Dadurch kann die Reihenfolge der Abarbeitung der Erweiterungen gesteuert werden.

<a name="definieren"></a>
## Eigene Extension Points definieren

Im eigenen Programmcode von Addons lassen sich eigene Extension Points setzen, die dann wiederum von anderen Entwicklern genutzt werden können.

Beispiel:
```
$meine_var = rex_extension::registerPoint(new rex_extension_point(
    'MEIN_EXTENSION_POINT',
    $meine_var,
    [$sinnvolle, $parameter, ... ]
));
```

<a name="core"></a>
## Core

CACHE_DELETED
: Daten: rex_i18n::msg('delete_cache_message')
: Parameter: keine

CLANG_ADDED
: Daten: keine
: Parameter: ['id' => $clang->getId(), 'name' => $clang->getName(), 'clang' => $clang]

CLANG_DELETED
: Daten: keine
: Parameter: ['id' => $clang->getId(), 'name' => $clang->getName(), 'clang' => $clang]

CLANG_FORM_ADD
: Daten: keine
: Parameter: keine

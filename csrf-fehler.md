# Fehler: CSRF-Token ungültig - wo tritt dieser Fehler auf, mögliche Fehlerquellen und deren Analysen

* [YFORM Datensatz lässt sich nicht speichern](#yform)

<a name="yform"></a>

## YFORM Datensatz lässt sich nicht speichern

Kommt es beim Speichern eines YFORM Datensatzes, beim Anlegen einer neuen Tabelle über den YFROM Table Manager oder sogar beim Speichern im yrewrite zu besagtem Fehler das der CSRF-Token ungültig ist kann das verschiedene Ursachen haben.

* Es exisitiert noch ein altes ytemplate welches per autoload geladen ist, aber nicht kompatibel mit der aktuellen YFORM Version ist. Ein entfernen der inkompatiblen ytemplates ist notwendig. 
* * Mögliche Speicherorte: Theme Addon, Project Addon, eigene Addons


Code zum Debuggen:

https://github.com/yakamara/redaxo_yform/blob/master/lib/yform/value/csrf.php#L20

* Kommt es überhaupt zu der Stelle?
* Unterscheiden sich tatsächlich die beiden Values?
* Haben beide einen Token, oder ist eins von beiden leer?


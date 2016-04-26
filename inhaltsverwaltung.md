# Inhaltsverwaltung

Ein eigentlicher Artikel, wie er auf der Webseite erscheint, wird über Blöcke erstellt. Das heißt, es gibt einen Artikel, welcher mehrere Blöcke hat (z.B. einen Headlineblock, einen Fließtext etc).

Weiterhin hat ein Artikel auch Metainformationen wie einen Artikelnamen, eine allgemeine Beschreibung oder vielleicht auch Online- und Offline-Zeiten. Diese können individuell über das AddON Metainfo erweitert werden.

Sofern mehrere Sprachen aktiviert sind, gibt es einen Artikel auch in mehreren Sprachen – quasi einen parallelen Artikel. Dieser hat andere Inhalte und auch andere Metadaten.

Ein weiteres Feature kann man über die Templates definieren: den Spalten-/Bereichsmodus. Man kann somit einen Artikel aufteilen und gestalterisch besser voneinander trennen.

- [Blöcke (Slices) / Module](#bloecke_slices_module)
- [Metadaten](#metadaten)
- [mehrere Sprachen](#mehrere_sprachen)
- [Spalten](#spalten)

 
<a name="bloecke_slices_module"></a>
## Blöcke (Slices) / Module

Die eigentlichen Inhalte werden aus Modulen zusammengebaut. Man könnte sie auch Minitemplates nennen, wobei eine unendliche Anzahl von diesen in einem Artikel möglich sind. Diese Module können sehr unterschiedlich sein. Mögliche Formen eines Moduls sind zum Beispiel Headline, Fließtext, Grafiken hochladen und darstellen oder dynamische Listen aus Datenbanken, dynamische Grafiken, Unternavigationen etc.

Jeder Abschnitt eines Artikels, der mit einem bestimmten Modul erstellt wurde, wird als Block bezeichnet. Diese Blöcke werden in den REDAXO-Tabellen als “Artikel-Slices” gespeichert. Die Summe aller Blöcke (= Slices) ergibt dann den kompletten Artikel.

Zunächst fängt man mit einem Block an und baut sich nun nach und nach seinen Artikel auf. Über die Blockliste kann man nun den entsprechenden Block auswählen und bekommt eine Eingabemaske, in der man den entsprechenden Inhalt einpflegt. Über zwei Icons kann der Inhalt nach oben oder unten sortiert werden (Sofern die Verschiebebuttons nicht auftauchen, wurden sie für den Redakteur nicht aktiviert).

<a name="metadaten"></a>
## Metadaten

Metadaten sind Rahmendaten eines Artikels. Im aktuellen Bild sind zum Beispiel neben dem Artikelnamen die Online- und Offline-Zeit sowie eine Beschreibung und weitere Felder angezeigt und für den Redakteur pflegbar. Wie diese Metadaten verwendet werden, hängt stark von der Programmierung ab. Zum Beispiel könnte die Beschreibung eines Artikels für Suchmaschinen verwendet werden, die Online/Offline-Zeit für eine Sperrung und Darstellung des Artikels. Diese Funktionen müssen vom Entwickler beim Anpassen des Systems selbst hinterlegt werden.

Metadaten lassen sich über das System AddOn “Metainfo” anpassen und erweitern.

<a name="mehrere_sprachen"></a>
## mehrere Sprachen

REDAXO ist mehrsprachfähig. Sofern mehrere Sprachen aktiviert sind und auch der Admin dem Redakteur die Sprachen oder eine spezielle Sprache zugewiesen hat, kann nun ein Artikel in den verschiedenen Sprachvarianten angepasst werden.

Grundsätzlich ist ein Artikel immer in allen Sprachen vorhanden und unterscheidet sich durch den Inhalt und die Metadaten. Die Struktur der verschiedenen Sprachen ist demzufolge gleich! Wenn ein Artikel in einer Sprache gelöscht wird, werden auch alle anderen Sprachartikel gelöscht. Darauf sollte man achten.

Ansonsten hat man eine Sprachauswahl und kann zwischen den Artikel in den verschiedenen Sprachen springen. Die Sprachen werden vom Admin über “System>Sprachen” erweitert.

Ebenfalls ist es möglich, eine Seite mehrsprachig zu erstellen und jede Sprache mit einer anderen Struktur zu realisieren. So kann beispielsweise der Ansatz gewählt werden, dass jede Sprache als eigene Root-Kategorie angelegt wird.


<a name="spalten"></a>
## Spalten

Es kann ein Spalten/Bereichsmodus aktiviert werden, welcher der Admin bei den Templates zuweisen kann. Um verschiedene Spalten zu sehen, muss das entsprechende Template vorher bei der Artikelliste ausgewählt sein.

Dann tauchen die entsprechenden Spalten oberhalb der Inhaltsverwaltung auf und man kann zwischen diesen springen.

Dies ermöglicht es, einen Artikel in mehrere Bereiche aufzugliedern und diese an verschiedenen Stellen im Template einzubinden.

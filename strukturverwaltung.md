# Strukturverwaltung

- [Artikel und Kategorien](#artikel_und_kategorien)
- [Kategorien](#kategorien)
- [Artikel](#artikel)

<a name="artikel_und_kategorien"></a>
## Artikel und Kategorie

Nach dem erfolgreichen Login in REDAXO ist die Strukturverwaltung die erste Seite, die Sie sehen. Die Strukturverwaltung ist der zentrale Bereich.

Das seitenbildende Element ist der **Artikel**. Er steht in der Regel für eine Inhaltsseite Ihrer Webseite. Für jeden Artikel kann ein **Template** ausgewählt werden, das den Rahmen oder das Erscheinungsbild der Webseite bestimmt. Über die Funktion **Status** kann – soweit programmiert – die Seite **online und offline** geschaltet werden.

Die Verwaltung der Artikel erfolgt über die **Kategorien**. In REDAXO wird eine hierarchische Struktur eingesetzt. Das heißt, verschiedene Kategorien (Ordner) enthalten verschiedene Artikel (Inhalte). Jede Kategorie hat einen **Startartikel** (Startartikel sind Einstiegsseiten einer Kategorie – im Normalfall Übersichtsseiten).

Normale Artikel können in beliebiger Anzahl erstellt werden. Einem Artikel kann man ein Template zuweisen, welches die Darstellungsform bestimmt. Ein Artikel besteht aus mehreren **Blöcken** und repräsentiert den eigentlichen Inhalt. Die Erstellung dieser Blöcke basiert auf **Modulen**. Mittels der Module werden Eingabemasken für Textbausteine, Bilder u. a. definiert und die Anzeige der dort eingegebenen Inhalte formatiert.

Weiterhin hat der Artikel Metadaten, die ihn allgemein beschreiben (z.B. Kurzbeschreibung, Suchbegriff und Grafik).

Kategorien können auch in der Form genutzt werden, um Navigationsstrukturen abzubilden. Für die meisten Fälle gilt: Was in der Struktur zu sehen ist, sieht man auch auf der Sitemap und in der Navigation. Die Priorität organisiert die Reihenfolge.


<a name="kategorien"></a>
## Kategorie

Kategorien werden, wie in einem Explorer oder Finder, zur Strukturierung und Verwaltung der Artikel erstellt. Sie können wiederum andere Kategorien und Artikel enthalten.

**Erstellen**

Zum Erstellen einer neuen Kategorie, klicken Sie auf das (+)-Symbol, geben Sie den Namen der Kategorie ein und speichern Sie Ihre Eingabe über die Schaltfläche “edit_category” ab. Die so erstellte Kategorie ist in den Funktion offline gestellt. Für die Verwaltung hat die Einstellung keinerlei Funktion.

**Funktion/Status**

Diese Einstellung kann vom Entwickler ausgelesen und genutzt werden. Neben der Verwaltung können Kategorien die Seitennavigation Ihrer Webseite bilden. Über die oben beschriebene Funktion “online/offline” kann der Name sichtbar geschaltet werden. Diese Funktion wird in der Regel bei der Programmierung eines Templates genutzt.

Jede Kategorie enthält nach dem Erstellen immer einen Startartikel, der nicht gelöscht oder in der Funktion offline/online verändert werden kann.

Wechseln Sie in die gewünschte Kategorie, indem Sie auf den Namen der Kategorie klicken. Die Kategorie wird danach mit den enthaltenen Artikeln angezeigt.

**Prio**

Über die Einstellung Prio kann die Reihenfolge der Kategorien in der Strukturverwaltung verändert werden. Die Reihenfolge kann auch bei der Ausgabe der Kategorien auf der Webseite genutzt werden.

<a name="artikel"></a>
## Artikel

Artikel sind die eigentlichen Inhalte. Ein Artikel besteht aus einem Artikelnamen, einem Template, beschreibenden Daten (Metadaten) und dem eigentlichen Inhalt, welcher auf der Webseite im Normalfall zu sehen ist.

In der Strukturverwaltung kommt man über die Kategorien zu den Artikeln und sieht diese immer unterhalb einer Kategorie und deren Unterkategorien.

Es gibt zwei Arten von Artikeln. Den Startartikel und den “normalen” Artikel. Ein Startartikel hängt immer an einer Kategorie, das heißt, es ist immer ein Startartikel in einer Kategorie vorhanden. Um weitere Artikel anzulegen, kann man neben dem Artikelnamen auf das Plus-Icon klicken und einen neuen Artikel anlegen.

Mit online/offline kann man, wie bei den Kategorien auch, den Artikel aktivieren und deaktivieren. Abhängig von der Programmierung wird dann dieser Artikel angezeigt oder nicht. Man kann beliebig viele Artikel anlegen und über die “Prio”-Spalte positionieren. Mit dem Template wird definiert, in welchem Rahmen ein Artikel dargestellt werden soll.

Inhalte werden über Blöcke gepflegt. Wenn man auf dem Artikelnamen klickt, springt man in die Inhaltsverwaltung. Siehe 2.2 Inhaltsverwaltung

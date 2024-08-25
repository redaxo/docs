# Strukturverwaltung

* [Über die Struktur](#ueber)
* [Funktionsbeschreibung](#funktionen)
  + [Pfad](#pfad)
  + [Kategorie erstellen](#kat_e)
  + [Artikel erstellen und pflegen](#art_e)
  + [Online / Offline](#ofon)
  + [Ändern](#aendern)
    - [Prio](#prio)
    - [Kategorien und Artikel umbenennen](#rename)
    - [Artikel-Template ändern](#template)
    - [Metadaten/Einstellungen einer Kategorie](#meta)
* [Sprachen](#sprache)
* [Weitere strukturbildende Funktionen](#more)
  + [Artikel / Kategorien Kopieren und Verschieben](#copy)
  + [Artikel in Startartikel umwandeln](#convert)
  + [Artikel in Kategorie umwandeln](#convertcat)

<a name="ueber"></a>

## Über die Struktur

Die Strukturverwaltung wird gewöhnlich direkt nach dem Login aufgerufen und ist über den Menüpunkt „Struktur“ erreichbar.

Über die Strukturverwaltung werden Kategorien und Artikel angelegt und hierarchisch verwaltet, die sowohl als Navigation im Backend dienen als auch optional als Navigationsmenü im Frontend verwendet werden können.

Den Kategorien sind Artikeln zugeordnet, in denen die Inhalte der Website organisiert werden. Jede Kategorie hat einen Startartikel. Startartikel sind die Einstiegsseiten einer Kategorie. Normale Artikel können in beliebiger Anzahl erstellt werden. Die Reihenfolge der einzelnen Kategorien und Artikel wird über die Priorität festgelegt.

Die verfügbaren Optionen hängen von den Rechten des jeweiligen Benutzers ab. Ob Artikel oder Kategorien im Frontend dargestellt werden sollen, lässt sich über die Funktion `online` oder `offline` bestimmen.

![Systemcheck](/assets/v5.2.0-Struktur-01-overview.png.png)

Struktur nach dem Login / Hauptebene

Die Strukturansicht ist zweigeteilt. Im oberen Abschnitt werden immer die Unterkategorien der aktuell gewählten Kategorie dargestellt, darunter die Artikel der gerade aktiven Kategorie.

<a name="funktionen"></a>

## Funktionsbeschreibung

In der Struktur kann man die Struktur der Website verwalten und erweitern.
Folgende Funktionen stehen zur Verfügung:

<a name="pfad"></a>

### Pfad

Die Pfadanzeige zeigt an, wo man sich innerhalb der Struktur befindet. Bei Klick auf einen Abschnitt des Pfades wechselt man direkt in die gewünschte Kategorie.

<a name="kat_e"></a>

### Kategorie erstellen

Das Erstellen einer neuen Kategorie erfolgt über das (+)-Symbol. Danach legt man den Namen der Kategorie fest und speichert die Eingabe über die Schaltfläche `Kategorie hinzufügen` . Die erstellte Kategorie ist zunächst offline gestellt.

<a name="art_e"></a>

### Artikel erstellen und pflegen

Man erstellt einen neuen Artikel über das (+)-Symbol und gibt anschließend den Namen des Artikels ein. Hierbei besteht auch die Möglichkeit, ein vorgegebenes Template für die Seitendarstellung auszuwählen. Nach Bestätigen über die Schaltfläche `Artikel hinzufügen` wird der Artikel angelegt. Der erstellte Artikel ist zunächst offline gestellt. Um den Artikel zur Bearbeitung aufzurufen, klickt man auf seinen Namen. Mehr dazu im Kapitel [Redaktion](/{{path}}/{{version}}/redaktion).

<a name="ofon"></a>

### Online / Offline

Hiermit können Artikel und Kategorien den Status `online` oder `offline` erhalten.

Sofern der Entwickler das bei der Programmierung der Website berücksichtigt, werden offline gestellte Artikel und Kategorien in den Navigationen der Website ausgeblendet oder gar gesperrt. In der Strukturverwaltung selbst hat diese Funktion keine Auswirkung – die Inhalte, Artikel und Kategorien können weiterhin bearbeitet und betrachtet werden.  

<a name="aendern"></a>

### Ändern

Das Ändern der Artikel– und Kategorienamen, die Reihenfolge, der optionalen Kategorie-Metadaten oder die Template-Auswahl für Artikel sind über den Link `ändern` zugänglich.

<a name="prio"></a>

#### Prio

Die Priorität (Prio) definiert die Reihenfolge der Artikel und Kategorien in der Struktur. Die Prio kann man ändern, indem man neben den Artikel- oder Kategorienamen auf `ändern` klickt und anschließend den Prio-Wert ändert. Man speichert die Einstellung mit “Artikel speichern” oder “Kategorie speichern”.

<a name="rename"></a>

#### Artikel und Kategorien umbenennen

Das Umbenennen einer Kategorie oder eines Arikels erfolgt über die “Ändern”-Funktion. Nach Aufruf kann der Name in einem Formularfeld geändert werden. Nach Bestätigung mit `Artikel speichern` oder `Kategorie speichern` wird der Name geändert.

<a name="template"></a>

#### Artikel-Template ändern

Nach Aufruf der `Ändern` -Funktion erscheint beim Artikel ein Auswahlfeld zur Festlegung des Templates. Nach Bestätigung mit `Artikel speichern` wird die Auswahl übernommen.

<a name="meta"></a>

#### Metadaten / Einstellungen einer Kategorie

Anders als bei Artikeln werden Metadaten der Kategorien direkt in der Struktur bearbeitet. Hierzu ruft man die `Ändern` -Funktion auf. Es erscheint ein `(+)` -Symbol, das es ermöglicht, weitere Einstellungen zur Kategorie durchzuführen.

> Das `(+)` -Symbol erscheint nur, wenn Metafelder für die Kategorie hinterlegt wurden.

<a name="sprache"></a>

### Sprachen

REDAXO ist mehrsprachenfähig. Sofern mehrere Sprachen aktiviert sind und der Redakteur die entsprechenden Berechtigungen hat, erscheint in REDAXO oben rechts neben der Pfadleiste eine Sprachauswahl. Damit kann innerhalb der Struktur zwischen den einzelnen Sprachen gewechselt werden. Die Struktur ist in allen Sprachen identisch. Sie unterscheidet sich in der Benennung der Kategorien und Artikel.

Werden in einer Sprache ein neuer Artikel oder eine neue Kategorie angelegt, werden diese in allen Sprachen mit dem gleichen Namen angelegt. Name und  Metadaten können sprachabhängig gepflegt werden.  

Möchte man einen Artikel oder eine Kategorie in einer Sprache nicht in der Navigation oder in Artikellisten einer Sprache anzeigen, können diese mit dem Offline-Status (sofern in der Programmierung der Website vorgesehen) ausgeblendet werden.

Die Sprachen werden vom Admin verwaltet und bereitgestellt.

> **Achtung** Wenn ein Artikel oder eine Kategorie in einer Sprache gelöscht wird, werden diese auch in allen weiteren Sprachversionen gelöscht.

<a name="more"></a>

## Weitere strukturbildende Funktionen

Einige Funktionen stehen nicht direkt in der Struktur zur Verfügung und müssen in den Artikeln durchgeführt werden. Da diese die Struktur beeinflussen, werden sie hier beschrieben.

<a name="copy"></a>

### Artikel oder Kategorien kopieren und verschieben

Diese Funktionen müssen im Artikel im Reiter `Funktionen` durchgeführt werden. Kategorien können nur kopiert oder verschoben werden, indem man im Startartikel der Kategorie diese Funktion durchführt.

<a name="convert"></a>

### Artikel in Startartikel umwandeln

Befinden sich mehrere Artikel in einer Kategorie, so ist es möglich, einen normalen Artikel auszuwählen und diesen als neuen Startartikel der Kategorie festzulegen. Dies erfolgt im Funktionsreiter des entsprechenden Artikels. Der ursprüngliche Startartikel wird dann zu einem einfachen Artikel umgewandelt.

<a name="convertcat"></a>

### Artikel in Kategorie umwandeln

Normale Artikel können in eine Kategorie umgewandelt werden. Dies erfolgt im Funktionsreiter des entsprechenden Artikels.

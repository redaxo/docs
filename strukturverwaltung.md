# Strukturverwaltung

- [Über](#ueber)
- [Funktionsbeschreibung](#funktionen)
  - [Pfad](#pfad)
  - [Kategorie erstellen](#kat_e)
  - [Artikel erstellen](#art_e)
  - [Online / Offline](#ofon)
  - [Ändern](#aendern)
    - [Prio](#prio)
    - [Kategorien und Artikel umbenennen](#rename)
    - [Artikel-Template ändern](#template)
    - [Metadaten einer Kategorie](#meta)
- [Sprachen](#sprache)

<a name="ueber"></a>
## Über
Über die Strukturverwaltung werden Kategorien angelegt und verwaltet, die sowohl als Navigation im Backend dienen und optional als Navigationsmenü im Frontend verwendet werden können. Die verfügbaren Optionen hängen von den Rechten des jeweiligen Benutzers ab. Die Strukturverwaltung wird meistens direkt nach dem Login (je nach vergebenen Rechten) aufgerufen und ist über den Menüpunkt „Struktur“ erreichbar. Die Reihenfolge der einzelnen Kategorien wird über die Prioritätenspalte festgelegt. Den Kategorien sind Artikel zugeordnet, in denen die Inhalte der Website organisiert werden. 
Ob die Inhalte im Frontend dargestellt werden sollen, lässt sich über die Funktion „online“ oder „offline“ bestimmen.

![Systemcheck](/assets/v5.2.0-Struktur-01-overview.png.png)
Struktur nach dem Login / Hauptebene

Die Strukturansicht  ist zweigeteilt. Im Oberen Abschnitt werden immer die Unterkategorien der aktuell gewählten Kategorie dargestellt, darunter die Artikel der gerade aktiven Kategorie. 

<a name="funktionen"></a>
## Funktionsbeschreibung
In der Struktur kann man die Struktur der Website verwalten und erweiteren.
Folgende Funktionen stehen hierzu zur Verfügung: 

<a name="pfad"></a>
### Pfad 
Die Pfadanzeige zeigt an, wo man sich innerhalb der Struktur befindest. Bei Klick auf einen Abschitt des Pfades wechselt man direkt in die gewünschte Kategorie. 

<a name="kat_e"></a>
### Kategorie erstellen
Das Erstellen einer neuen Kategorie erfolgt über das (+)-Symbol. Dana legt man den Namen der Kategorie fest und speichert die Eingabe über die Schaltfläche “Kategorie hinzufügen”. Die erstellte Kategorie ist zunächst offline gestellt. 

<a name="art_e"></a>
### Artikel erstellen
Man erstellt einen neuen Artikel über das (+)-Symbol und gibt anschließend den Namen des Artikels ein. Hierbei besteht auch die Möglichkeit ein vorgegebenes Template für die Seitendarstellung auszuwählen. Nach Bestätigen über die Schaltfläche “Artikel hinzufügen” wird der Artikel angelegt. Der erstellte Artikel ist zunächst offline gestellt. Um den Artikel zur Bearbeitung aufzurufen, klickt man auf seinen Namen. 

<a name="ofon"></a>
### Online / Offline
Hiermit können Artikel und Kategorien den Status online oder offline erhalten. 
Sofern bei der Programmierung der Website berücksichtigt, werden offline gestellte Artikel und Kategorien in den Navigationen der Website ausgeblendet oder gar gesperrt. In der Strukturverwaltung selbst hat diese Funktion keine Auswirkung, die Inhalte, Artikel und Kategorien können weiterhin bearbeitet und betrachtet werden.  

<a name="aendern"></a>
### Ändern 
Das Ändern der Artikel– und Kategorienamen, die Reigenfolge, optionale Metadaten der Kategorien oder die Templateauswahl für Artikel sind über die “ändern”-Funktion zugänglich. 

<a name="prio"></a>
#### Prio
Die Priorität (Prio) definiert die Reihenfolge der Artikel und Kategorien in der Struktur. Die Prio kann man ändern, indem man neben den Artikel- oder Kategorienamen auf “ändern” klickt und anschließend den Prio-Wert ändert. Man speichert die Einstellung mit “Artikel speichern” oder “Kategorie speichern”.

<a name="rename"></a>
#### Artikel und Kategorien umbenennen
Das umbenennen einer Kategorie oder eines Arikels erfolgt über die “Ändern”-Funktion. Nach Aufruf kann der Name in einem Formularfeld geändert werden. Nach Bestätigung mit “Artikel speichern” oder “Kategorie speichern” wird der Name geändert. 

<a name="template"></a>
#### Artikel-Template ändern
Nach Aufruf der “Ändern”-Funktion erscheint beim Artikel ein Auswahlfeld zur Festlegung des Templates. Nach Bestätigung mit “Artikel speichern” wird die Auswahl übernommen. 

<a name="meta"></a>
#### Metadaten einer Kategorie (optional) 
Anders als bei Artikeln werden Metadaten der Kategorien (optional) direkt in der Struktur bearbeitet. Hierzu ruft man die “Ändern”-Funktion auf. Es erscheint (sofern im Projekt vorgesehen) ein (+)-Symbol, das es ermöglicht weitere Einstellungen zur Kategorie durchzuführen. 

<a name="sprache"></a>
### Sprachen
REDAXO ist Mehrsprachfähig. Sofern mehrere Sprachen aktiviert sind und der Redakteur die entsprechnden Berechtigungen hat, erscheint in REDAXO oben rechts neben der Pfadleiste eine Sprachauswahl. Damit kann innerhalb der Struktur zwischen den einzelnen Sprachen gewechselt werden. Die Struktur der ist in allen Sprachen identisch. Sie unterscheidet sich in der Benennung der Kategorien und Artikel. Wird in einer Sprache ein neuer Artikel angelegt, steht dieser in allen Sprachen mit der gleichen Bezeichnung angelegt. Titel und  Metadaten können sprachabhängig gepflegt werden.  Möchte man einen Artikel oder eine Kategorie in einer Sprache nicht in der Navigation oder in Artikellisten einer Sprache anzeigen, können diese mit dem Offline-Staus (sofern in der Programmierung der Website vorgesehen) ausgeblendet werden. 
Die Sprachen werden vom Admin verwaltet und bereitgestellt. 

> **Achtung** Wenn ein Artikel oder eine Kategorie in einer Sprache gelöscht wird, werden auch alle alle weiteren Sprachversionen gelöscht.

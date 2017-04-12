# Redaktion
* [Redaktion](#redaktion)
  * [Einleitung](#einleitung)
  * [Blöcke](#blöcke)
    * [Block bearbeiten](#block-bearbeiten)
    * [Block löschen ](#block-löschen-)
    * [Block verschieben](#block-verschieben)
  * [Bedienelemente in REDAXO ](#bedienelemente-in-redaxo-)
    * [Formularfelder](#formularfelder)
    * [Linkmap-Widget](#linkmap-widget)
    * [Media-Widget](#media-widget)
    * [Medialist-Widget](#medialist-widget)
      * [Texteditoren und weitere Eingabemöglichkeiten](#texteditoren-und-weitere-eingabemöglichkeiten)
  * [Artikel-Funktionen](#artikel-funktionen)
    * [Artikel in Startartikel umwandeln](#artikel-in-startartikel-umwandeln)
    * [Artikel in Kategorie umwandeln](#artikel-in-kategorie-umwandeln)
    * [Inhalte kopieren](#inhalte-kopieren)
    * [Artikel / Kategorien Kopieren und Verschieben](#artikel--kategorien-kopieren-und-verschieben)
  * [Metadaten](#metadaten)
  * [Sprachen](#sprachen)
    * [Inhalte zwischen Sprachen kopieren ](#inhalte-zwischen-sprachen-kopieren-)
  * [Spalten](#spalten)
  * [Arbeitsversion / Liveversion](#arbeitsversion--liveversion)
  * [History](#history)


## Einleitung
Die Artikel der Webpräsenz findet und erstellt man in den Kategorien der Strukturverwaltung. Dort wählt man auch das Template aus, welches die Anzeige des Artikels und die Anzahl der zu pflegenden Spalten definiert. Es gibt zwei Artikeltypen: ***Normale Artikel*** und ***Startartikel***. Ein Startartikel repräsentiert immer die Kategorie und wird automatisch bei Erstellung einer Kategorie angelegt. Normale Artikel werden zusätzlich in einer Kategorie abgelegt. Die Inhalte der Artikel werden über Blöcke eingepflegt. Zusätzliche Informationen können in den Metadaten hinterlegt werden. 

## Blöcke
Die Inhalte (Content) eines Artikels werden mit Hilfe von Blöcken zusammengebaut. Sie werden durch die installierten Module in REDAXO zur Verfügung gestellt. Die Funktionen der Blöcke reichen von einfachen Texteingaben/-ausgaben bis zu kleinen Applikationen zur Generierung der Inhalte auf der jeweiligen Seite. Mögliche Einsatzzwecke sind beispielhaft: Headlines, Fliesstext, Galerien und die Steuerung von Ausgaben installierter Addons.

![Artikel mit Blöcken](/assets/v5.2.0-redaktion-02-block-auswahl.png)

 Die Blöcke werden im Editiermodus (1) des Artikels eingepflegt. 

![Blockauswahl](/assets/v5.2.0-redaktion-01-bloecke.png)

Um einen Block hinzuzufügen, 
- klickt man auf das Aufklappmenü „Block hinzufügen" (2)
- und wählt den gewüschten Block (3)
- füllt das Formular aus (sofern erforderlich)
- speichert mit „Block speichern"

Möchte man den aktuellen Stand der Bearbeitung zwischenspeichern und den Block geöffnet halten um weiter zu arbeiten, klickt man auf **Block übernehmen**. Möchte man den aktuellen Stand nicht speichern, kann man die Bearbeitung **abbrechen**.

> Da in jeder Redaxo-Installation unterschiedliche, häufig individuell erstellte Blöcke, zur Verfügung stehen, wird deren Funktion hier nicht erläutert. 

### Block bearbeiten
Um einen vorhanden Block zu bearbeiten, klickt man auf das grüne Editier-Symbol

### Block löschen 
Einen Block löscht man durch klick auf das rote Symbol mit dem Mülleimer

### Block verschieben
Blöcke können mit den Pfeilen rechts um jeweils eine Position nach oben oder unten verschoben werden. 

## Bedienelemente in REDAXO 
Es gibt einige Eingabemöglichkeiten die in REDAXO wiederkehren. Hierzu zählen Formulareingaben, Linkauswahl und Auswahlfelder für Medien. 
![Beispiel-Block mit diversen Eingabemöglichkeiten](/assets/v5.2.0-redaktion-03-widgetsandforms.png)

### Formularfelder
Die meisten Blöcke fragen in Formularen die Eingaben des Redakteurs ab. Hier können über Textfelder, Checkboxen, Auswahllisten Einstellungen und die Texteinplfege durchgeführt werden. 

### Linkmap-Widget
Über das Linkmap-Widget können Artikel innderhalb der Redaxo-Präsenz verlinkt werden. 

### Media-Widget (4) 
Mit dem Media-Widget werden einzelte Medien aus dem Medienpool ausgewählt. Das können beispielsweise Bilder oder Dokumente sein.

### Medialist-Widget (5) 
Zur Auswahl mehrerer Medien gibt es das Medialist-Widget. Hier können aus dem Medienpool mehrere Medien ausgewählt werden und deren Reihenfolge organisiert werden. Medialist-Widgets werden beispielsweise für die Erstellung von Downloadlisten oder Galerien benötigt. 

#### Texteditoren und weitere Eingabemöglichkeiten (6) 
Weitere Eingabemöglichkeiten werden über AddOns in REDAXO bereitgestellt. Hierzu zählen beispielhaft auch Markdown- und WYSIWYG-Editoren (MS-Word ähnlich).


## Artikel-Funktionen
Im Reiter ***Funktionen*** stehen folgende Funktionen je nach Artikeltyp zur Verfügung. 

### Artikel in Startartikel umwandeln
[Siehe: Strukturverwaltung](/{{path}}/{{version}}/strukturverwaltung#convertcat)
### Artikel in Kategorie umwandeln
[Siehe: Strukturverwaltung](/{{path}}/{{version}}/strukturverwaltung#convertcat)
### Inhalte kopieren
[Siehe: Sprachen](#sprachen)
### Artikel / Kategorien Kopieren und Verschieben
[Siehe: Strukturverwaltung](/{{path}}/{{version}}/strukturverwaltung#convert)


## Metadaten
Im Reiter Metadaten können zusätzliche Einstellungen für den Artikel durchgeführt werden. Dies können u.a. Timer-Einstellungen, Informationen für Suchmaschinen und soziale Netzwerke sein. Die Metadaten werden individuell für die Webpräsenz festgelegt und werden durch das Metainfo-AddOn bereitgestellt.

## Sprachen
REDAXO ist mehrsprachfähig. Sofern mehrere Sprachen aktiviert sind und der Redakteur die entsprechnden Berechtigungen hat, erscheint in Backend oben rechts neben der Pfadleiste eine Sprachauswahl. Damit kann innerhalb eines Artikels zwischen den zur Verfügung stehenden Sprachversionen gewechselt werden. 
Ein Artikel ist immer in allen Sprachen vorhanden und unterscheidet sich durch den Titel, die Inhalte und die Metadaten. Möchte man einen Artikel oder eine Kategorie in einer Sprache nicht in der Navigation oder in Artikellisten einer Sprache anzeigen, können diese mit dem Offline-Staus (sofern in der Programmierung der Website vorgesehen) ausgeblendet werden. 
Die Sprachen werden vom Admin verwaltet und bereitgestellt. 

> Wenn ein Artikel in einer Sprache gelöscht wird, werden auch alle übrigen Sprachversionen gelöscht.

### Inhalte zwischen Sprachen kopieren 
Im Reiter **Funktionen** steht die Kopierfunktion **Inhalte kopieren** zur Verfügung. Hiermit kann ein ganzer Artikel mit all seinen Blöcken identisch in eine andere Sprache zur Übersetzung übertragen werden. Befinden sich in der gewünschetn Zielsprache bereits Inhalte, werden die Blöcke der Quelle ans Ende des Zielartikels gesetzt. 

## Spalten
Ein Artikel kann in mehrere Bereiche unterteilt sein, die voneinander unabhängig gepflegt werden können. Je nach ausgewählten Template können unterschiedlich viele Spalten zur Verfügung gestellt werden. Häufig wird diese Funktion verwendet um z.B. eine Seitenleiste oder eine Fußnote zu pflegen oder komplexere Layouts zu realisieren. 
Um in eine Spalte zu gelangen, klicken Sie im Editiermodus auf die Bezeichnung der gewünschten Spalte. Diese finden Sie im Reiter **Editiermodus** als Untermenüpunkte. Die Pflege der Spalten erfolgt über Blöcke. 

## Arbeitsversion / Liveversion
- Notiz Screenshot anlegen -

Sollte das Versions-PlugIn der Struktur installiert sein, ist es möglich Arbeits- und Liveversionen der Artikel zu pflegen. Die Liveversion ist die aktuell auf der Website veröffentlichte Version. In der Arbeitsversion erstellt man eine neue Ausgabe des Artikels.
Jeder Artikel hat zunächst eine leere Arbeitsversion zugeordnet. Es ist allerdings möglich die Inhalte der Liveversion in die Arbeitsversion zu übertragen, so dass man an der aktuellen Version weiterarbeiten kann. Um die Arbeitsversion ansehen zu können, klickt man auf „Voransicht“ Nach Abschluss der Überarbeitung kann die Arbeitsversion als Liveversion freigegeben werden und somit online geschaltet werden. .


## History
- Notiz Screenshot anlegen -
- Notiz Screenshot anlegen -

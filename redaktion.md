# Redaktion
* [Redaktion](#redaktion)
  * [Einleitung](#einleitung)
  * [Blöcke](#bloecke)
    * [Block bearbeiten](#block-bearbeiten)
    * [Block löschen ](#block-loeschen-)
    * [Block verschieben](#block-verschieben)
  * [Bedienelemente in REDAXO ](#bedienelemente)
    * [Formularfelder](#formularfelder)
    * [Link](#linkmap)
    * [Linkliste](#linklist)
    * [Medien-Link](#media)
    * [Medienliste](#medialist)
      * [Texteditoren und weitere Eingabemöglichkeiten](#andere)
  * [Artikel-Funktionen](#funktionen)
    * [Artikel in Startartikel umwandeln](#convert)
    * [Artikel in Kategorie umwandeln](#convertcat)
    * [Inhalte kopieren](#copycontent)
    * [Artikel / Kategorien Kopieren und Verschieben](#move)
  * [Metadaten](#metadaten)
  * [Sprachen](#sprachen)
    * [Inhalte zwischen Sprachen kopieren ](#copylang)
  * [Spalten](#spalten)
  * [Arbeitsversion / Liveversion](#version)
  * [History](#history)

<a name="einleitung"></a>
## Einleitung
Die Artikel der Webpräsenz findet und erstellt man in den Kategorien der Strukturverwaltung. Dort wählt man auch das Template aus, welches die Anzeige des Artikels und die Anzahl der zu pflegenden Spalten definiert. Es gibt zwei Artikeltypen: ***Normale Artikel*** und ***Startartikel***.

Ein Startartikel repräsentiert immer die Kategorie und wird automatisch bei Erstellung einer Kategorie angelegt. Ein Startartikel ist erkennbar an seinem farblich hervorgehobenen Icon.
Normale Artikel kann in einer Kategorie zusätzlich ablegen.

Die Inhalte der Artikel werden über Blöcke eingepflegt. Zusätzliche Informationen und Einstellungen können in den Metadaten hinterlegt werden. 

<a name="bloecke"></a>
## Blöcke
Die Inhalte (der Content) eines Artikels werden mit Hilfe von Blöcken zusammengebaut. Sie werden durch die installierten Module in REDAXO zur Verfügung gestellt. Die Funktionen der Blöcke reichen von einfachen Texteingaben/-ausgaben bis zu kleinen Applikationen zur Generierung der Inhalte auf der jeweiligen Seite. Mögliche Einsatzzwecke sind vielfältig, beispielhaft seien genannt: Headlines, Fliesstext, Galerien und die Steuerung von Ausgaben installierter Addons.

![Artikel mit Blöcken](/assets/v5.2.0-redaktion-02-block-auswahl.png)
Editiermodus und Blockauswahl

Die Blöcke werden im Editiermodus (1) des Artikels eingepflegt. 

![Blockauswahl](/assets/v5.2.0-redaktion-01-bloecke.png)
Blockauswahlmenü

Um einen Block hinzuzufügen, 
- klickt man auf das Aufklappmenü `Block hinzufügen` (2)
- und wählt den gewünschten Block (3)
- füllt das Formular aus (sofern erforderlich)
- speichert mit `Block speichern`

Möchte man den aktuellen Stand der Bearbeitung zwischenspeichern und den Block geöffnet halten. Um weiter zu arbeiten, klickt man auf `Block übernehmen`. Möchte man den aktuellen Stand nicht speichern, kann man die Bearbeitung `abbrechen`.

> Da in jeder Redaxo-Installation unterschiedliche, häufig individuell erstellte Module zur Verfügung stehen, wird deren Funktion hier nicht erläutert. 

<a name="block-bearbeiten"></a>
### Block bearbeiten
Um einen vorhanden Block zu bearbeiten, klickt man auf das grüne Editier-Symbol.

<a name="block-loeschen"></a>
### Block löschen 
Einen Block löscht man durch Klick auf das rote Symbol mit dem Mülleimer.

<a name="block-verschieben"></a>
### Block verschieben
Blöcke können mit den Pfeilen rechts um jeweils eine Position nach oben oder unten verschoben werden. 

<a name="bedienelemente"></a>
## Bedienelemente in REDAXO 
Es gibt einige wiederkehrende Eingabemöglichkeiten in REDAXO. Hierzu zählen Formulareingaben, Linkauswahl und Auswahlfelder für Medien. 

<a name="formularfelder"></a>
### Formularfelder
Die meisten Blöcke fragen in Formularen die Eingaben des Redakteurs ab. Hier können über Textfelder, Checkboxen und Auswahllisten verschiedene Einstellungen definiert und Texte eingepflegt werden. 

<a name="linkmap"></a>
### Link

![Link-Widget](/assets/v5.2.0-redaktion-03-widget-link.png)
Link-widget

Über das Link-Widget kann ein einzelner Artikel der REDAXO-Webpräsenz verlinkt werden. Zur Auswahl eines Links klickt man auf das Sitemap-Symbol. Es öffnet sich dann ein Fenster (die Linkmap), in dem man innerhalb der Seitenstruktur den gewünschten Artikel auswählen kann. Um eine Kategorie zu verlinken, wählt man den dazugehörigen Startartikel. Mit dem anderen Symbol kann man die Linkauswahl wieder aufheben. 

<a name="linklist"></a>
### Linklist

![Linklist-Widget](/assets/v5.2.0-redaktion-03-widget-linklist.png)
Linklist-Widget

Mit dem Linklist-Widget können mehrere Artikel verlinkt werden. Die Reihenfolge der Links kann über die Pfeile verändert werden. Sonst verhält sich diese Eingabe wie beim Link-Widget.

<a name="media"></a>
### Medien-Link 

![Media-Link](/assets/v5.2.0-redaktion-03-widget-medium.png)
Media-Widget

Mit dem Media-Link-Widget werden einzelne Medien aus dem Medienpool ausgewählt. Das können beispielsweise Bilder oder Dokumente sein. Den Medienpool zur Auswahl des Mediums ruft man über das Listenmodul auf.

Um den Upload-Dialog des Medienpools aufzurufen, klickt man auf das (+)-Symbol. Möchte man die Informationen zum aktuell ausgewählten Medium im Medienpool aufrufen, klickt man auf das Auge. 

<a name="medialist"></a>
### Medienliste

![Medialist](/assets/v5.2.0-redaktion-03-widget-medialist.png)
Medialist-Widget

Zur Auswahl mehrerer Medien gibt es das Medialist-Widget. Hier können aus dem Medienpool mehrere Medien ausgewählt und deren Reihenfolge organisiert werden. Medialist-Widgets werden beispielsweise für die Erstellung von Downloadlisten oder Galerien benötigt. Sonst verhält sich diese Eingabe wie der Medien-Link.

<a name="andere"></a>
### Texteditoren und weitere Eingabemöglichkeiten
Weitere Eingabemöglichkeiten werden über AddOns in REDAXO bereitgestellt. Hierzu zählen beispielhaft auch Markdown- und WYSIWYG-Editoren (MS-Word ähnlich).

<a name="funktionen"></a>
## Artikel-Funktionen
Im Reiter `Funktionen` stehen je nach Artikeltyp folgende Funktionen zur Verfügung. 

<a name="convert"></a>
### Artikel in Startartikel umwandeln
[Siehe: Strukturverwaltung](/{{path}}/{{version}}/strukturverwaltung#convertcat)
<a name="convertcat"></a>
### Artikel in Kategorie umwandeln
[Siehe: Strukturverwaltung](/{{path}}/{{version}}/strukturverwaltung#convertcat)
<a name="copycontent"></a>
### Inhalte kopieren
[Siehe: Sprachen](#sprachen)
<a name="move"></a>
### Artikel / Kategorien kopieren und verschieben
[Siehe: Strukturverwaltung](/{{path}}/{{version}}/strukturverwaltung#convert)

<a name="metadaten"></a>
## Metadaten
Im Reiter `Metadaten` können zusätzliche Einstellungen für den Artikel durchgeführt werden. Dies können u.a. Timer-Einstellungen, Informationen für Suchmaschinen und soziale Netzwerke sein. Die Metadaten werden individuell für die jeweilige Webpräsenz festgelegt und werden durch das Metainfo-AddOn bereitgestellt.

<a name="sprachen"></a>
## Sprachen
REDAXO ist mehrsprachenfähig. Sofern mehrere Sprachen aktiviert sind und der Redakteur die entsprechenden Berechtigungen besitzt, erscheint im Backend oben rechts neben der Pfadleiste eine Sprachauswahl. Damit kann innerhalb eines Artikels zwischen den zur Verfügung stehenden Sprachversionen gewechselt werden. 

Ein Artikel ist immer in allen Sprachen vorhanden und unterscheidet sich durch den Titel, die Inhalte und die Metadaten. Möchte man einen Artikel oder eine Kategorie in einer Sprache nicht in der Navigation oder in Artikellisten einer Sprache anzeigen, können diese mit dem Offline-Staus (sofern in der Programmierung der Website vorgesehen) ausgeblendet werden. 
Die Sprachen werden vom Admin verwaltet und bereitgestellt. 

> Wenn ein Artikel in einer Sprache gelöscht wird, werden auch alle übrigen Sprachversionen gelöscht.

<a name="copylang"></a>
### Inhalte zwischen Sprachen kopieren 
Im Reiter `Funktionen` steht die Kopierfunktion `Inhalte kopieren` zur Verfügung. Hiermit kann ein ganzer Artikel mit all seinen Blöcken identisch in eine andere Sprache zur Übersetzung übertragen werden. Befinden sich in der gewünschten Zielsprache bereits Inhalte, werden die Blöcke der Quelle ans Ende des Zielartikels gesetzt.

<a name="spalten"></a>
## Spalten
Ein Artikel kann in mehrere Bereiche unterteilt sein, die voneinander unabhängig gepflegt werden können. Je nach ausgewähltem Template können unterschiedlich viele Spalten zur Verfügung gestellt werden. Häufig wird diese Funktion verwendet um z.B. eine Seitenleiste oder eine Fußnote zu pflegen oder komplexere Layouts zu realisieren. 

Um in eine Spalte zu gelangen, klickt man im Editiermodus auf die Bezeichnung der gewünschten Spalte. Diese findet man im Reiter `Editiermodus` als Untermenüpunkte. Die Pflege der Spalten erfolgt, indem man mit Modulen Inhaltsblöcke anlegt.

<a name="version"></a>
## Arbeitsversion / Liveversion
![Version](/assets/v5.2.0-redaktion-04-version.png)
Arbeitsversion / Liveversion

Sollte das Versions-PlugIn der Struktur installiert sein, ist es möglich, Arbeits- und Liveversionen der Artikel zu pflegen. Die Liveversion ist die aktuell auf der Website veröffentlichte Version. Die Umschaltung zwischen Liveversion und Arbeitsversion erfolgt über das Drop-Down-Menü `Version`. 

In der Arbeitsversion erstellt man eine neue Ausgabe des Artikels.
Jeder Artikel hat eine leere Arbeitsversion zugeordnet, die sich nach Belieben füllen lässt. Es ist möglich, die Inhalte der Liveversion in die Arbeitsversion zu übertragen, so dass man an der aktuellen Version weiterarbeiten kann. Um eine Vorschau der Arbeitsversion zu erhalten, klickt man auf „Voransicht“. Nach Abschluss der Überarbeitung kann die Arbeitsversion als Liveversion freigegeben werden und somit online geschaltet werden.
> **Achtung!** Wird die Arbeitsversion als Liveversion freigegeben, wird die aktuelle Liveversion überschrieben bzw. gelöscht. Nutzt man jedoch auch das History-PlugIn, so ist es möglich, vorherige Versionen wiederherzustellen. 

<a name="history"></a>
## History
In REDAXO ist eine Versionierung (History) integriert. Ist diese aktiviert, erfasst REDAXO jede Änderung in den Artikel-Blöcken und Metadaten. 

![History](/assets/v5.2.0-redaktion-06-history.png)
History-Gegenüberstellung

Nach Klick auf das History-Symbol (runder Pfeil, mit Uhr, neben dem Reiter zum Editiermodus) öffnet sich eine Gegenüberstellung der Versionen. Über ein Drop-Down-Menü können die einzelnen Versionen ausgewählt werden und im rechten Fenster betrachtet werden.

Möchte man eine ältere Version wiederherstellen, klickt man auf `Diese Version übernehmen`. Hierbei wird die aktuelle Version als neue Version gespeichert, so dass es jederzeit möglich ist, den Vorgang rückgängig zu machen. 


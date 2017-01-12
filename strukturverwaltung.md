# Strukturverwaltung

- [Über](#ueber)
- [Funktionsbeschreibung](#funktionen)

<a name="ueber"></a>
## Über
Über die Strukturverwaltung werden Kategorien angelegt und verwaltet, die sowohl als Navigation im Backend dienen und optional als Navigationsmenü im Frontend verwendet werden können.Die verfügbaren Optionen hängen von den Rechten des jeweiligen Benutzers ab. Die Strukturverwaltung wird meistens direkt nach dem Login (je nach vergebenen Rechten) aufgerufen und ist über den Menüpunkt „Struktur“ erreichbar. Die Reihenfolge der einzelnen Kategorien wird über die Prioritätenspalte festgelegt. Den Kategorien sind Artikel zugeordnet, in denen die Inhalte der Website organisiert werden. 
Ob die Inhalte im Frontend dargestellt werden sollen, lässt sich über die Funktion „online“ oder „offline“ bestimmen.

![Systemcheck](/assets/v5.2.0-Struktur-01-overview.png.png)
Struktur nach dem Login / Hauptebene

Die Strukturansicht  ist zweigeteilt. Im Oberen Abschnitt werden immer die Unterkategorien Kategorien der aktuell gewählten Kategorie dargestellt, darunter die zugehörigen Kategorien der gerade aktiven Kategorie. 

<a name="funktionen"></a>
## Funktionsbeschreibung
In der Struktur kannst du die Struktur deiner Website verwalten und erweiteren.
Folgende Funktionen stehen hierzu zur Verfügung: 

### Pfad 
Die Pfadanzeige zeigt dir an, wo du dich innerhalb der Struktur befindest. Bei Klick auf einen Abschitt des Pfades wechselst du direkt in die gewünschte Kategorie. 

### Kategorie erstellen
Zum Erstellen einer neuen Kategorie, klicke auf das (+)-Symbol, gebe den Namen der Kategorie ein und speichere deine Eingabe über die Schaltfläche “Kategorie hinzufügen” ab. Die erstellte Kategorie ist zunächst offline gestellt. 

### Artikel erstellen
Zum Erstellen einer neues Artikels, klicke auf das (+)-Symbol, gebe den Namen des Artikels ein. Hierbei besteht auch die Möglichkeit ein vorgegebenes Template für die Seitendarstellung auszuwählen. Speichere deine Eingabe über die Schaltfläche “Artikel hinzufügen” ab. Der erstellte Artikel ist zunächst offline gestellt. 

### Online / Offline
Hiermit können Artikel und Kategorien den Status online oder offline erhalten. 
Sofern bei der Programmierung der Website berücksichtigt, werden offline gestellte Artikel und Kategorien in den Navigationen der Website ausgeblendet oder gar gesperrt. In der Strukturverwaltung selbst hat diese Funktion keine Auswirkung, die Inhalte, Artikel und Kategorien können weiterhin bearbeitet und betrachtet werden.  

### Ändern 
Das Ändern der Artikel– und Dateinamen, die Reigenfolge, optionale Metadaten oder die Templateauswahl sind über die “ändern”-Funktio zugänglich. 

#### Prio
Die Priorität (Prio) definiert die Reihenfolge der Artikel und Kategorien in der Struktur. Die Prio kannst du ändern, indem du neben den Artikel- oder Kategorienamen auf “ändern” klickst und anschließend den Prio-Wert änderst. Du speicherst die Einstellung mit “Artikel speichern” oder “Kategorie speichern”.

#### Artikel und Kategorien umbenennen
Das umbenennen einer Kategorie oder eines Arikels erfolgt über die “Ändern”-Funktion. Nach Aufruf kann der Name in einem Formularfeld geändert werden. Nach Bestätigung mit “Artikel speichern” oder “Kategorie speichern” wird der Name geändert. 

#### Artikel-Template ändern
Nach Aufruf der “Ändern”-Funktion erscheint beim Artikel ein Auswahlfeld zur Festlegung des Templates. Nach Bestätigung mit “Artikel speichern” wird die Auswahl übernommen. 

#### Metadaten einer Kategorie (optional) 
Anders als bei Artikeln werden Metadaten der Kategorien (optional) direkt in der Struktur bearbeitet. Hierzu ruft man die “Ändern”-Funktion auf. Es erscheint (sofern im Projekt vorgesehen) ein Plus-Symbol dass es ermöglicht weitere Einstellungen zur Kategorie durchzuführen. 

# Medienpool
Der Medienpool stellt die Funktionen zur Verwaltung von Mediendateien wie Bilder, Dokumente und Videos bereit. Die Medien können über Kategorien organisiert werden. Der Medienpool wird nach einem Klick auf den Link Medienpool in einem eigenen Fenster geöffnet.

Im Medienpool werden die Medien gelistet und bearbeitet, die über Upload- oder Synchronisationsfunktion auf den Server geladen wurden.
Um die Sortierung übersichtlicher zu gestalten, kann man Kategorien definieren und die hochgeladenen Medien diesen Kategorien zuweisen. 

Alle Medien, die im Medienpool verwaltet werden, befinden sich im Ordner “/media” deiner Redaxo-Installation.

- [Liste der Medien](#liste)
- [Detailansicht](#detail)
- [Medienkategorien verwalten](#kategorien)
- [Medien hinzufühen](#upload)
- [Medien löschen](#loeschen)
- [Datei austauschen](#tausch)
- [Medien verschieben](#schieben)
- [Medien verschieben](#schieben)
- [Dateien Synchronisieren](#sync)

<a name="liste"></a>
## Liste der Medien
![Liste der Medien / hier eine ausgewählte Kategorie](/assets/v5.2.0-medianpool-01-overview.png)

Nach Aufruf des Medienpools über den Menüpunkt “Medienpool”, gelangt man direkt in die Liste der Medien. Hier werden alle Medien der aktuell gewählten Kategorie gelistet. Medien, die keiner Kategorie zugeordnet sind, werden in der Hauptebene unter “Keine Kategorie” gelistet. Zur Auswahl einer Kategorie, steht dir ein Auswahlmenü neben der Suche zur Vefügung. 

<a name="detail"></a>
## Detailansicht

Klickt man in der Übersicht einer Kategorie auf den Titel eines Mediums, erhält man die Detailansicht.
Über die Detailansicht kann die Kategorie des Mediums gewechselt werden, das Medium getauscht werden, Titel- und ggf. (je nach Installation) weitere Informationen zum Medium hinterlegt werden. Über die Schaltfläche **Aktualisieren** werden Änderungen übernommen.

<a name="kategorien"></a>
## Medienkategorien verwalten

Im Reiter **Medienkategorien verwalten** können neue Kategorien angelegt und vorhandene editiert oder gelöscht werden. Zum Anlegen einer neuen Kategorie, klickt man auf das (+)-Symbol neben der Bezeichnung **Name** und trägt den Kategorienamen in das entsprechende Textfeld ein. Das Editieren beschränkt sich auf eine Umbenennung der Kategorie. Kategorien können nur gelöscht werden, wenn sie keine Medien beinhalten. Ansonsten erscheint ein Warnhinweis. 

> Tipp: Das Verschieben einer Kategorie ist aktuell nicht vorgesehen. Daher sollte man die Kategorisierung der Medien vor Projektbeginn ausführlich planen. 

<a name="upload"></a>
## Medien hinzufügen

Zum Hochladen von Dateien in den Medienpool, wählt man den Reiter “Medium hinzufügen”. 
Hier kann man zum Medium ein Titel hinterlegen und, je nach Installation, weitere Felder ausfüllen. Um eine Datei einer Kategorie zuzuordnen, kann man vor dem Upload gleich die passende Medienkategorie festlegen. Das gewünschte Medium wählt man im Abschnitt Datei. Dort steht eine Schaltfläche zum Aufruf des eigenen Dateisystems bereit. Der Ladevorgang wird dann aus gelöst mit der Schaltfläche “hinzufügen”. 

<a name="loeschen"></a>
## Medien löschen

### Löschen über Detailansicht
- Mit der Schaltfläche **Löschen** in der Detailansicht des Mediums entfernt man das Medium aus dem Medienpool. 

### Löschen über Detailansicht
- Zu löschende Dateien werden über die Checkboxen ausgewählt.
- Anschließen Scrollen zum Ende der Liste
- Bestätigen des Löschvorgangs durch Klick auf “löschen”

> Möchte man die Aktion auf alle Medien der Kategorie anwenden, kann man alle Medien mit der Checkbox am Ende der Liste markieren. 

> Sollte das Medium in Verwendung sein, wird das Medium nicht gelöscht. Es wird eine Liste angzeigt, wo das Medium in Verwendung ist. 

<a name="tausch"></a>
## Datei austauschen (ersetzen)

Anstelle eines neuen Uploads und Neuverlinken aller Vorkommen eines Mediums, kann man ganz einfach ein vorhandenes Medium durch ein neues ersetzen. Hierbei wird das alte Medium überschrieben, der Dateiname bleibt jedoch bestehen. Unter **Datei tauschen** in der Detailansicht, findet man eine Uploadmöglichkeit für den Austausch der Datei. 

<a name="schieben"></a>
## Medien verschieben
Das Verschieben eines Mediums in eine andere Kategorie kann wahlweise über die Detailansicht erfolgen oder auch für mehrere Dateien in der Liste der Medien erfolgen. 

### Verschieben über Detailansicht
- Aufruf der Detailansicht eines Mediums
- Auswahl einer neuen Kategorie
- bestätigen mit “aktualisieren”

### Verschieben über Liste der Medien
- Über die Checkboxen die Medien markieren, die verschoben werden sollen 
- Zum Ende der Liste scrollen
- Unter “Ausgewählte Medien - in Kategorie” die neue Kategorie auswählen und auf “verschieben” klicken

 > Möchte man die Aktion auf alle Medien der Kategorie anwenden, kannst man alle Medien mit der Checkbox am Ende der Liste markieren.

<a name="sync"></a>
## Dateien synchronisieren

Um mehrere Dateien in den Medienpool zu importieren, gibt es die Funktion “Dateien synchronisieren”. Alle zusätzlich (z.B. per SFTP, WebDAV) in den Ordner “/media” geladenen Dateien werden dann unter “betroffene Dateien” gelistet. Man wählt die Dateien mit einem Häkchen vor dem Dateinamen aus und die entsprechende Medienkategorie. Durch Klick auf “Synchronisieren” werden dann alle gewählten Dateien in die ausgewählte Medienkategorie eingespielt. Beim Synchronisieren einzelner Dateien kann man hier auch gleich den Titel vergeben, bei mehreren Dateien muss man das im Nachhinein in der jeweiligen Detailansicht machen.

> **Achtug**: Es sollte darauf geachtet werden, dass die neuen Dateien, die in den Medienordner kopiert werden sollen keine vorhandenen Dateien überschreiben (gleicher Dateiname). Ein Backup des Verzeichnisses und der Datebank sollte möglichst vorher erfolgen.  

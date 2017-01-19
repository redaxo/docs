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
Nach Aufruf des Medienpools über den Menüpunkt “Medienpool”, gelangst du direkt in die Liste der Medien. Hier werden alle Medien der aktuell gewählten Kategorie gelistet. Medien, die keiner Kategorie zugeordnet sind, werden in der Hauptebene unter “Keine Kategorie” gelistet. Zur Auswahl einer Kategorie, steht dir ein Auswahlmenü neben der Suche zur Vefügung. 

<a name="detail"></a>
## Detailansicht

Klickst du in der Übersicht einer Kategorie auf den Titel eines Mediums, gelangst du in die Detailansicht.
Über die Detailansicht kann man die Kategorie wechseln, die Medien ändern, Titel- und ggf. (je nach Installation) weitere Informationen zum Medium hinterlegen. Über die Schaltfläche **Aktualisieren** werden Änderungen übernommen.

<a name="kategorien"></a>
## Medienkategorien verwalten

Unter der Überschrift **Medienkategorien verwalten** können neue Kategorien angelegt und vorhandene editiert oder gelöscht werden. Zum Anlegen einer neuen Kategorie klickt man auf das Plus-Symbol neben der Bezeichnung **Name** und trägt den Kategorienamen in das entsprechende Textfeld ein. Das Editieren beschränkt sich auf eine Umbenennung der Kategorie. Kategorien können nur gelöscht werden, wenn sie keine Dateien beinhalten. Ansonsten erscheint ein Warnhinweis. 

<a name="upload"></a>
## Medien hinzufügen

Zum Hochladen von Dateien in den Medienpool, wählt man den Menüpunkt “Medium hinzufügen”. Hier kann zu der Datei ergänzend ein Titel angegeben werden. Um eine Datei gleich richtig einer Kategorie zuzuordnen, kann beim Upload gleich die entsprechende Medienkategorie auswählen.

<a name="loeschen"></a>
## Medien löschen

### Löschen über Detailansicht
- Mit der Schaltfläche **Löschen** in der Detailansicht des Mediums entfernst du das Medium aus dem Medienpool. 

### Löschen über Detailansicht
- Markiere mit den Checkboxen die Medien, die du löschen möchtest 
- Scrolle an das Ende der Liste
- Klicke dann auf “löschen”

> Möchtest du die Aktion auf alle Medien der Kategorie anwenden, kannst du alle Medien mit der Checkbox am Ende der Liste markieren. 

> Sollte das Medium in Verwendung sein, wird das Medium nicht gelöscht. Es wird eine Liste angzeigt, wo das Medium in Verwendung ist. 

<a name="tausch"></a>
## Datei austauschen (ersetzen)

Anstelle eines neuen Uploads und Neuverlinken aller Vorkommen eines Mediums, kannst du ganz einfach ein vorhandenes Medium durch ein neues ersetzen. Hierbei wird das alte Medium überschrieben, der Dateiname bleibt jedoch bestehen. Unter **Datei tauschen** in der Detailansicht, findest du eine Uploadmöglichkeit für den Austausch der Datei. 

<a name="schieben"></a>
## Medien verschieben
Das Verscheiben eines Mediums in eine andere Kategorie kannst du wahlweise über die Detailansicht durchführen oder auch für mehrere Dateien in der Liste der Medien durchführen. 

### Verschieben über Detailansicht
- Rufe die Detailansicht des Mediums auf
- Wähle eine neue Katgorie
- bestätige dann mit “aktualisieren”

### Verschieben über Liste der Medien
- Markiere mit den Checkboxen die Medien, die du verschieben möchtest 
- Scrolle an das Ende der Liste
- Wähle dann unter “Ausgewählte Medien - in Kategorie” die neue Kategorie aus und klicke dann auf “verschieben”

 > Möchtest du die Aktion auf alle Medien der Kategorie anwenden, kannst du alle Medien mit der Checkbox am Ende der Liste markieren.

<a name="sync"></a>
## Dateien synchronisieren

Um mehrere Dateien gleichzeitig in den Medienpool hochzuladen, gibt es die Funktion “Dateien synchronisieren”. Alle zusätzlich per FTP in den Ordner “/media” geladenen Dateien werden dann unter “betroffene Dateien” gelistet. Man wählt die Dateien mit einem Häkchen vor dem Dateinamen aus und die entsprechende Medienkategorie. Durch Klick auf “Synchronisieren” werden dann alle gewählten Dateien in die ausgewählte Medienkategorie eingespielt. Beim Synchronisieren einzelner Dateien kann man hier auch gleich den Titel vergeben, bei mehreren Dateien muss man das im Nachhinein in der jeweiligen Detailansicht machen.

> **Achtug**: Achte darauf, dass die neuen Dateien, die du per FTP in den Medienordner kopierst keine vorhandenen Dateien überschreiben (gleicher Dateiname). Führe vorher ein Backup des Verzeichnisses und der Datebank durch.  

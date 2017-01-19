# Medienpool
Der Medienpool stellt die Funktionen zur Verwaltung von Mediendateien wie Bilder, Dokumente und Videos bereit. Die Medien können über Kategorien organisiert werden. Der Medienpool wird nach einem Klick auf den Link Medienpool in einem eigenen Fenster geöffnet.

## Medien verwalten

Im Medienpool werden nur die Dateien angezeigt, die über Upload- oder Synchronisationsfunktion auf den Server geladen wurden. Alle Medien, die mit dem Medienpool verwaltet werden, befinden sich in dem Ordner “/media” der Redaxo-Installation.
Um die Sortierung übersichtlicher zu gestalten, kann man Kategorien definieren und die hochgeladenen Dateien diesen Kategorien zuweisen. 

**Liste der Medien**

Zu jeder Kategorie kann man sich die entsprechenden Dateien anzeigen lassen. Durch Klick auf den Bildtitel erhält man die Detailinformationen.

**Detailansicht**

Klicken in der Übersicht einer Kategorie auf den Titel eines Mediums, du gelangst dann in die Detailansicht.
Über die Detailansicht kann man die Kategorie wechseln, die Datei ändern, Titel- und ggf. (je nach Installation) weitere Informationen zum Medium hinterlegen. Über die Schaltfläche **Aktualisieren** werden Änderungen übernommen.


## Medienkategorien verwalten

Unter der Überschrift **Medienkategorien verwalten** können neue Kategorien angelegt und vorhandene editiert oder gelöscht werden. Zum Anlegen einer neuen Kategorie klickt man auf das Plus-Symbol neben der Bezeichnung **Name** und trägt den Kategorienamen in das entsprechende Textfeld ein. Das Editieren beschränkt sich auf eine Umbenennung der Kategorie. Kategorien können nur gelöscht werden, wenn sie keine Dateien beinhalten. Ansonsten erscheint ein Warnhinweis. 

## Medien hinzufügen

Zum Hochladen von Dateien in den Medienpool, wählt man den Menüpunkt “Medium hinzufügen”. Hier kann zu der Datei ergänzend ein Titel angegeben werden. Um eine Datei gleich richtig einer Kategorie zuzuordnen, kann beim Upload gleich die entsprechende Medienkategorie auswählen.

## Medien löschen

### Löschen über Detailansicht
- Mit der Schaltfläche **Löschen** in der Detailansicht des Mediums entfernst du das Medium aus dem Medienpool. 

### Löschen über Detailansicht
- Markiere mit den Checkboxen die Medien, die du löschen möchtest 
- Scrolle an das Ende der Liste
- Klicke dann auf “löschen”

 > Möchtest du die Aktion auf alle Medien der Kategorie anwenden, kannst du alle Medien mit der Checkbox am Ende der Liste markieren. 

 > Sollte das Medium in Verwendung sein, wird das Medium nicht gelöscht. Es wird eine Liste angzeigt, wo das Medium in Verwendung ist. 

## Datei  austauschen (ersetzen)

Anstelle eines neuen Uploads und Neuverlinken aller Vorkommen eines Mediums, kannst du ganz einfach ein vorhandenes Medium durch ein neues ersetzen. Hierbei wird das alte Medium überschrieben, der Dateiname bleibt jedoch bestehen. Unter **Datei tauschen** findest du eine Uploadmöglichkeit für den Austausch der Datei.  


## Medien verschieben
Das Verscheiben eines Mediums in eine andere Kategorie kannst du wahlweise über die Detailansicht durchführen oder auch für mehrere Dateien in der Liste der Medien durchführen. 

### Verscheiben über Detailansicht
- Rufe die Detailansicht des Mediums auf
- Wähle eine neue Katgorie
- bestätige dann mit “aktualisieren”

### Verschieben über Liste der Medien
- Markiere mit den Checkboxen die Medien, die du verschieben möchtest 
- Scrolle an das Ende der Liste
- Wähle dann unter “Ausgewählte Medien - in Kategorie” die neue Kategorie aus und klicke dann auf “verschieben”

 > Möchtest du die Aktion auf alle Medien der Kategorie anwenden, kannst du alle Medien mit der Checkbox am Ende der Liste markieren.

## Dateien synchronisieren

Um mehrere Dateien gleichzeitig in den Medienpool hochzuladen, gibt es die Funktion “Dateien synchronisieren”. Alle per FTP in den Ordner “/media” geladenen Dateien werden dann unter “betroffene Dateien” gelistet. Man wählt die Dateien mit einem Häkchen vor dem Dateinamen aus und die entsprechende Medienkategorie. Durch Klick auf “Synchronisieren” werden dann alle gewählten Dateien in die ausgewählte Medienkategorie eingespielt. Beim Synchronisieren einzelner Dateien kann man hier auch gleich den Titel vergeben, bei mehreren Dateien muss man das im Nachhinein in der jeweiligen Detailansicht machen.

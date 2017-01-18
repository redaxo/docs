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
 
Mit der Schaltfläche **Löschen** in der Detailansicht des Mediums entfernst du das Medium aus dem Medienpool. 
  > Sollte das Medium in Verwendung sein, wird das Medium nicht gelöscht. 

## Dateien tauschen / ersetzen
...

## Dateien verschieben
...


## Dateien synchronisieren

Um mehrere Dateien gleichzeitig in den Medienpool hochzuladen, gibt es die Funktion “Dateien synchronisieren”. Alle per FTP in den Ordner “/media” geladenen Dateien werden dann unter “betroffene Dateien” gelistet. Man wählt die Dateien mit einem Häkchen vor dem Dateinamen aus und die entsprechende Medienkategorie. Durch Klick auf “Synchronisieren” werden dann alle gewählten Dateien in die ausgewählte Medienkategorie eingespielt. Beim Synchronisieren einzelner Dateien kann man hier auch gleich den Titel vergeben, bei mehreren Dateien muss man das im Nachhinein in der jeweiligen Detailansicht machen.

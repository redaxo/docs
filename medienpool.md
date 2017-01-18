# Medienpool

Über den Medienpool können Dateien auf den Server geladen, verwaltet und gelöscht werden. Im Allgemeinen werden darüber Grafiken und Textdateien verwaltet. Es können aber auch beliebige andere Dateitypen bearbeitet werden.

Der Medienpool wird nach einem Klick auf den Link Medienpool in einem eigenen Fenster geöffnet.

# Medien verwalten

Im Medienpool werden nur die Dateien angezeigt, die über Upload- oder Synchronisationsfunktion auf den Server geladen wurden. Alle Dateien, die mit dem Medienpool verwaltet werden, befinden sich in dem Ordner “/media” der Redaxo-Installation.

Um die Sortierung übersichtlicher zu gestalten, kann man Kategorien definieren und die hochgeladenen Dateien diesen Kategorien zuweisen. 

**Übersicht**

Zu jeder Kategorie kann man sich die entsprechenden Dateien anzeigen lassen. Durch Klick auf den Bildtitel erhält man die Detailinformationen.

**Detailansicht**

Klicken Sie in der Übersicht einer Kategorie auf den Titel einer Datei, so gelangen Sie zur Detailansicht.
Über die Detailansicht kann man die Kategorie wechseln, die Datei ändern, Titel-, Beschreibungs- und Copyrighttexte einfügen oder die Datei löschen. Über die Schaltfläche **Aktualisieren** werden die Änderungen übernommen. 

Dateien können aus dem Medienpool nur gelöscht werden, wenn die Datei nicht in einem Artikel/Block eingefügt ist. Andernfalls erscheint eine Warnmeldung mit der Information, in welchen Artikeln diese Datei eingebunden ist.

## Medienkategorien verwalten

Unter der Überschrift **Medienkategorien verwalten** können neue Kategorien angelegt und vorhandene editiert oder gelöscht werden. Zum Anlegen einer neuen Kategorie klickt man auf das Plus-Symbol neben der Bezeichnung **Name** und trägt den Kategorienamen in das entsprechende Textfeld ein. Das Editieren beschränkt sich auf eine Umbenennung der Kategorie. Kategorien können nur gelöscht werden, wenn sie keine Dateien beinhalten. Ansonsten erscheint ein Warnhinweis.

## Dateien hinzufügen

Zum Hochladen von Dateien in den Medienpool bzw. das Verzeichnis “/media”, wählt man den Menüpunkt “Datei hinzufügen”. Hier kann zu der Datei ergänzend ein Titel angegeben werden. Um eine Datei gleich richtig einer Kategorie zuzuordnen, kann beim Upload gleich die entsprechende Medienkategorie auswählen.

## Dateien synchronisieren

Um mehrere Dateien gleichzeitig in den Medienpool hochzuladen, gibt es die Funktion “Dateien synchronisieren”. Alle per FTP in den Ordner “/media” geladenen Dateien werden dann unter “betroffene Dateien” gelistet. Man wählt die Dateien mit einem Häkchen vor dem Dateinamen aus und die entsprechende Medienkategorie. Durch Klick auf “Synchronisieren” werden dann alle gewählten Dateien in die ausgewählte Medienkategorie eingespielt. Beim Synchronisieren einzelner Dateien kann man hier auch gleich den Titel vergeben, bei mehreren Dateien muss man das im Nachhinein in der jeweiligen Detailansicht machen.

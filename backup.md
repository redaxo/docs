# Backup
Mit dem Backup-Addon kannst du du die Datenbank und die Dateien deiner Redaxo-Installation sichern und wiederherstellen.
Sobald das AddOn installiert und aktiviert wurde, erscheint der Bereich “Backup” in der AddOns-Navigationsleiste des Backends.


## Daten exportieren

Die Daten der Datenbank und die Dateien werden jeweils separat gespeichert. Die exportierten Daten können direkt auf dem Server gespeichert oder als Dateien heruntergeladen werden, je nach Bedarf. Beim Testen von verschiedenen Varianten von Funktionen beispielsweise, kann zuvor eine Sicherung durchgeführt werden. Diese speichert den Ist-Zustand ab und kann auf dem Server belassen werden. Falls die Änderung sich als nicht sinnvoll erwiesen hat, kann direkt auf diese zurückgegriffen werden. Das Herunterladen als Datei ermöglicht das Sichern der Daten auf einem anderen Rechner.

Beim Datenbank-Export wird eine .sql-Datei erzeugt, die die Struktur und die Inhalte der gewünschten Tabellen deiner Redaxo-Installation enthält. Beim Export schlägt das Addons die wichtigsten Tabellen zur Sicherung vor. Weitere Tabellen können zur Sicherung ausgewählt werden. 
Beim Dateiexport werden die ausgewählten Dateien und/oder Verzeichnisse in komprimierter Form gespeichert.


Redaxo schlägt automatisch einen Dateinnamen für die exportierten Daten vor. Dieser Name kann aber beliebig verändert werden.

Wählen Sie die Option “Auf dem Server speichern” wird die Datei auf dem Server gespeichert und hier unter Import angezeigt. Sie finden die auf dem Server gespeicherte Datei im Ordner “/redaxo/include/addons/import_export/files”.

## Daten importieren

Datenbank-Import
Datenbankimport
Unter “Datenbankimport” können Sie die Redaxo-Tabellen und deren Inhalte importieren. Sie haben die Möglichkeit, entweder eine extern gespeicherte, zuvor exportierte sql-Datei auszuwählen und zu importieren. Klicken Sie dazu auf “Durchsuchen”, wählen Sie eine sql-Datei von Ihrem Rechner aus und bestätigen Sie die Auswahl durch Klicken auf den “Import”-Button.

Oder Sie wählen eine der hier gelisteten, auf dem Server gespeicherten Import-Dateien aus, indem Sie auf das rot markierte “Import” klicken.

> In beiden Fällen werden die bisherigen Inhalte der Datenbank gelöscht und überschrieben! Dieser Vorgang kann nicht wieder rückgängig gemacht werden.


## Dateien-Import
Dateienimport
Danach können Sie unter Dateienimport die benötigten Dateien importieren. Hier gibt es wieder sowohl die Möglichkeit, eine lokal gespeicherte, exportierte Datei auszuwählen als auch auf eine der auf dem Server gespeicherten Dateien zurückzugreifen.

Nach erfolgreichem Import werden alle Artikel sowie der Cache neu generiert. Auch hier gilt wieder: alle “alten” Dateien werden gelöscht.

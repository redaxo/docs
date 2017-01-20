# Backup
Wie bei jeder Software oder Website macht es Sinn, gerade vor größeren Veränderungen am System oder vor dem Umzug auf einen neuen Server, ein Backup durchzuführen. Redaxo stellt dir über das Backup-Addon die Möglichkeit zur Verfügung sämtliche Daten deiner Webpräsenz über eine einfache Oberfläche zu sichern und zu Importieren. Zudem ist es möglich, in Kombination mit einem Cronjob, regelmäßige Sicherungen der Daten durchzuführen.  

Sobald das AddOn installiert und aktiviert wurde, erscheint der Bereich “Backup” in der AddOns-Navigationsleiste des Backends.

Das Backup-Addon unterscheidet zwischen Datenbank und Dateien. Für eine komplette Sicherung der Website sind also beide Schritte durchzuführen. 

![Screenshot](/assets/v5.2.0-backup-01-overview.png)
Screenshot: Datenbank-Backup

## Datenbankexport
Beim Datenbank-Export wird eine .sql-Datei erzeugt, die die Struktur und die Inhalte der gewünschten Tabellen deiner Redaxo-Installation enthält. Beim Export schlägt das Addons die wichtigsten Tabellen zur Sicherung vor. Weitere Tabellen können zur Sicherung ausgewählt werden. Du kannst wählen, ob die Sicherung auf dem Server abgelegt werden soll oder ob di die erzeugte Datei herunterladen möchtest. 

**3 Schritte zum Datenbank-Export:** 
- Wähle evtl. weitere Tabellen zur Sichrerung aus
- Wähle den gewünschten Speicherort
- Um die Sicherung anzustoßen klicke auf “exportieren”.

> Möchtest du auch die Zugangsdaten der Redakteure sichern, wähle zusätzlich die Tabelle **rex_user** aus. 

![Screenshot](/assets/v5.2.0-backup-02-files.png)
Screenshot: Datei-Backup

## Dateiexport
Beim Dateiexport werden die ausgewählten Dateien und/oder Verzeichnisse in komprimierter Form gespeichert. Redaxo selbst wird hier nicht gesichert. Eine Vorauswahl von Dateien findet nicht statt. 

**3 Schritte zum Datei-Export:** 
- Wähle die gewünschten Ordner auf dem Server Sichrerung aus
- Wähle den gewünschten Speicherort
- Um die Sicherung anzustoßen klicke auf “exportieren”.



## Daten importieren

Unter “Datenbankimport” können Sie die Redaxo-Tabellen und deren Inhalte importieren. Sie haben die Möglichkeit, entweder eine extern gespeicherte, zuvor exportierte sql-Datei auszuwählen und zu importieren. Klicken Sie dazu auf “Durchsuchen”, wählen Sie eine sql-Datei von Ihrem Rechner aus und bestätigen Sie die Auswahl durch Klicken auf den “Import”-Button.

Oder du wählst eine der hier gelisteten, auf dem Server gespeicherten Import-Dateien aus, indem du auf das rot markierte “Import” klicken.

> In beiden Fällen werden die bisherigen Inhalte der Datenbank gelöscht und überschrieben! Dieser Vorgang kann nicht wieder rückgängig gemacht werden.


## Dateien-Import
Dateienimpo
Danach können Sirte unter Dateienimport die benötigten Dateien importieren. Hier gibt es wieder sowohl die Möglichkeit, eine lokal gespeicherte, exportierte Datei auszuwählen als auch auf eine der auf dem Server gespeicherten Dateien zurückzugreifen.

Nach erfolgreichem Import werden alle Artikel sowie der Cache neu generiert. Auch hier gilt wieder: alle “alten” Dateien werden gelöscht.

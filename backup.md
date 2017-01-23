# Backup
Vor größeren Veränderungen am System oder vor dem Umzug auf einen neuen Server sollte man eine Datensicherung durchführen. 
Für kleinere Webpräsenzen steht in Redaxo ein [Backup-Addon](#addon) zur Sicherung der Datenbank und ausgewählter Dateiordner zur Verfügung. Zudem ist es möglich, in Kombination mit einem Cronjob, regelmäßige Sicherungen der Datenbank durchzuführen.

> Da das Backup-Addon abhängig von der Laufzeitkonfiguration der PHP-Installation ist, kann es bei großen Datenbeständen zu Abbrüchen des Sicherungsvorgangs kommen. Hier sollten entweder die Laufzeitparameter geändert werden, oder eine manuelle Sicherung per FTP(s) und PHPMyadmin durchgeführt werden. 

Tägliche Backups sollten möglichst automatisch über die im Webhosting des Providers bereitgestellten Sicherungsmöglichkeiten (z.B. in [Plesk](https://www.plesk.com/)) erfolgen. 

- [Backup-Addon](#addon)
  - [Datenbank-Export](#dbexport)
  - [Datei-Export](#fileexport)
  - [Daten importieren](#import)
    - [Upload](#upload)
    - [Vom Server laden](#fromserver)

<a name="addon"></a>
## Backup-Addon 

Sobald das AddOn installiert und aktiviert wurde, erscheint der Bereich “Backup” in der AddOns-Navigationsleiste des Backends.
Das Backup-Addon unterscheidet zwischen Datenbank und Dateien. Für eine komplette Sicherung der Website müssen beide Schritte durchgeführt werden. 


<a name="dbexport"></a>
### Datenbank-Export

![Screenshot](/assets/v5.2.0-backup-01-overview.png)
Screenshot: Datenbank-Backup

Beim Datenbank-Export wird eine *.sql*-Datei erzeugt, welche die Struktur und Inhalte der gewünschten Tabellen deiner Redaxo-Installation enthält. Beim Export schlägt das Addons die wichtigsten Tabellen zur Sicherung vor. Weitere Tabellen können zur Sicherung ausgewählt werden. Du kannst wählen, ob die Sicherung auf dem Server abgelegt werden soll oder ob du die erzeugte Datei herunterladen möchtest. 

**3 Schritte zum Datenbank-Export:** 
- Wähle optional weitere Tabellen zur Sichrerung aus
- Wähle den gewünschten Speicherort
- Klicke auf “exportieren” um die Sicherung zu starten

> Wähle zusätzlich die Tabelle **rex_user** aus, wenn du auch die Zugangsdaten der Redakteure sichern möchtest. 

<a name="fileexport"></a>
### Datei-Export

![Screenshot](/assets/v5.2.0-backup-02-files.png)
Screenshot: Datei-Backup

Beim Datei-Export werden die ausgewählten Dateien und/oder Verzeichnisse in komprimierter Form gespeichert. Redaxo selbst wird hier nicht gesichert. Eine Vorauswahl von Dateien findet nicht statt. 

**3 Schritte zum Datei-Export:** 
- Wähle die gewünschten Ordner auf dem Server Sichrerung aus
- Wähle den gewünschten Speicherort
- Klicke auf “exportieren” um die Sicherung zu starten

<a name="import"></a>
### Daten importieren

Im Reiter **Import** kannst du deine Sicherungen einspielen. Hierzu kannst du Sicherungen von deinem Rechner hochladen oder die auf dem Server gespeicherten Sicherungen wiederherstellen. 

> **Hinweis** die vorhandenen Daten (Datenbank und Dateien) werden hierbei gelöscht. 

<a name="upload"></a>
#### Upload

Im Abschnitt **Upload** kannst du deine Sicherungsdateien hochladen und einspielen.  

![Screenshot](/assets/v5.2.0-backup-03-upload.png)
Screenshot: Datenimport Upload

- Unter Datenbankexport kannst du eine Datenbanksicherung einspielen
- Unter Dateiexport kannst du eine Dateisicherung einspielen

Klicke auf das jeweilige Dateiauswahlfeld um eine bei dir lokal gespeicherte Sicherung auszuwählen. Bestätige dann den Upload mit der Schaltfläche **Import**. 

Wichtig: Führe keine weiteren Schritte in Redaxo durch, bis der Import beendet ist!

<a name="fromserver"></a>
#### Vom Server laden

Im Abschnitt **Vom Server laden** spielst du Sicherungen die auf dem Server gespeichert wurden wieder ein. 

![Screenshot](/assets/v5.2.0-backup-04-fromserver.png)
Screenshot: Datenimport vom Server

- Unter Datenbank-Exporte werden dir die Sicherungen der Datenbank gelistet
- Unter Datei-Exporte siehst du die Liste der Dateisicherungen

Um eine Datenbank- oder Dateisicherung wieder einzuspielen, klicke in der jeweiligen Zeile auf **importieren**. 

Wichtig: Führe keine weiteren Schritte in Redaxo durch, bis der Import beendet ist!

Nach erfolgreichem Import werden alle Artikel sowie der Cache neu generiert. Alte Daten werden vom Server gelöscht. 

# Backup
Wie bei jeder Software oder Website ist es sinnvoll, gerade vor größeren Veränderungen am System oder vor dem Umzug auf einen neuen Server, ein Backup durchzuführen. Redaxo stellt dir über das Backup-Addon die Möglichkeit zur Verfügung sämtliche Daten deiner Webpräsenz über eine einfache Oberfläche zu sichern und zu Importieren. Zudem ist es möglich, in Kombination mit einem Cronjob, regelmäßige Sicherungen der Daten durchzuführen.  

Sobald das AddOn installiert und aktiviert wurde, erscheint der Bereich “Backup” in der AddOns-Navigationsleiste des Backends.

Das Backup-Addon unterscheidet zwischen Datenbank und Dateien. Für eine komplette Sicherung der Website sind also beide Schritte durchzuführen. 

- [Datenbankexport](#dbexport)
- [Dateiexport](#fileexport)
- [Daten importieren](#import)
  - [Upload](#upload)
  - [Vom Server](#fromserver)

<a name="dbexport"></a>
## Datenbankexport

![Screenshot](/assets/v5.2.0-backup-01-overview.png)
Screenshot: Datenbank-Backup

Beim Datenbank-Export wird eine .sql-Datei erzeugt, die die Struktur und die Inhalte der gewünschten Tabellen deiner Redaxo-Installation enthält. Beim Export schlägt das Addons die wichtigsten Tabellen zur Sicherung vor. Weitere Tabellen können zur Sicherung ausgewählt werden. Du kannst wählen, ob die Sicherung auf dem Server abgelegt werden soll oder ob di die erzeugte Datei herunterladen möchtest. 

**3 Schritte zum Datenbank-Export:** 
- Wähle evtl. weitere Tabellen zur Sichrerung aus
- Wähle den gewünschten Speicherort
- Um die Sicherung anzustoßen klicke auf “exportieren”.

> Möchtest du auch die Zugangsdaten der Redakteure sichern, wähle zusätzlich die Tabelle **rex_user** aus. 

<a name="fileexport"></a>
## Dateiexport

![Screenshot](/assets/v5.2.0-backup-02-files.png)
Screenshot: Datei-Backup

Beim Dateiexport werden die ausgewählten Dateien und/oder Verzeichnisse in komprimierter Form gespeichert. Redaxo selbst wird hier nicht gesichert. Eine Vorauswahl von Dateien findet nicht statt. 

**3 Schritte zum Datei-Export:** 
- Wähle die gewünschten Ordner auf dem Server Sichrerung aus
- Wähle den gewünschten Speicherort
- Um die Sicherung anzustoßen klicke auf “exportieren”.

<a name="import"></a>
## Daten importieren

Im Reiter Import kannst du deine Sicherungen einspielen. Hierzu kannst du Sicherungen von deinem Rechner hochladen oder die auf dem Server gespeicherten Sicherungen wiederherstellen. 

> **Hinweis** die vorhandenen Daten (Datenbank und Dateien) werden hierbei gelöscht. 

<a name="upload"></a>
### Upload

Im Abschnitt **Upload** kannst du deine Sicherungsdateien hochladen und einspielen.  

![Screenshot](/assets/v5.2.0-backup-03-upload.png)
Screenshot: Datenimport Upload

- Unter Datenbankexport kannst du eine Datenbanksicherung einspielen
- Unter Dateiexport kannst du eine Dateisicherung einspielen

Klicke auf das jeweilige Dateiauswahlfeld um eine bei dir lokal gespeicherte Sicherung auszuwählen. Bestätige dann den Upload mit der Schaltfläche Import. 
Führe keine weiteren Schritte in Redaxo durch, bis der Import beendet ist. 

<a name="fromserver"></a>
### Vom Server laden

Im Abschnitt **Vom Server laden** spielst du Sicherungen die auf dem Server gespeichert wurden wieder ein. 

![Screenshot](/assets/v5.2.0-backup-04-fromserver.png)
Screenshot: Datenimport vom Server

- Unter Datenbankexporte werden dir die Sicherungen der Datenbank gelistet
- Unter Dateiexporte siehst du die Liste der Dateisicherungen

Um eine Datenbank- oder Dateisicherung wieder einzuspielen, klicke in der jeweiligen Zeile auf **importieren**. 
Führe keine weiteren Schritte in Redaxo durch, bis der Import beendet ist. 
Nach erfolgreichem Import werden alle Artikel sowie der Cache neu generiert. Alte Daten werden vom Server gelöscht. 

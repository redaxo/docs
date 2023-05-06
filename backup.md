# Backup

* [Backup-Hinweise](#backup-hinweise)
* [Backup-AddOn](#addon)
  + [Datenbank-Export](#dbexport)
  + [Datei-Export](#fileexport)
  + [Daten importieren](#import)
    - [Upload](#upload)
    - [Vom Server laden](#fromserver)

<a name="backup-hinweise"></a>

## Backup-Hinweise

Vor größeren Veränderungen am System oder vor dem Umzug auf einen neuen Server sollte eine Datensicherung durchgeführt werden.
Für kleinere Webpräsenzen steht in REDAXO ein [Backup-AddOn](#addon) zur Sicherung der Datenbank und ausgewählter Dateiordner zur Verfügung. Zudem ist es möglich, in Kombination mit einem Cronjob regelmäßige Sicherungen der Datenbank durchzuführen.

> Da das Backup-AddOn abhängig von der Laufzeitkonfiguration der PHP-Installation ist, kann es bei großen Datenbeständen zu Abbrüchen des Sicherungsvorgangs kommen. Hier sollten entweder die Laufzeitparameter geändert werden, oder eine manuelle Sicherung per FTP(s) und PHPMyadmin durchgeführt werden.
> **Backups älterer REDAXO-Versionen als 5.0**
> Das Einspielen eines REDAXO-Backups älterer Versionen als 5.0 ist nicht vorgesehen.

Tägliche Backups sollten möglichst automatisch über die im Webhosting des Providers bereitgestellten Sicherungsmöglichkeiten (z. B. in [Plesk](https://www.plesk.com/)) erfolgen.

<a name="addon"></a>

## Backup-AddOn

Das Backup-AddOn ist über den Menüpunkt `Backup` erreichbar.
Es unterscheidet zwischen Datenbank und Dateien. Für eine komplette Sicherung der Website sollten die Datenbank und die wichtigsten Dateien gesichert werden. Eine Sicherung von REDAXO selbst findet nicht statt.

Zur Speicherung der Backups können "Auf dem Server speichern" (Speicherort: `redaxo/data/addons/backup`) oder ein direkter Download gewählt werden. 

<a name="dbexport"></a>

### Datenbank-Export

![Screenshot](/assets/v5.2.0-backup-01-overview.png)

Screenshot: Datenbank-Backup

Beim Datenbank-Export wird eine *.sql*-Datei erzeugt, welche die Struktur und Inhalte der gewünschten Tabellen der REDAXO-Installation enthält. Beim Export schlägt das AddOn die wichtigsten Tabellen zur Sicherung vor. Weitere Tabellen können zur Sicherung ausgewählt werden. Des Weiteren kann ausgewählt werden, ob die Sicherung nach Abschluss des Vorgangs auf dem Server abgelegt oder auf den Computer heruntergeladen werden soll.

**Drei Schritte zum Datenbank-Export:**

* Optional weitere Tabellen zur Sicherung auswählen
* Gewünschten Speicherort auswählen
* Ein Klick auf `Exportieren` startet die Sicherung

> **Tipp:** Wenn auch die Zugangsdaten der Redakteure gesichert werden sollen, muss zusätzlich die Tabelle **rex_user** ausgewählt werden.

<a name="fileexport"></a>

### Datei-Export

![Screenshot](/assets/v5.2.0-backup-02-files.png)

Screenshot: Datei-Backup

Beim Datei-Export werden die ausgewählten Dateien und/oder Verzeichnisse in komprimierter Form gespeichert. REDAXO selbst wird hier nicht gesichert. Eine Vorauswahl von Dateien findet nicht statt.

**Drei Schritte zum Datei-Export:**

* Die gewünschten Ordner auf dem Server zur Sicherung auswählen
* Den gewünschten Speicherort auswählen
* Ein Klick auf `Exportieren` startet die Sicherung

<a name="import"></a>

### Daten importieren

Im Reiter `Import` können Sicherungen vom Computer hochgeladen oder die auf dem Server gespeicherten Sicherungen wiederhergestellt werden.

> **Hinweis:** Die vorhandenen Daten (Datenbank und Dateien) werden hierbei gelöscht.

<a name="upload"></a>

#### Upload

Im Abschnitt `Upload` können Sicherungsdateien hochgeladen und eingespielt werden.  

![Screenshot](/assets/v5.2.0-backup-03-upload.png)

Screenshot: Daten-Import Upload

* Die Datenbank-Sicherung kann unter "Datenbank-Backup wiederherstellen" eingespielt werden
* Die Datei-Sicherung kann unter "Datei-Backup wiederherstellen" eingespielt werden

Mit einem Klick auf das jeweilige Dateiauswahlfeld kann die lokal gespeicherte Sicherung ausgewählt und mit einem Klick auf `Import` hochgeladen werden.

> **Wichtig:** Bis zum Abschluss des Imports dürfen keine weiteren Aktionen in REDAXO ausgeführt werden!

<a name="fromserver"></a>

#### Vom Server laden

Im Abschnitt `Vom Server laden` kann man Sicherungen, die auf dem Server gespeichert wurden, wieder einspielen.

![Screenshot](/assets/v5.2.0-backup-04-fromserver.png)

Screenshot: Daten-Import vom Server

* `Datenbank-Exporte` listet die Sicherungen der Datenbank auf.
* `Datei-Exporte` zeigt die Liste der Datei-Sicherungen.

Um eine Datenbank- oder Datei-Sicherung wieder einzuspielen, klickt man in der jeweiligen Zeile auf `importieren`.

> **Wichtig:** Bis zum Abschluss des Imports dürfen keine weiteren Aktionen in REDAXO ausgeführt werden!

Nach erfolgreichem Import werden alle Artikel sowie der Cache neu generiert. Alte Daten werden vom Server gelöscht.

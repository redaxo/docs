# Cronjobs

Cronjobs dienen der regelmäßigen automatisierten Ausführung von Programmcode. Das Cronjobs AddOn ist Bestandteil der Redaxo Basisinstallation, muss jedoch bei Bedarf separat installiert werden.

Im AddOn lassen sich dann beliebig viele Einträge erstellen, die gemäß den Einstellungen jedes Eintrages abgearbeitet werden.

## Die Einstellungen eines Cronjobs

### Name

Zunächst gibt man den Namen eines Eintrags ein. Dies kann beispielsweise "RSS Feed lesen" oder "Monatliches Backup" sein.

### Beschreibung

Eine aussagekräftige Beschreibung vervollständigt den informativen Teil des Eintrages.

### Umgebung

Im Feld [Umgebung] kann man ein oder mehrere Ereignisse wählen, bei denen der Cronjob ausgeführt wird.

- Frontend
- Backend
- Skript

Sobald ein eingestelltes Intervall erreicht ist, wartet das AddOn auf das eingestellte Ereignis: einen Seitenaufruf im Frontend, auf eine Aktion durch einen Nutzer im Backend oder den Aufruf der Skriptumgebung. Tritt das eingestellte Ereignis ein, wird der Cronjob ausgeführt. Obwohl alle drei Einträge gleichzeitig aktiviert werden können, macht es keinen Sinn den Eintrag "Skript" gleichzeitig mit "Frontend" oder "Backend" auszuwählen - von Testzwecken einmal abgesehen.

Somit können Cronjobs ausgelöst werden durch:

- einen Seitenaufruf im Frontend
- einen Seitenaufruf im Backend
- einen direkten Aufruf der Cronjob Scriptumgebung durch einen externen Dienst

Bei der Ausführung in der Umgebung "Frontend" und "Backend" läuft der Cronjob in der Session des jeweiligen Users, sodass dort auch ein Zugriff auf die Session möglich ist. Nur die Einstellung "Skript" erlaubt die Ausführung des Cronjobs unabhängig von einem Aufruf von Redaxo im Frontend oder im Backend.

Nur mit der Einstellung "Backend" ist es möglich den Cronjob manuell in den Einstellungen des AddOns zu starten.

### Ausführung

Wenn eines der Ereignisse "Frontend" oder "Backend" eintritt, so kann der Cronjob seinen Dienst zu Beginn des Aufrufes erledigen oder am Ende. Nur in Ausnahmefällen sollte die Einstellung "Beginn" gewählt werden, da sie den jeweiligen Aufruf verzögert. Das fällt natürlich weniger ins Gewicht, wenn die Ausführung am Ende geschieht.

### Status

Im Feld "Status" kann ein Cronjob deaktiviert werden. Standard ist "aktiviert".

### Typ

Im Feld "Typ" stehen die Auswahlmöglichkeiten

- PHP-Code
- PHP-Callback
- URL-Aufruf

zur Verfügung. AddOns können dort weitere Einträge hinzufügen.

Beispielsweise:

- Datenbankexport (durch das AddOn "Backup")
- Search it: Reindexieren (durch das AddOn "Search it")

Je nach Einstellung im Feld "Typ" stehen unterschiedliche Eingabemöglichkeiten im Bereich "Typspezifische Parameter" zur Verfügung.
So kann bei der Einstellung "PHP-Code" kompletter PHP-Code eingegeben werden, bei der Einstellung "PHP-Callback" lediglich ein Aufruf.

AddOns können eigene typspezifische Parameter zur Verfügung stellen.

### Intervall

Die Standardeinstellung für den Bereich "Intervall" ist die tägliche Ausführung, jeweils beim nächsten Aufruf der Umgebung nach 0:00 Uhr.

## Neue Typen durch AddOns definieren

AddOns können eigene Ausführungstypen definieren. Dies wird beispielsweise im System AddOn "Backup" verwendet, um automatisierte Backups auszuführen.
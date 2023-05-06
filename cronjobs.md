# Cronjobs

- [Zweck des Cronjob-AddOns](#zweck)
- [Einstellungen eines Cronjobs](#einstellungen)
  - [Name](#name)
  - [Beschreibung](#beschreibung)
  - [Umgebung](#umgebung)
  - [Ausführung](#ausfuehrung)
  - [Status](#status)
  - [Typ](#typ)
  - [Intervall](#intervall)
- [Neue Typen durch AddOns definieren](#neue-typen)

<a name="zweck"></a>

## Zweck des Cronjob-AddOns

Cronjobs dienen der regelmäßigen automatisierten Ausführung von Programmcode. Das Cronjobs-AddOn ist Bestandteil der REDAXO-Basisinstallation, muss jedoch bei Bedarf separat installiert werden.

Im AddOn lassen sich dann beliebig viele Einträge erstellen, die gemäß den Einstellungen jedes Eintrages abgearbeitet werden.

<a name="einstellungen"></a>

## Einstellungen eines Cronjobs

<a name="name"></a>

### Name

Zunächst gibt man den Namen eines Eintrags ein. Dies kann beispielsweise `RSS Feed lesen` oder `Monatliches Backup` sein.

<a name="beschreibung"></a>

### Beschreibung

Eine aussagekräftige Beschreibung vervollständigt den informativen Teil des Eintrages.

<a name="umgebung"></a>

### Umgebung

Im Feld `Umgebung` kann man ein oder mehrere Ereignisse wählen, bei denen der Cronjob ausgeführt wird.

- Frontend
- Backend
- Skript

Sobald ein eingestelltes Intervall erreicht ist, wartet das AddOn auf das eingestellte Ereignis: einen Seitenaufruf im Frontend, auf eine Aktion durch einen Nutzer im Backend oder den Aufruf der Skriptumgebung. Tritt das eingestellte Ereignis ein, wird der Cronjob ausgeführt.

Obwohl alle drei Einträge gleichzeitig aktiviert werden können, sollte man die Umgebung `Skript` nicht gleichzeitig mit `Frontend` oder `Backend` auswählen - von Testzwecken einmal abgesehen.

Somit können Cronjobs ausgelöst werden durch:

- Einen Seitenaufruf im Frontend
- Einen Seitenaufruf im Backend
- Einen direkten Aufruf der Cronjob-Skriptumgebung durch den Server

Bei der Ausführung in der Umgebung `Frontend` und `Backend` läuft der Cronjob in der Session des jeweiligen Users, sodass dort auch ein Zugriff auf die Session möglich ist. Nur die Umgebung `Skript` erlaubt die Ausführung des Cronjobs unabhängig von einem Aufruf von REDAXO im Frontend oder im Backend. Der Aufruf des Skripts erfolgt durch `.../redaxo/bin/console cronjob:run`, also z.B. `/home/users/12345/www/redaxo/bin/console cronjob:run`

Nur in der Umgebung `Backend` ist es möglich, den Cronjob manuell in den Einstellungen des AddOns zu starten.


#### Empfehlungen 

Die empfohlene Umgebung ist `Skript`, hierbei wird der Cronjob über einen serverseitigen Cronjob aufgerufen. 

Sollte die Ausführung als Cronjob nicht möglich sein (z.B.: aufgrund mangelnder Rechte auf dem Server), stehen die alternativen Umgebungen `Frontend` und `Backend` zur Verfügung. 

Bei `Script` findet die Ausführung über den Cronjob des Betriebssystems statt (z.B. `crontab -e`) und ist unabhängig von den Seitenaufrufen in REDAXO. Zum Aufruf muss `redaxo/bin/console cronjob:run` aufgerufen werden. Das Intervall zwischen den Server-Cronjobs muss kleiner oder gleich sein, als das kleinste Intervall im REDAXO-Cronjob.

`Frontend` und `Backend` werden ausgeführt, wenn im Frontend und / oder Backend Seitenaufrufe erfolgen. Dies hat u.U. zur Folge, dass die Cronjobs ggf. später ausgeführt werden, als erwünscht. (z.B. bei regelmäßigen Backups, E-Mail-Benachrichtigungen)  


<a name="ausfuehrung"></a>

### Ausführung

Wenn eines der Ereignisse `Frontend` oder `Backend` eintritt, so kann der Cronjob seinen Dienst zu Beginn des Aufrufs erledigen oder am Ende. Nur in Ausnahmefällen sollte die Einstellung `Beginn` gewählt werden, da sie den jeweiligen Aufruf verzögert. Das fällt natürlich weniger ins Gewicht, wenn die Ausführung am Ende geschieht.

<a name="status"></a>

### Status

Im Feld `Status` kann ein Cronjob deaktiviert werden. Standard ist `aktiviert`.

<a name="typ"></a>

### Typ

Im Feld `Typ` bestehen die Auswahlmöglichkeiten:

- PHP-Code
- PHP-Callback
- URL-Aufruf

AddOns können dort weitere Einträge hinzufügen.

Beispielsweise:

- Datenbankexport (durch das AddOn `Backup`)
- Search it: Reindexieren (durch das AddOn `Search it`)

Je nach Einstellung im Feld `Typ` stehen unterschiedliche Eingabemöglichkeiten im Bereich `Typspezifische Parameter` zur Verfügung.
So kann bei der Einstellung `PHP-Code` kompletter PHP-Code eingegeben werden, bei der Einstellung `PHP-Callback` lediglich ein Aufruf.

AddOns können eigene, typspezifische Parameter zur Verfügung stellen.

<a name="intervall"></a>

### Intervall

Die Standardeinstellung für den Bereich `Intervall` ist die tägliche Ausführung, jeweils beim nächsten Aufruf der Umgebung nach 0:00 Uhr.

<a name="neue-typen"></a>

## Neue Typen durch AddOns definieren

AddOns können eigene Ausführungstypen definieren. Dies wird beispielsweise im System AddOn `Backup` verwendet, um automatisierte Backups auszuführen.

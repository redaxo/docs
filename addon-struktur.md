# AddOn: Aufbau und Struktur 


| Ordner | Datei | Beschreibung |
| --- | --- | --- |
|  | **package.yml** | Definiert das Addon, grundlegende Einstellungen - Diese Detei ist **unbedingt erforderlich**.  |
|  | boot.php | Die boot.php wird bei jeder Aktion in Redaxo ausgeführt. Hier können beliebige Befehle ausgeführt werden.  |
|  | install.php | Wird automatisch bei der Installation ausgeführt. (z.B. Anlage von Datenbanken, Installation von Modulen, bestimmte Prüfungen, Festlegen erster Konfigurationswerte. |
|  | uninstall.php | Gegenstück zu install.php. Hier können zusätzliche Deinstallationsschritte eingefügt werden.  |
|  | install.sql | SQL-Datei, die bei Installation ausgeführt werden soll |
|  | uninstall.sql | SQL-Datei, die bei Deinstallation ausgeführt werden soll |
| assets | *.css, *.js | Hier werden die Assets des AddOns abgelegt. Bei Installation werden diese in den Ordner **/assets/addon/addon_name/** kopiert. Sie stehen somit öffentlich zur Verfügung. Es sind Unterordner möglich.  |
| data |  | Hier kann das AddOn zusätzliche Daten ablegen. Diese werden im Ordner  /redaxo/data/addons/addon_name abgelegt |
| fragments |  | Ordner für Fragmente  |
| lang | *.lang | Hier werden die Sprachdateien abgelegt |
| lib |  | Autolord-Ordner, alle hier gefundenen PHP-Classes und Functions werden automatisch eingebunden. |
| pages |  | Ordner für die Backendseiten des AddOns (z.B. Hilfe, Setup)  |
| plugins |  | Hier findet man die mitgelieferten PlugIns |
| vendor |  | Vendor-Ordner, hier werden fertige Classes, Skripte, Applikationen von „Lieferanten“-Quellen abgelegt. Wie beim Lib-Ordner werden deren Classes automatisch geladen. Beispiel: PHPMailer |



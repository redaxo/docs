# AddOn: Aufbau und Struktur 

Ein AddOn kann aus mehreren Verzeichnissen und Dateien bestehen, nachfolgend gelistet zeigen wir hier die gebräuchlichsten. Das AddOn besteht aus einer verpflichtenden Konfigurationsdatei package.yml und den nachfolgenden optionalen Ordnern und Dateien. **Richtig gelesen:** Nur die package.yml ist erforderlich. Ein solches AddOn hätte sicher einen sehr geringen Nutzen. daher gibt es mehrere Dateien, die den Aufbau eines AddOns vereinfachen. Der AddOn-Entwickler ist aber frei auch weitere Ordner z.B. für Module und Templates oder anderes zu erstellen. Dann verzichtet der AddOn-Entwickler jedoch auf sehr hilfreiche Automatismen und muss sich selbst um die Einbindung z.B. von PHP-Classes kümmern. 


| Ordner | Datei | Beschreibung |
| --- | --- | --- |
|  | **package.yml** | Definiert das Addon, grundlegende Einstellungen - Diese Detei ist **unbedingt erforderlich**.  |
|  | boot.php | Die boot.php wird bei jeder Aktion in Redaxo ausgeführt. Hier können beliebige Befehle ausgeführt werden.  |
|  | help.php | Wird als Hilfeseite zum AddOn eingebunden |
|  | install.php | Wird automatisch bei der Installation ausgeführt. (z.B. Anlage von Datenbanken, Installation von Modulen, bestimmte Prüfungen, Festlegen erster Konfigurationswerte. |
|  | uninstall.php | Gegenstück zu install.php. Hier können zusätzliche Deinstallationsschritte eingefügt werden.  |
|  | install.sql | SQL-Datei, die bei Installation ausgeführt werden soll |
|  | uninstall.sql | SQL-Datei, die bei Deinstallation ausgeführt werden soll |
|  | README.md | Sofern gefunden und eine help.php liegt nicht vor, wird diese automatisch als Hilfeseite eingebunden |
| assets | *.css, *.js, *.png etc. | Hier werden die Assets des AddOns abgelegt. Bei Installation werden diese in den Ordner **/assets/addon/addon_name/** kopiert. Sie stehen somit öffentlich zur Verfügung. Es sind Unterordner möglich.  |
| data |  | Hier kann das AddOn zusätzliche Daten ablegen. Diese werden im Ordner  /redaxo/data/addons/addon_name abgelegt |
| fragments |  | Ordner für Fragmente  |
| lang | *.lang | Hier werden die Sprachdateien abgelegt |
| lib |  | Autolord-Ordner, alle hier gefundenen PHP-Classes und Functions werden automatisch eingebunden. |
| pages |  | Ordner für die Backendseiten des AddOns (z.B. Hilfe, Setup)  |
|  | index.php | Wird automatisch beim Aufruf des Menüpunktes aufgerufen und bindet ggf. zusätzliche seiten ein.  |
| plugins |  | Hier findet man die mitgelieferten PlugIns |
| vendor |  | Vendor-Ordner, hier werden fertige Classes, Skripte, Applikationen von „Lieferanten“-Quellen abgelegt. Wie beim Lib-Ordner werden deren Classes automatisch geladen. Beispiel: PHPMailer |


# AddOn: Aufbau und Struktur

Ein AddOn kann aus mehreren Verzeichnissen und Dateien bestehen, nachfolgend werden nur die gebräuchlichsten aufgelistet. Das AddOn besteht aus einer verpflichtenden Konfigurationsdatei package.yml und den nachfolgenden optionalen Ordnern und Dateien.
**Richtig gelesen:** Nur die [**package.yml**](/{{path}}/{{version}}/addon-package) ist erforderlich. Ein solch leeres AddOn hätte sicher einen sehr geringen Nutzen, daher gibt es mehrere Dateien und Ordner, die den Aufbau und die Ausführung eines AddOns vereinfachen.

Den Entwickelnden steht es frei, weitere Ordner z. B. Module und Templates oder anderes zu erstellen. Hier verzichtet man jedoch auf hilfreiche Automatismen (z. B. Autoload, automatisches Kopieren) und muss sich selbst um die korrekte Einbindung, z. B. von PHP-Classes und Assets kümmern.

## Ordner- und Datei-Struktur

Der AddOn-Ordner (wie auch das AddOn selbst) muss einen **eindeutigen, unverwechselbaren** Namen haben, den AddOnkey. Damit es nicht zu Konflikten mit anderen AddOns mit gleicher Bezeichnung kommt, sollte der Key in [MyREDAXO](https://redaxo.org/myredaxo/login/) registriert sein. Er wird in der [ `package.yml` ](/{{path}}/{{version}}/addon-package) hinterlegt.

Abhängig vom Projekt werden in AddOns folgende Ordner und Dateien verwendet:

| Ordner | Datei | Beschreibung |
| --- | --- | --- |
|  | [**package.yml**](/{{path}}/{{version}}/addon-package)| Definiert das AddOn, grundlegende Einstellungen - Diese Datei ist **unbedingt erforderlich**  |
|  | boot.php | Die boot.php wird bei jeder Aktion in REDAXO ausgeführt. Hier können beliebige Befehle ausgeführt werden |
|  | help.php | Alternative zur Readme. Wird automatisch als Hilfeseite zum AddOn eingebunden, kann Programmcode enthalten.|
|  | install.php | Wird automatisch bei der Installation ausgeführt. (z. B. Anlegen von Datenbanken, Installation von Modulen, bestimmte Prüfungen, Festlegen erster Konfigurationswerte |
|  | uninstall.php | Gegenstück zu install.php. Hier können zusätzliche Deinstallationsschritte eingefügt werden.  |
|  | install.sql | SQL-Datei, die bei der Installation ausgeführt wird |
|  | uninstall.sql | SQL-Datei, die bei der Deinstallation ausgeführt wird |
|  | update.php | Die update.php wird ausgeführt, wenn eine Aktualisierung über den Installer erfolgt. Die update.php wird nicht bei einem manuellen Update ausgeführt. |
|  | README.md | Sofern gefunden und eine help.php nicht vorliegt, wird diese Datei automatisch als Hilfeseite eingebunden. Die README kann mehrsprachig hinterlegt werden. README.en.md würde dann in einem englischsprachigen Backend aufgerufen werden. Ist die README semantisch korrekt aufgebaut, wird automatisch ein Inhaltsverzeichnis generiert.|
| assets | *.css, *.js, *.png etc. | Hier werden die Assets des AddOns abgelegt. Bei Installation werden diese in den Ordner **/assets/addon/addon_name/** kopiert. Sie stehen somit öffentlich zur Verfügung. Es sind Unterordner möglich |
| data |  | Hier kann das AddOn zusätzliche Daten ablegen. Diese werden im Ordner   `/redaxo/data/addons/addon_name` abgelegt |
| fragments |  | Ordner für [Fragmente](/{{path}}/{{version}}/fragmente)  |
| lang | *.lang | Hier werden die Sprachdateien abgelegt |
| lib |  | Ordner für eigene Classes und Funktionen, selbst entwickelte Dateien |
| pages |  | Ordner für die Backendseiten des AddOns (z. B. Hilfe, Setup)  |
|  | index.php | Wird automatisch beim Aufruf des Menüpunktes aufgerufen und bindet ggf. zusätzliche Seiten ein.  |
| plugins |  | Hier findet man die mitgelieferten PlugIns |
| vendor |  | Vendor-Ordner – hier werden fertige Classes, Skripte, Applikationen von „Lieferanten“-Quellen/Vendors abgelegt.|
| ignore_installer |  | Zun Ausschluss von Ordnern und Dateien bei der Erstellung des Installationspaketes |

> **Autoload** lib und vendor werden rekursiv nach PHP-Klassen durchsucht. Die gefundenen Klassen werden automatisch eingebunden.
> Zusätzlich zu den hier genannten Dateien empfiehlt sich, gerade bei Veröffentlichung des Codes in öffentlichen Portalen oder Repositories, ein CHANGELOG.md und eine Lizenz-Datei LICENSE / oder LICENSE.md beizulegen.

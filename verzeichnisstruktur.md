# Verzeichnisstruktur

- [Orderstruktur des CMS](#ordnerstruktur)
- [Liste der wichtigsten Pfade samt ihrer Pfad-Variablen](#liste-der-pfade)

<a name="hinweise"></a>
## Orderstruktur des CMS

In vielen Fällen ist es hilfreich, die Verzeichnisstruktur von REDAXO selbst zu kennen: Wo liegen die Core-Dateien, wo die Klassen und Funktionen, die AddOns und PlugIns, wo die Cache-Dateien und die öffentlich erreichbaren Dateien wie die Assets (CSS, JS) von AddOns oder die durch den Redakteur hochgeladenen Dateien? 

Einige der Verzeichnisse sind durch htaccess-Dateien vor dem öffentlichen Zugriff geschützt, andere müssen frei erreichbar sein.

> **Hinweis:** Die folgende Tabelle gibt einen groben Überblick; sie ist bewusst nicht vollständig und listet nur die wichtigsten Verzeichnisse aus.

| Pfad | Beschreibung |
| ------------- | ------------- |
| `/redaxo/data/` | der Basisordner für die von einer Website individuell generierten Dateien, z.B. die Konfigurationsdatei config.yml im core-Unterordner |
| `/redaxo/cache/` | Speicherort für alle Cache-Dateien |
| `/redaxo/src/` | Der Hauptordner (Source) für den Core |
| `/redaxo/src/addons/` | Alle AddOns von Redaxo |
| `/redaxo/src/core/assets/` | Assets für das Backend, im wesentlichen Javascripts |
| `/redaxo/src/core/fragments/` | Die Fragmente enthalten PHP- und HTML-Code und dienen als kleine "Bausteine" dazu, das Backend einheitlich zu gestalten. Sie können auch für die eigene Programmierung verwendet und erweitert werden |
| `/redaxo/src/core/functions/` | Die wesentlichen PHP-Funktionen |
| `/redaxo/src/core/lang/` | Die Sprachdateien für das Backend |
| `/redaxo/src/core/layout/` | Die zwei Dateien in diesem Ordner generieren den Footer, bzw. Header des Backends |
| `/redaxo/src/core/lib/` | Der Kernbereich von REDAXO |
| `/redaxo/src/core/pages/` | Einige zentrale Seiten des Backends, wie z.B. Login, Profil, Setup, etc. |
| `/redaxo/src/core/tests/` | Automatisierte Tests für Core-Klassen und -Funktionen |
| `/redaxo/src/core/vendor/` | Funktionen von externen Bibliotheken, z.B: Composer, Symphony, etc. |

<a name="hinweise"></a>
## Liste der wichtigsten Pfade samt ihrer Pfad-Variablen

Da man bei der eigenen Programmierung – sei es bei eigenen AddOns oder auch bei Modulen und Templates – des öfteren auf solche Pfade zugreifen muss, gibt es Variablen, die man dafür nutzen kann. Die folgende Tabelle listet die wesentlichen Variablen auf.

> **Hinweis:** Die Liste ist bewusst nicht vollständig und enthält nur die wichtigsten Verzeichnisse.

| Pfad | Beschreibung | Pfad-Variable |
| ------------- | ------------- | ------------- |
| `/` | | `rex_path::frontend($file, $pathType)` |
| `/index.php` | Einstiegspunkt zum Frontend | `rex_path::frontendController($params)` |
| `/media/`  | In den Medienpool geladene Dateien | `rex_path::media($file, $pathType)` |
| `/assets/` | öffentliche Hilfsdateien | `rex_path::assets($file, $pathType)` |
| `/assets/addons/addonname/` | öffentliches Hilfsdateien eine AddOns | `rex_path::addonAssets($addon, $file, $pathType)` |
| `/assets/addons/addonname/plugins/pluginname/` | öffentliches Hilfsdateien eine AddOns | `rex_path::pluginAssets($addon, $plugin, $file, $pathType)` |
| `/redaxo/` | gesicherter Ordner, kein Zugriff auf die Website von außen außer zu r index.php | `rex_path::backend($file, $pathType)` |
| `/redaxo/index.php` | Einstiegspunkt zum Backend | `rex_path::backendController($params)` |
| `/redaxo/cache/` | Cache-Dateien | `rex_path::cache($file)` |
| `/redaxo/data/` | private Hilfsdateien | `rex_path::data($file)` |
| `/redaxo/data/addons/addonname/` | Private Hilfs- und Backup-Dateien eines AddOns | `rex_path::addonData($addon, $file)` |
| `/redaxo/data/addons/addonname/plugins/pluginname` | Private Hilfs- und Backup-Dateien eines Plugins | `rex_path::pluginData($addon, $plugin, $file)` |
| `/redaxo/src/` | | `rex_path::src($file)` |
| `/redaxo/src/core/` | libs, pages of  | `rex_path::core($file)` |
| `/redaxo/src/addons/addonname/` | | `rex_path::addon($addon, $file)` |
| `/redaxo/src/addons/addonname/pages/` | Seite eines AddOns | `rex_path::addon($addon, $file).'pages/'` |
| `/redaxo/src/addons/addonname/lib/` | Klassen und Bibliotheken eines AddOns, mit Autoload-Funktion | `rex_path::addon($addon, $file).'lib/'` |
| `/redaxo/src/addons/addonname/vendor/` | Klassen und Bibliotheken eines AddOns, die kein Autoload benötigen, oftmals auch Third-Party-Dateien | `rex_path::addon($addon, $file).'vendor/'` |
| `/redaxo/src/addons/addonname/assets/` | öffentliche Hilfsdateien, sie werden bei der Installation des AddOns in den öffentlichen Ordner kopiert | `rex_path::addon($addon, $file).'assets/'` |
| `/redaxo/src/addons/addonname/tests/` | Automatisierte Tests für AddOn-Klassen und -Funktionen | `rex_path::addon($addon, $file).'tests/'` |
| `/redaxo/src/addons/addonname/(un)install.(sql/php)` | Datei zur Installation, bzw. Deinstallation des AddOns | z.B. `rex_path::addon($addon, $file).'install.php'` |
| `/redaxo/src/addons/addonname/config.inc.php` | Konfigurations-Datei des AddOns | `rex_path::addon($addon, $file).'config.inc.php'` |
| `/redaxo/src/addons/addonname/package.yml` | AddOn-Definitionen wie Version, Author, einzelne Seiten | `rex_path::addon($addon, $file).'package.yml'` |
| `/redaxo/src/addons/addonname/plugins/pluginname` | | `rex_path::plugin($addon, $plugin, $file)` |

`$file`, `$params` and `$pathType` sind optionale Parameter. 
Mögliche Pfad-Typen sind `rex_path::ABSOLUTE` (default) und `rex_path::RELATIVE`.


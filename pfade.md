# Pfade
- [Dateisystem - rex_path](#rex_path)
    - [base](#base)
    - [frontend](#frontend)
    - [frontendController](#frontendController)
    - [backend](#backend)
    - [backendController](#backendController)
    - [media](#media)
    - [assets](#assets)
    - [coreAssets](#coreAssets)
    - [addonAssets](#addonAssets)
    - [pluginAssets](#pluginAssets)
    - [data](#data)
    - [coreData](#coreData)
    - [addonData](#addonData)
    - [pluginData](#pluginData)
    - [cache](#cache)
    - [coreCache](#coreCache)
    - [addonCache](#addonCache)
    - [pluginCache](#pluginCache)
    - [src](#src)
    - [core](#core)
    - [addon](#addon)
    - [plugin](#plugin)
    - [absolute](#absolute)


Zugriff auf das Dateisystem

Die Klassen `rex_path` und `rex_url` ermöglichen den Zugriff auf die entsprechenden Ressourcen im Dateisystem (´rex_path´) bzw. per URL (`rex_url`).

<a name="rex_path"></a>
## Dateisystem - rex_path

> **Hinweis:** Es wird nicht geprüft, ob die zurückgegebenen Pfade gültig sind oder existieren.

<a name="base"></a>
### base

Gibt den Base Pfad der übergebenen Datei zurück.

Beispiel:
`rex_path::base('media/meinbild.jpg')` => '/htdocs/meinverzeichnis/media/meinbild.jpg'



<a name="frontend"></a>
### frontend

Gibt den Frontend Pfad der übergebenen Datei zurück.

Beispiel:
`rex_path::base('media/meinbild.jpg')` => '/htdocs/meinverzeichnis/media/meinbild.jpg'



<a name="frontendController"></a>
### frontendController

Pfad zum Frontend Controller.

Beispiel:
`rex_path::frontendController()` => '/htdocs/meinverzeichnis/index.php'



<a name="backend"></a>
### backend

Pfad zum Backend.

Beispiel:
`rex_path::backend()` => '/htdocs/meinverzeichnis/redaxo/'
`rex_path::backend('meinedatei.php')` => '/htdocs/meinverzeichnis/redaxo/meinedatei.php'



<a name="backendController"></a>
### backendController

Pfad zum Backend Controller.

Beispiel:
`rex_path::backendController()` => '/htdocs/meinverzeichnis/redaxo/index.php'



<a name="media"></a>
### media

Pfad zum Media Verzeichnis.

Beispiel:
`rex_path::media()` => '/htdocs/meinverzeichnis/media/'



<a name="assets"></a>
### assets

Pfad zum Assets Verzeichnis.

Beispiel:
`rex_path::assets()` => '/htdocs/meinverzeichnis/assets/'



<a name="coreAssets"></a>
### coreAssets

Pfad zum Assets Verzeichnis des Core.

Beispiel:
`rex_path::coreAssets()` => '/htdocs/meinverzeichnis/assets/core/'
`rex_path::coreAssets('file.txt')` => '/htdocs/meinverzeichnis/assets/core/file.txt'



<a name="addonAssets"></a>
### addonAssets

Pfad zum Assets Verzeichnis eines AddOns.

Beispiel:
`rex_path::addonAssets('meinaddon')` => '/htdocs/meinverzeichnis/assets/addons/meinaddon/'
`rex_path::addonAssets('meinaddon','file.txt')` => '/htdocs/meinverzeichnis/assets/addons/meinaddon/file.txt'



<a name="pluginAssets"></a>
### pluginAssets

Pfad zum Assets Verzeichnis eines Plugins.

Beispiel:
`rex_path::pluginAssets('meinaddon','meinplugin')` => '/htdocs/meinverzeichnis/assets/addons/meinaddon/plugins/meinplugin/'
`rex_path::pluginAssets('meinaddon','meinplugin','file.txt')` => '/htdocs/meinverzeichnis/assets/addons/meinaddon/plugins/meinplugin/file.txt'



<a name="data"></a>
### data

Pfad zum Data Verzeichnis.

Beispiel:
`rex_path::data()` => '/htdocs/meinverzeichnis/data/'



<a name="coreData"></a>
### coreData

Pfad zum Data Verzeichnis des Core.

Beispiel:
`rex_path::coreData()` => '/htdocs/meinverzeichnis/data/core/'
`rex_path::coreData('file.txt')` => '/htdocs/meinverzeichnis/data/core/file.txt'



<a name="addonData"></a>
### addonData

Pfad zum Data Verzeichnis eines AddOns.

Beispiel:
`rex_path::addonData('meinaddon')` => '/htdocs/meinverzeichnis/data/addons/meinaddon/'
`rex_path::addonData('meinaddon','file.txt')` => '/htdocs/meinverzeichnis/data/addons/meinaddon/file.txt'



<a name="pluginData"></a>
### pluginData

Pfad zum Data Verzeichnis eines Plugins.

Beispiel:
`rex_path::pluginData('meinaddon','meinplugin')` => '/htdocs/meinverzeichnis/data/addons/meinaddon/plugins/meinplugin/'
`rex_path::pluginData('meinaddon','meinplugin','file.txt')` => '/htdocs/meinverzeichnis/data/addons/meinaddon/plugins/meinplugin/file.txt'



<a name="cache"></a>
### cache

Pfad zum Cache Verzeichnis.

Beispiel:
`rex_path::cache()` => '/htdocs/meinverzeichnis/redaxo/cache/'
`rex_path::cache('file.txt')` => '/htdocs/meinverzeichnis/redaxo/cache/file.txt'



<a name="coreCache"></a>
### coreCache

Pfad zum Data Verzeichnis.

Beispiel:
`rex_path::coreCache()` => '/htdocs/meinverzeichnis/redaxo/cache/core/'
`rex_path::coreCache('file.txt')` => '/htdocs/meinverzeichnis/redaxo/cache/core/file.txt'



<a name="addonCache"></a>
### addonCache

Pfad zum Cache Verzeichnis eines AddOns.

Beispiel:
`rex_path::addonCache('meinaddon')` => '/htdocs/meinverzeichnis/redaxo/cache/addons/meinaddon/'
`rex_path::addonCache('meinaddon','file.txt')` => '/htdocs/meinverzeichnis/redaxo/cache/addons/meinaddon/file.txt'



<a name="pluginCache"></a>
### pluginCache

Pfad zum Cache Verzeichnis eines Plugins.

Beispiel:
`rex_path::pluginCache('meinaddon','meinplugin')` => '/htdocs/meinverzeichnis/redaxo/cache/addons/meinaddon/plugins/meinplugin/'
`rex_path::pluginCache('meinaddon','meinplugin','file.txt')` => '/htdocs/meinverzeichnis/redaxo/cache/addons/meinaddon/plugins/meinplugin/file.txt'



<a name="src"></a>
### src

Pfad zum src Verzeichnis.

Beispiel:
`rex_path::src()` => '/htdocs/meinverzeichnis/redaxo/src/'
`rex_path::src('file.txt')` => '/htdocs/meinverzeichnis/redaxo/src/file.txt'



<a name="core"></a>
### core

Pfad zum core Verzeichnis.

Beispiel:
`rex_path::core()` => '/htdocs/meinverzeichnis/redaxo/src/core/'
`rex_path::core('file.txt')` => '/htdocs/meinverzeichnis/redaxo/src/core/file.txt'



<a name="addon"></a>
### addon

Pfad zum addon Verzeichnis.

Beispiel:
`rex_path::addon('meinaddon')` => '/htdocs/meinverzeichnis/redaxo/src/addons/meinaddon/'
`rex_path::addon('meinaddon','file.txt')` => '/htdocs/meinverzeichnis/redaxo/src/addons/meinaddon/file.txt'



<a name="plugin"></a>
### plugin

Pfad zum plugin Verzeichnis.

Beispiel:
`rex_path::plugin('meinaddon','meinplugin')` => '/htdocs/meinverzeichnis/redaxo/src/addons/meinaddon/plugins/meinplugin/'
`rex_path::plugin('meinaddon','meinplugin','file.txt')` => '/htdocs/meinverzeichnis/redaxo/src/addons/meinaddon/plugins/meinplugin/file.txt'



<a name="absolute"></a>
### absolute

Wandelt einen relativen Pfad zu einem absoluten Pfad.

Beispiel:
`rex_path::absolute('../../src/addons')` => 'src/addons'




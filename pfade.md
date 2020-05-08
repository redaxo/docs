# Pfade

- [Zugriff auf Dateisystem](#zugriff)
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
  - [log](#log)
  - [src](#src)
  - [core](#core)
  - [addon](#addon)
  - [plugin](#plugin)
  - [absolute](#absolute)
- [URLs - rex_url](#rex_url)
  - [init](#urlinit)
  - [base](#urlbase)
  - [frontend](#urlfrontend)
  - [frontendController](#urlfrontendController)
  - [backend](#urlbackend)
  - [backendController](#urlbackendController)
  - [backendPage](#urlbackendPage)
  - [currentBackendPage](#urlcurrentBackendPage)
  - [media](#urlmedia)
  - [assets](#urlassets)
  - [coreAssets](#urlcoreAssets)
  - [addonAssets](#urladdonAssets)
  - [pluginAssets](#urlpluginAssets)

<a name="zugriff"></a>

## Zugriff auf das Dateisystem

Die Klassen `rex_path` und `rex_url` ermöglichen den Zugriff auf die entsprechenden Ressourcen im Dateisystem (`rex_path`) bzw. per URL (`rex_url`).

<a name="rex_path"></a>

## Dateisystem - rex_path

> **Hinweis:** Es wird nicht geprüft, ob die zurückgegebenen Pfade gültig sind oder existieren.

<a name="base"></a>

### base

Gibt den Base Pfad mit der übergebenen Datei oder dem Ordner zurück

Beispiele:

`rex_path::base()` => '/htdocs/meinverzeichnis/'

`rex_path::base('index.php')` => '/htdocs/meinverzeichnis/index.php'

<a name="frontend"></a>

### frontend

Gibt den Frontend-Pfad mit der übergebenen Datei oder dem Ordner zurück

Beispiele:

`rex_path::frontend()` => '/htdocs/meinverzeichnis/'

`rex_path::frontend('index.php')` => '/htdocs/meinverzeichnis/index.php'

<a name="frontendController"></a>

### frontendController

Pfad zum Frontend-Controller

Beispiel:
`rex_path::frontendController()` => '/htdocs/meinverzeichnis/index.php'

<a name="backend"></a>

### backend

Pfad zum Backend

Beispiel:
`rex_path::backend()` => '/htdocs/meinverzeichnis/redaxo/'

`rex_path::backend('meinedatei.php')` => '/htdocs/meinverzeichnis/redaxo/meinedatei.php'

<a name="backendController"></a>

### backendController

Pfad zum Backend-Controller

Beispiel:
`rex_path::backendController()` => '/htdocs/meinverzeichnis/redaxo/index.php'

<a name="media"></a>

### media

Pfad zum Media-Verzeichnis

Beispiel:
`rex_path::media()` => '/htdocs/meinverzeichnis/media/'

<a name="assets"></a>

### assets

Pfad zum Assets-Verzeichnis

Beispiel:
`rex_path::assets()` => '/htdocs/meinverzeichnis/assets/'

<a name="coreAssets"></a>

### coreAssets

Pfad zum Assets-Verzeichnis des Core

Beispiel:
`rex_path::coreAssets()` => '/htdocs/meinverzeichnis/assets/core/'
`rex_path::coreAssets('file.txt')` => '/htdocs/meinverzeichnis/assets/core/file.txt'

<a name="addonAssets"></a>

### addonAssets

Pfad zum Assets-Verzeichnis eines AddOns

Beispiel:
`rex_path::addonAssets('meinaddon')` => '/htdocs/meinverzeichnis/assets/addons/meinaddon/'
`rex_path::addonAssets('meinaddon','file.txt')` => '/htdocs/meinverzeichnis/assets/addons/meinaddon/file.txt'

<a name="pluginAssets"></a>

### pluginAssets

Pfad zum Assets-Verzeichnis eines Plugins

Beispiel:
`rex_path::pluginAssets('meinaddon','meinplugin')` => '/htdocs/meinverzeichnis/assets/addons/meinaddon/plugins/meinplugin/'
`rex_path::pluginAssets('meinaddon','meinplugin','file.txt')` => '/htdocs/meinverzeichnis/assets/addons/meinaddon/plugins/meinplugin/file.txt'

<a name="data"></a>

### data

Pfad zum Data-Verzeichnis

Beispiel:
`rex_path::data()` => '/htdocs/meinverzeichnis/data/'

<a name="coreData"></a>

### coreData

Pfad zum Data-Verzeichnis des Core

Beispiel:
`rex_path::coreData()` => '/htdocs/meinverzeichnis/data/core/'
`rex_path::coreData('file.txt')` => '/htdocs/meinverzeichnis/data/core/file.txt'

<a name="addonData"></a>

### addonData

Pfad zum Data-Verzeichnis eines AddOns

Beispiel:
`rex_path::addonData('meinaddon')` => '/htdocs/meinverzeichnis/data/addons/meinaddon/'
`rex_path::addonData('meinaddon','file.txt')` => '/htdocs/meinverzeichnis/data/addons/meinaddon/file.txt'

<a name="pluginData"></a>

### pluginData

Pfad zum Data-Verzeichnis eines Plugins

Beispiel:
`rex_path::pluginData('meinaddon','meinplugin')` => '/htdocs/meinverzeichnis/data/addons/meinaddon/plugins/meinplugin/'
`rex_path::pluginData('meinaddon','meinplugin','file.txt')` => '/htdocs/meinverzeichnis/data/addons/meinaddon/plugins/meinplugin/file.txt'

<a name="cache"></a>

### cache

Pfad zum Cache-Verzeichnis

Beispiel:
`rex_path::cache()` => '/htdocs/meinverzeichnis/redaxo/cache/'
`rex_path::cache('file.txt')` => '/htdocs/meinverzeichnis/redaxo/cache/file.txt'

<a name="coreCache"></a>

### coreCache

Pfad zum Data-Verzeichnis

Beispiel:
`rex_path::coreCache()` => '/htdocs/meinverzeichnis/redaxo/cache/core/'
`rex_path::coreCache('file.txt')` => '/htdocs/meinverzeichnis/redaxo/cache/core/file.txt'

<a name="addonCache"></a>

### addonCache

Pfad zum Cache-Verzeichnis eines AddOns

Beispiel:
`rex_path::addonCache('meinaddon')` => '/htdocs/meinverzeichnis/redaxo/cache/addons/meinaddon/'
`rex_path::addonCache('meinaddon','file.txt')` => '/htdocs/meinverzeichnis/redaxo/cache/addons/meinaddon/file.txt'

<a name="pluginCache"></a>

### pluginCache

Pfad zum Cache-Verzeichnis eines Plugins

Beispiel:
`rex_path::pluginCache('meinaddon','meinplugin')` => '/htdocs/meinverzeichnis/redaxo/cache/addons/meinaddon/plugins/meinplugin/'
`rex_path::pluginCache('meinaddon','meinplugin','file.txt')` => '/htdocs/meinverzeichnis/redaxo/cache/addons/meinaddon/plugins/meinplugin/file.txt'

<a name="log"></a>

### Log

Pfad zur angegebenen Log-Datei.

Beispiel:
`rex_path::log('mail.log')`  => `/httpdocs/redaxo/data/log/mail.log`

<a name="src"></a>

### src

Pfad zum Src-Verzeichnis

Beispiel:
`rex_path::src()` => '/htdocs/meinverzeichnis/redaxo/src/'
`rex_path::src('file.txt')` => '/htdocs/meinverzeichnis/redaxo/src/file.txt'

<a name="core"></a>

### core

Pfad zum Core-Verzeichnis

Beispiel:
`rex_path::core()` => '/htdocs/meinverzeichnis/redaxo/src/core/'
`rex_path::core('file.txt')` => '/htdocs/meinverzeichnis/redaxo/src/core/file.txt'

<a name="addon"></a>

### addon

Pfad zum AddOn-Verzeichnis

Beispiel:
`rex_path::addon('meinaddon')` => '/htdocs/meinverzeichnis/redaxo/src/addons/meinaddon/'
`rex_path::addon('meinaddon','file.txt')` => '/htdocs/meinverzeichnis/redaxo/src/addons/meinaddon/file.txt'

<a name="plugin"></a>

### plugin

Pfad zum PlugIn-Verzeichnis

Beispiel:
`rex_path::plugin('meinaddon','meinplugin')` => '/htdocs/meinverzeichnis/redaxo/src/addons/meinaddon/plugins/meinplugin/'
`rex_path::plugin('meinaddon','meinplugin','file.txt')` => '/htdocs/meinverzeichnis/redaxo/src/addons/meinaddon/plugins/meinplugin/file.txt'

<a name="absolute"></a>

### absolute

Wandelt einen relativen Pfad zu einem absoluten Pfad

Beispiel:
`rex_path::absolute('../../src/addons')` => 'src/addons'

<a name="rex_url"></a>

## URLs - rex_url

> **Hinweis:** Bei allen URL-Funktionen der Klasse `rex_url` wird eine Installation von Redaxo in einem Unterverzeichnis berücksichtigt.

Funktionen, die Parameter zu URLs umschreiben, können die URL auch "escaped" zurückgeben.

<a name="urlbase"></a>

### base

Liefert den Basispfad der Website

Beispiel:
`rex_url::base()` => '/'
`rex_url::base('file.txt')` => '/file.txt'

<a name="urlfrontend"></a>

### frontend

Liefert den Frontendpfad der Website

Beispiel:
`rex_url::frontend()` => '/'
Bei Installation in einem Unterverzeichnis:
`rex_url::frontend()` => '/verzeichnis/'
`rex_url::frontend('file.txt')` => '/verzeichnis/file.txt'

<a name="urlfrontendController"></a>

### frontendController

Generiert eine URL aus übergebenen Parametern

Beispiel:
`rex_url::frontendController(['key'=>'value'])` => '/index.php?key=value'
`rex_url::frontendController(['k1'=>'v1','k2'=>'v2'], true)` => '/index.php?k1=v1&amp;k2=v2'

<a name="urlbackend"></a>

### backend

Liefert den Backendpfad der Website

Beispiel:
`rex_url::backend()` => '/redaxo/'
`rex_url::backend('file.txt')` => '/redaxo/file.txt'

<a name="urlbackendController"></a>

### backendController

Generiert eine Backend-URL aus übergebenen Parametern

Beispiel:
`rex_url::backendController(['key'=>'value'])` => '/redaxo/index.php?key=value'
`rex_url::backendController(['k1'=>'v1','k2'=>'v2'], true)` => '/redaxo/index.php?k1=v1&amp;k2=v2'

<a name="urlbackendPage"></a>

### backendPage

Generiert eine URL zu einer Backend Seite

Beispiel:
`rex_url::backendPage('mypage',['key'=>'value'])` => '/redaxo/index.php?page=mypage&key=value'
`rex_url::backendPage('mypage',['k1'=>'v1','k2'=>'v2'], true)` => '/redaxo/index.php?page=mypage&amp;k1=v1&amp;k2=v2'

<a name="urlcurrentBackendPage"></a>

### currentBackendPage

Generiert eine URL zur aktuellen Backend-Seite. Sollte sinnvollerweise nur von einer Backend-Page aufgerufen werden, ansonsten ist der Parameter `page` leer.

Beispiel:
`rex_url::currentBackendPage(['key'=>'value'])` => '/redaxo/index.php?page=currpage&key=value'
`rex_url::currentBackendPage(['k1'=>'v1','k2'=>'v2'], true)` => '/redaxo/index.php?page=currpage&amp;k1=v1&amp;k2=v2'

<a name="urlmedia"></a>

### media

Liefert den Frontendpfad zum Media-Verzeichnis

Beispiel:
`rex_url::media()` => '/media/'
`rex_url::media('file.txt')` => '/media/file.txt'

<a name="urlassets"></a>

### assets

Liefert den Frontendpfad zum Assets-Verzeichnis

Beispiel:
`rex_url::assets()` => '/assets/'
`rex_url::assets('file.txt')` => '/assets/file.txt'

<a name="urlcoreAssets"></a>

### coreAssets

Liefert den Frontendpfad zum Assets-Verzeichnis des Core

Beispiel:
`rex_url::coreAssets()` => '/assets/core/'
`rex_url::coreAssets('file.txt')` => '/assets/core/file.txt'

<a name="urladdonAssets"></a>

### addonAssets

Liefert den Frontendpfad zum Assets-Verzeichnis eines AddOns

Beispiel:
`rex_url::addonAssets('meinaddon')` => '/assets/addons/meinaddon/'
`rex_url::addonAssets('meinaddon','file.txt')` => '/assets/addons/meinaddon/file.txt'

<a name="urlpluginAssets"></a>

### pluginAssets

Liefert den Frontendpfad zum Assets-Verzeichnis eines Plugins

Beispiel:
`rex_url::pluginAssets('meinaddon','meinplugin')` => '/assets/addons/meinaddon/plugins/meinplugin/'
`rex_url::pluginAssets('meinaddon','meinplugin','file.txt')` => '/assets/addons/meinaddon/plugins/meinplugin/file.txt'

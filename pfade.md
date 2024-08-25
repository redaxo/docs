# Pfade

* [Zugriff auf Dateisystem](#zugriff)
* [Dateisystem - rex_path](#rex_path)
  + [base](#base)
  + [frontend](#frontend)
  + [frontendController](#frontendController)
  + [backend](#backend)
  + [backendController](#backendController)
  + [media](#media)
  + [assets](#assets)
  + [coreAssets](#coreAssets)
  + [addonAssets](#addonAssets)
  + [pluginAssets](#pluginAssets)
  + [data](#data)
  + [coreData](#coreData)
  + [addonData](#addonData)
  + [pluginData](#pluginData)
  + [cache](#cache)
  + [coreCache](#coreCache)
  + [addonCache](#addonCache)
  + [pluginCache](#pluginCache)
  + [log](#log)
  + [src](#src)
  + [core](#core)
  + [addon](#addon)
  + [plugin](#plugin)
  + [absolute](#absolute)
* [URLs - rex_url](#rex_url)
  + [base](#urlbase)
  + [frontend](#urlfrontend)
  + [frontendController](#urlfrontendController)
  + [backend](#urlbackend)
  + [backendController](#urlbackendController)
  + [backendPage](#urlbackendPage)
  + [currentBackendPage](#urlcurrentBackendPage)
  + [media](#urlmedia)
  + [assets](#urlassets)
  + [coreAssets](#urlcoreAssets)
  + [addonAssets](#urladdonAssets)
  + [pluginAssets](#urlpluginAssets)

<a name="zugriff"></a>

## Zugriff auf das Dateisystem

Die Klassen `rex_path` und `rex_url` ermöglichen den Zugriff auf die entsprechenden Ressourcen im Dateisystem ( `rex_path` ) bzw. per URL ( `rex_url` ).

<a name="rex_path"></a>

## Dateisystem - rex_path

> **Hinweis:** Es wird nicht geprüft, ob die zurückgegebenen Pfade gültig sind oder existieren.

<a name="base"></a>

### base

Gibt den Base Pfad mit der übergebenen Datei oder dem Ordner zurück

Beispiele:

```php
rex_path::base()
// ergibt: "/htdocs/meinverzeichnis/"
```

```php
rex_path::base('index.php')
// ergibt: "/htdocs/meinverzeichnis/index.php"
```

<a name="frontend"></a>

### frontend

Gibt den Frontend-Pfad mit der übergebenen Datei oder dem Ordner zurück

Beispiele:

```php
rex_path::frontend()
// ergibt: "/htdocs/meinverzeichnis/"
```

```php
rex_path::frontend('index.php')
// ergibt: "/htdocs/meinverzeichnis/index.php"
```

<a name="frontendController"></a>

### frontendController

Pfad zum Frontend-Controller

Beispiel:
```php
rex_path::frontendController()
// ergibt: "/htdocs/meinverzeichnis/index.php"
```

<a name="backend"></a>

### backend

Pfad zum Backend

Beispiel:
```php
rex_path::backend()
// ergibt: "/htdocs/meinverzeichnis/redaxo/"
```

```php
rex_path::backend('meinedatei.php')
// ergibt: "/htdocs/meinverzeichnis/redaxo/meinedatei.php"
```

<a name="backendController"></a>

### backendController

Pfad zum Backend-Controller

Beispiel:
```php
rex_path::backendController()
// ergibt: "/htdocs/meinverzeichnis/redaxo/index.php"
```

<a name="media"></a>

### media

Pfad zum Media-Verzeichnis

Beispiel:
```php
rex_path::media()
// ergibt: "/htdocs/meinverzeichnis/media/"
```

<a name="assets"></a>

### assets

Pfad zum Assets-Verzeichnis

Beispiel:
```php
rex_path::assets()
// ergibt: "/htdocs/meinverzeichnis/assets/"
```

<a name="coreAssets"></a>

### coreAssets

Pfad zum Assets-Verzeichnis des Core

Beispiel:
```php
rex_path::coreAssets()
// ergibt: "/htdocs/meinverzeichnis/assets/core/"
```
```php
rex_path::coreAssets('file.txt')
// ergibt: "/htdocs/meinverzeichnis/assets/core/file.txt"
```

<a name="addonAssets"></a>

### addonAssets

Pfad zum Assets-Verzeichnis eines AddOns

Beispiel:
```php
rex_path::addonAssets('meinaddon')
// ergibt: "/htdocs/meinverzeichnis/assets/addons/meinaddon/"
```
```php
rex_path::addonAssets('meinaddon','file.txt')
// ergibt: "/htdocs/meinverzeichnis/assets/addons/meinaddon/file.txt"
```

<a name="pluginAssets"></a>

### pluginAssets

Pfad zum Assets-Verzeichnis eines Plugins

Beispiel:
```php
rex_path::pluginAssets('meinaddon','meinplugin')
// ergibt: "/htdocs/meinverzeichnis/assets/addons/meinaddon/plugins/meinplugin/"
```
```php
rex_path::pluginAssets('meinaddon','meinplugin','file.txt')
// ergibt: "/htdocs/meinverzeichnis/assets/addons/meinaddon/plugins/meinplugin/file.txt"
```

<a name="data"></a>

### data

Pfad zum Data-Verzeichnis

Beispiel:
```php
rex_path::data()
// ergibt: "/htdocs/meinverzeichnis/data/"
```

<a name="coreData"></a>

### coreData

Pfad zum Data-Verzeichnis des Core

Beispiel:
```php
rex_path::coreData()
// ergibt: "/htdocs/meinverzeichnis/data/core/"
```
```php
rex_path::coreData('file.txt')
// ergibt: "/htdocs/meinverzeichnis/data/core/file.txt"
```

<a name="addonData"></a>

### addonData

Pfad zum Data-Verzeichnis eines AddOns

Beispiel:
```php
rex_path::addonData('meinaddon')
// ergibt: "/htdocs/meinverzeichnis/data/addons/meinaddon/"
```
```php
rex_path::addonData('meinaddon','file.txt')
// ergibt: "/htdocs/meinverzeichnis/data/addons/meinaddon/file.txt"
```

<a name="pluginData"></a>

### pluginData

Pfad zum Data-Verzeichnis eines Plugins

Beispiel:
```php
rex_path::pluginData('meinaddon','meinplugin')
// ergibt: "/htdocs/meinverzeichnis/data/addons/meinaddon/plugins/meinplugin/"
```
```php
rex_path::pluginData('meinaddon','meinplugin','file.txt')
// ergibt: "/htdocs/meinverzeichnis/data/addons/meinaddon/plugins/meinplugin/file.txt"
```

<a name="cache"></a>

### cache

Pfad zum Cache-Verzeichnis

Beispiel:
```php
rex_path::cache()
// ergibt: "/htdocs/meinverzeichnis/redaxo/cache/"
```
```php
rex_path::cache('file.txt')
// ergibt: "/htdocs/meinverzeichnis/redaxo/cache/file.txt"
```

<a name="coreCache"></a>

### coreCache

Pfad zum Data-Verzeichnis

Beispiel:
```php
rex_path::coreCache()
// ergibt: "/htdocs/meinverzeichnis/redaxo/cache/core/"
```
```php
rex_path::coreCache('file.txt')
// ergibt: "/htdocs/meinverzeichnis/redaxo/cache/core/file.txt"
```

<a name="addonCache"></a>

### addonCache

Pfad zum Cache-Verzeichnis eines AddOns

Beispiel:
```php
rex_path::addonCache('meinaddon')
// ergibt: "/htdocs/meinverzeichnis/redaxo/cache/addons/meinaddon/"
```
```php
rex_path::addonCache('meinaddon','file.txt')
// ergibt: "/htdocs/meinverzeichnis/redaxo/cache/addons/meinaddon/file.txt"
```

<a name="pluginCache"></a>

### pluginCache

Pfad zum Cache-Verzeichnis eines Plugins

Beispiel:
```php
rex_path::pluginCache('meinaddon','meinplugin')
// ergibt: "/htdocs/meinverzeichnis/redaxo/cache/addons/meinaddon/plugins/meinplugin/"
```
```php
rex_path::pluginCache('meinaddon','meinplugin','file.txt')
// ergibt: "/htdocs/meinverzeichnis/redaxo/cache/addons/meinaddon/plugins/meinplugin/file.txt"
```

<a name="log"></a>

### Log

Pfad zur angegebenen Log-Datei.

Beispiel:
`rex_path::log('mail.log')` => `/httpdocs/redaxo/data/log/mail.log` 

<a name="src"></a>

### src

Pfad zum Src-Verzeichnis

Beispiel:
```php
rex_path::src()
// ergibt: "/htdocs/meinverzeichnis/redaxo/src/"
```
```php
rex_path::src('file.txt')
// ergibt: "/htdocs/meinverzeichnis/redaxo/src/file.txt"
```

<a name="core"></a>

### core

Pfad zum Core-Verzeichnis

Beispiel:
```php
rex_path::core()
// ergibt: "/htdocs/meinverzeichnis/redaxo/src/core/"
```
```php
rex_path::core('file.txt')
// ergibt: "/htdocs/meinverzeichnis/redaxo/src/core/file.txt"
```

<a name="addon"></a>

### addon

Pfad zum AddOn-Verzeichnis

Beispiel:
```php
rex_path::addon('meinaddon')
// ergibt: "/htdocs/meinverzeichnis/redaxo/src/addons/meinaddon/"
```
```php
rex_path::addon('meinaddon','file.txt')
// ergibt: "/htdocs/meinverzeichnis/redaxo/src/addons/meinaddon/file.txt"
```

<a name="plugin"></a>

### plugin

Pfad zum PlugIn-Verzeichnis

Beispiel:
```php
rex_path::plugin('meinaddon','meinplugin')
// ergibt: "/htdocs/meinverzeichnis/redaxo/src/addons/meinaddon/plugins/meinplugin/"
```
```php
rex_path::plugin('meinaddon','meinplugin','file.txt')
// ergibt: "/htdocs/meinverzeichnis/redaxo/src/addons/meinaddon/plugins/meinplugin/file.txt"
```

<a name="absolute"></a>

### absolute

Wandelt einen relativen Pfad zu einem absoluten Pfad

Beispiel:
```php
rex_path::absolute('../../src/addons')
// ergibt: "src/addons"
```

<a name="rex_url"></a>

## URLs - rex_url

> **Hinweis:** Bei allen URL-Funktionen der Klasse `rex_url` wird eine Installation von REDAXO in einem Unterverzeichnis berücksichtigt.

Funktionen, die Parameter zu URLs umschreiben, können die URL auch "escaped" zurückgeben.

<a name="urlbase"></a>

### base

Liefert den Basispfad der Website

Beispiel:
```php
rex_url::base()
// ergibt: "/"
```
```php
rex_url::base('file.txt')
// ergibt: "/file.txt"
```

<a name="urlfrontend"></a>

### frontend

Liefert den Frontendpfad der Website

Beispiel:
```php
rex_url::frontend()
// ergibt: "/"
```
Bei Installation in einem Unterverzeichnis:
```php
rex_url::frontend()
// ergibt: "/verzeichnis/"
```
```php
rex_url::frontend('file.txt')
// ergibt: "/verzeichnis/file.txt"
```

<a name="urlfrontendController"></a>

### frontendController

Generiert eine URL aus übergebenen Parametern

Beispiel:
```php
rex_url::frontendController(['key'=>'value'])
// ergibt: "/index.php?key=value"
```
```php
rex_url::frontendController(['k1'=>'v1','k2'=>'v2'], true)
// ergibt: "/index.php?k1=v1&amp; k2=v2"
```

<a name="urlbackend"></a>

### backend

Liefert den Backendpfad der Website

Beispiel:
```php
rex_url::backend()
// ergibt: "/redaxo/"
```
```php
rex_url::backend('file.txt')
// ergibt: "/redaxo/file.txt"
```

<a name="urlbackendController"></a>

### backendController

Generiert eine Backend-URL aus übergebenen Parametern

Beispiel:
```php
rex_url::backendController(['key'=>'value'])
// ergibt: "/redaxo/index.php?key=value"
```
```php
rex_url::backendController(['k1'=>'v1','k2'=>'v2'], true)
// ergibt: "/redaxo/index.php?k1=v1&amp; k2=v2"
```

<a name="urlbackendPage"></a>

### backendPage

Generiert eine URL zu einer Backend Seite

Beispiel:
```php
rex_url::backendPage('mypage',['key'=>'value'])
// ergibt: "/redaxo/index.php?page=mypage&key=value"
```
```php
rex_url::backendPage('mypage',['k1'=>'v1','k2'=>'v2'], true)
// ergibt: "/redaxo/index.php?page=mypage&amp; k1=v1&amp; k2=v2"
```

<a name="urlcurrentBackendPage"></a>

### currentBackendPage

Generiert eine URL zur aktuellen Backend-Seite. Sollte sinnvollerweise nur von einer Backend-Page aufgerufen werden, ansonsten ist der Parameter `page` leer.

Beispiel:
```php
rex_url::currentBackendPage(['key'=>'value'])
// ergibt: "/redaxo/index.php?page=currpage&key=value"
```
```php
rex_url::currentBackendPage(['k1'=>'v1','k2'=>'v2'], true)
// ergibt: "/redaxo/index.php?page=currpage&amp; k1=v1&amp; k2=v2"
```

<a name="urlmedia"></a>

### media

Liefert den Frontendpfad zum Media-Verzeichnis

Beispiel:
```php
rex_url::media()
// ergibt: "/media/"
```
```php
rex_url::media('file.txt')
// ergibt: "/media/file.txt"
```

<a name="urlassets"></a>

### assets

Liefert den Frontendpfad zum Assets-Verzeichnis

Beispiel:
```php
rex_url::assets()
// ergibt: "/assets/"
```
```php
rex_url::assets('file.txt')
// ergibt: "/assets/file.txt"
```

<a name="urlcoreAssets"></a>

### coreAssets

Liefert den Frontendpfad zum Assets-Verzeichnis des Core

Beispiel:
```php
rex_url::coreAssets()
// ergibt: "/assets/core/"
```
```php
rex_url::coreAssets('file.txt')
// ergibt: "/assets/core/file.txt"
```

<a name="urladdonAssets"></a>

### addonAssets

Liefert den Frontendpfad zum Assets-Verzeichnis eines AddOns

Beispiel:
```php
rex_url::addonAssets('meinaddon')
// ergibt: "/assets/addons/meinaddon/"
```
```php
rex_url::addonAssets('meinaddon','file.txt')
// ergibt: "/assets/addons/meinaddon/file.txt"
```

<a name="urlpluginAssets"></a>

### pluginAssets

Liefert den Frontendpfad zum Assets-Verzeichnis eines Plugins

Beispiel:
```php
rex_url::pluginAssets('meinaddon','meinplugin')
// ergibt: "/assets/addons/meinaddon/plugins/meinplugin/"
```
```php
rex_url::pluginAssets('meinaddon','meinplugin','file.txt')
// ergibt: "/assets/addons/meinaddon/plugins/meinplugin/file.txt"
```

# Änderungen REDAXO 4 zu 5

- [$REX](#rex)
- [REX_VAR](#rex-var)
- [Funktionen und Klassen](#funktiopnen-klassen)
- [Extension Points](#extension-points)
- [rex_sql](#rex-sql)
    - [Fehlermeldung in REDAXO 4](#fehler-rex4)
    - [Fehlermeldung in REDAXO 5](#fehler-rex5)
- [rex_form](#rex)
- [Packages (AddOns/PlugIns)](#packages)

<a name="rex"></a>
## $REX

> *Hinweis:* Die Listen sind nicht vollständig.

Die globale Variable `$REX` wurde entfernt. Im Wesentlichen wurde sie ersetzt durch die statische Klasse `rex`, viele Dinge aus `$REX` werden nun aber auch an anderen Stellen gelagert. AddOn-spezifische Dinge sollten zum Beispiel direkt in den neuen AddOn-Objekten gelagert werden (siehe unten). Möchte man aber Daten modulübergreifend zwischenlagern o.ä., kann man dafür durchaus die Methoden `rex::setProperty()` und `rex::getProperty()` verwenden.

| REDAXO 4 | REDAXO 5 |
| ------------- | ------------- |
| `$REX['KEY']` etc. | `rex::getProperty('key')` `rex::setProperty('key', $value)` |
| `$REX['SERVER']` | `rex::getServer()` |
| `$REX['SERVERNAME']` | `rex::getServerName()` |
| `$REX['REDAXO']` | `rex::isBackend()` |
| `$REX['CUR_CLANG']` | `rex_clang::getCurrentId()` |
| `$REX['ARTICLE_ID']` | `rex_article::getCurrentId()` |
| `$REX['START_ARTICLE_ID']` | `rex_article::getSiteStartArticleId()` |
| `$REX['NOTFOUND_ARTICLE_ID']` | `rex_article::getNotfoundArticleId()` |
| `$REX['CLANG']` | `rex_clang::getAll()` |
| `$REX['MOD_REWRITE']` | Existiert nicht mehr |
| `$REX['TABLE_PREFIX']` | `rex::getTablePrefix()`<br>`rex::getTable($table)` (ergibt: `'rex_'.$table`) |
| `$REX['DB']` | `rex::getProperty('db')` |
| `$REX['USER']`<br>`$REX['USER']->hasPerm('myperm[]')` | `rex::getUser()`<br>`rex::getUser()->hasPerm('myperm[]')` |
| `$REX['PERM'][] = 'myperm[]'` | `rex_perm::register('myperm[]', $name = null)`<br>Zweiter (optionaler) Parameter ist ein Bezeichner, der in der Rechteverwaltung erscheint |
| `$REX['EXTPERM'][] = 'myperm[]'` | `rex_perm::register('myperm[]', $name = null, rex_perm::OPTIONS)` |
| `$REX['EXTRAPERM'][] = 'myperm[]'` | `rex_perm::register('myperm[]', $name = null, rex_perm::EXTRAS)` |
| `$REX['HTDOCS_PATH']`<br>`$REX['INCLUDE_PATH']`<br>`$REX['FRONTEND_PATH']`<br>`$REX['MEDIAFOLDER']`<br>`$REX['FRONTEND_FILE']` | `rex_path` [siehe hier](/{{path}}/{{version}}/pfade) |
| `$REX['ADDON']` | `rex_addon`, bzw. `rex_plugin` (siehe weiter unten) |

<a name="rex-var"></a>
## REX_VAR

| REDAXO 4 | REDAXO 5 |
| ------------- | ------------- |
| `VALUE[]` | `REX_INPUT_VALUE[]` |
| `REX_HTML_VALUE[id=1]` | `REX_VALUE[id=1 output=html]` |
| `INPUT_PHP` | `REX_INPUT_VALUE[]` |
| `REX_PHP` | `REX_VALUE[id=1 output=php]` |
| `REX_LINK_BUTTON[id=1]` | `REX_LINK[id=1 widget=1]` |
| `REX_LINKLIST_BUTTON[id=1]` | `REX_LINKLIST[id=1 widget=1]` |
| `REX_MEDIA_BUTTON[id=1]` | `REX_MEDIA[id=1 widget=1]` |
| `REX_MEDIALIST_BUTTON[id=1]` | `REX_MEDIALIST[id=1 widget=1]` |

<a name="funktionen-klassen"></a>
## Funktionen und Klassen

| REDAXO 4 | REDAXO 5 |
| ------------- | ------------- |
| `OOArticle`<br>`OOCategory`<br>`OOMedia`<br>`OOMediaCategory`<br>`OOArticleSlice` | `rex_article`<br>`rex_category`<br>`rex_media`<br>`rex_media_category`<br>`rex_article_slice` |
| `rex_article` | `rex_article_content` |
| `OOArticle::getArticleById()`<br>`OOCategory::getCategoryById()`<br>`OOMedia::getMediaByFilename()`<br>`OOMediaCategory::getCategoryById()` | `rex_article::get()`<br>`rex_category::get()`<br>`rex_media::get()`<br>`rex_media_category::get()` |
| `OOArticle::isValid()`<br>`OOCategory::isValid()`<br>`OOMedia::isValid()`<br> `OOMediaCategory::isValid()` | Entfernt, stattdessen:<br>`$art instanceof rex_article` etc. |
| `$article->getDescription`()<br>`$article->isStartPage()` | `$article->getValue('art_description')`<br>`$article->isStartArticle()` |
| `rex_register_extension()`<br>`rex_register_extension_point()`<br>`REX_EXTENSION_EARLY`<br>`REX_EXTENSION_LATE` | `rex_extension::register()`<br>`rex_extension::registerPoint()`<br>`rex_extension::EARLY`<br>`rex_extension::LATE` |
| `rex_title()`<br>`rex_info()`<br>`rex_warning()`, etc. | `rex_view::title()`<br>`rex_view::info()`<br>`rex_view::warning()`<br>, etc. |
| `rex_put_file_contents()` | `rex_file::put()`<br>`rex_file::putCache()` (JSON-formatiert)<br> `rex_file::putConfig()` (YAML-formatiert) |
| `rex_get_file_contents()` | `rex_file::get()`<br>`rex_file::getCache()`<br> `rex_file::getConfig()` |
| `rex_replace_dynamic_contents()` | Entfernt, da dynamische Inhalte in eigenen Dateien gespeichert werden sollen |
| `rex_deleteDir()`<br>`rex_deleteFiles()`<br>`rex_createDir()`<br>`rex_copyDir()` | `rex_dir::delete()`<br>`rex_dir::deleteFiles()`<br>`rex_dir::create()`<br>`rex_dir::copy()` |
| `rex_absPath()` | `rex_path::absolute()` |
| `rex_send_file()`<br>`rex_send_resource()`<br>`rex_send_article()`<br>`rex_send_content()` | `rex_response::sendFile()`<br>`rex_response::sendResource()`<br>`rex_response::sendArticle()`<br>`rex_response::sendContent()` |
| `rex_generateAll()`<br>`rex_deleteAll()` | `rex_delete_cache()` |
| `rex_call_func()`<br>`rex_check_callable()` | Entfernt, stattdessen: `call_user_func()` / `call_user_func_array()`<br />Entfernt, stattdessen: `is_callable()` |
| `rex_split_string()` | `rex_string::split()` |
| `rex_addslashes()` | Entfernt, stattdessen: `addslashes()` / `addcslashes()` |
| `rex_highlight_string`()<br>`rex_highlight_file()` | `rex_string::highlight()` |
| `rex_tabindex()` | Entfernt |
| `rex_hasBackendSession()` | `rex_backend_login::hasSession()` |
| `$I18N->msg`()<br>`rex_translate()` | `rex_i18n::msg()`<br>`rex_i18n::translate()` |
| `rex_lang_is_utf8()` | Entfernt, da REDAXO 5 immer UTF8 verwendet |
| `rex_create_lang()` | Entfernt, da rex_i18n nun statisch ist |
| `OOAddon::getProperty($addon, $property)`<br>`OOAddon::isAvailable($addon)`<br>`OOPlugin::isInstalled($addon, $plugin)` etc. | `rex_addon::get($addon)->getProperty($property)`<br>`rex_addon::get($addon)->isAvailable()`<br>`rex_plugin::get($addon, $plugin)->isInstalled()` etc. |
| `rex_install_dump()`<br>`rex_organize_priorities()` | `rex_sql_util::importDump()`<br>`rex_sql_util::organizePriorities()` |
| `rex_getAttributes()`<br>`rex_setAttributes()` | In der Form entfernt, stattdessen `rex_sql::getArrayValue()` und `rex_sql::setArrayValue()` |
| `rex_a79_textile()` | `rex_textile::parse()` |

<a name="extension-points"></a>
## Extension Points

| REDAXO 4 | REDAXO 5 |
| ------------- | ------------- |
| `ALL_GENERATED` | `CACHE_DELETED` |
| `ADDONS_INCLUDED` | `PACKAGES_INCLUDED` |
| `OUTPUT_FILTER_CACHE` | `RESPONSE_SHUTDOWN` |
| `OOMEDIA_IS_IN_USE` | `MEDIA_IS_IN_USE` |

<a name="rex-sql"></a>
## rex_sql

Die Methoden `setQuery()`, `insert()`, `update()` etc. liefern keine boolschen Werte mehr zurück, sondern das aktuelle rex_sql-Objekt.

| REDAXO 4 | REDAXO 5 |
| ------------- | ------------- |
| `$sql->setWhere('myid="35" OR abc="zdf"')` | `$sql->setWhere('myid = :id OR abc = :abc', array(':id' => 3, ':abc' => 'zdf'))`<br>oder<br>`$sql->setWhere(array(array('id' => 3, 'abc' => 'zdf')))`|
| `$sql->setQuery('UPDATE rex_table SET a="$i" WHERE myid="35" ')` | `$sql->setQuery('UPDATE rex_table SET a=? WHERE myid="35" ', array($i))` |
| `$sql->setQuery('SELECT * FROM rex_table WHERE col_str = "$adf" and col_int = "4"')` | `$sql->setQuery('SELECT * FROM rex_table WHERE col_str = :mystr and col_int = :myint', array(':mystr' => $adf, ':myint' => 4))`|

 Bei Fehlern wird eine `rex_sql_exception` geworfen.

<a name="fehler-rex4"></a>
### Fehlermeldung in REDAXO 4

```php
<?php
if ($sql->update()) {
    $info = 'Success';
} else {
    $error = $sql->getError();
}
```

<a name="fehler-rex5"></a>
### Fehlermeldung in REDAXO 5

```php
<?php
try {
    $sql->update();
    $info = 'Success';
} catch (rex_sql_exception $e) {
    $error = $e->getMessage();
}
```

<a name="rex-form"></a>
## rex_form

| REDAXO 4 | REDAXO 5 |
| ------------- | ------------- |
| `$form = rex_form::factory('table', 'legend', 'id="'.$id.'"', 'post', false, 'my_form_class');` | `$form = new my_form_class('table', 'legend', 'id="'.$id.'"', 'post', false);`<br>oder<br> `$form = my_form_class::factory('table', 'legend', 'id="'.$id.'"', 'post', false);` |

<a name="packages"></a>
## Packages (AddOns/PlugIns)

Package ist der neue gemeinsame Oberbegriff für AddOns und PlugIns.

| REDAXO 4 | REDAXO 5 |
| ------------- | ------------- |
| `(un)install.inc.php` | `(un)install.php` |
| `config.inc.php` | `package.yml`<br>`boot.php` |
| `classes/` | `lib/`<br>`vendor/` (für externe Klassen) |
| `files/` | `assets/` |
| `pages/index.inc.php` | `pages/index.php` |

Die statischen Package-Informationen, wie Version, Autor etc. sollten statt in der `boot.php` (ehemals `config.inc.php`), in der neuen `package.yml` stehen. In dieser Datei kann auch angegeben werden, welche REDAXO-Version, welche PHP-Extensions oder welche AddOns und PlugIns benötigt werden (wird automatisch überprüft). Beispiel:

```yaml
package: mein_addon
version: '1.3'
author: Vorname Nachname
supportpage: forum.redaxo.de

page:
  title: Mein tolles AddOn
  perm: mein_addon[]
  block: system

requires:
  redaxo: '~5.1'
  php:
    version: '>=5.3.4'
    extensions: [gd, xml]
  packages:
    structure: '5.0.1'
    structure/content: '>5.0, <5.2'
```

Es können aber auch weiterhin Package-Informationen in der `boot.php` gesetzt werden, aber nicht mehr über `$REX['ADDON']`, sondern über die neue Package-api. Das aktuelle Objekt (`rex_addon` oder `rex_plugin`) ist in den Dateien (`boot.php`, `install.php`, `pages/index.php` etc.) über `$this` erreichbar.

```
// Beispiel boot.php
$this->setProperty('author', 'Vorname Nachname');

// Beispiel install.php
$error = '';

// Überprüfungen
if($error)
  $this->setProperty('installmsg', $error);
else
  $this->setProperty('install', true);
```

Innerhalb von Klassen und Funktionen, wo das Package nicht über `$this` zur Verfügung steht, kann so auf die Daten zugegriffen werden:

```
$author = rex_addon::get('myaddon')->getProperty('author');
```

Außer der `package.yml` sind alle Dateien (`boot.php`, `install.php`, `uninstall.php` etc.) optional. Die `package.yml` benötigt auf jeden Fall die "package"- und "version"-Angabe.

Dadurch, dass die Dateien aus den Objekten heraus eingebunden werden (damit `$this` zur Verfügung steht), sind globale Variablen nicht mehr automatisch verfügbar.

Der Klassenordner `classes` heißt jetzt `lib`. Die Klassen in diesem Ordner (und in den Unterordnern) müssen nicht mehr manuell über `include/require` eingebunden werden, dies übernimmt das "Autoloading" bei Bedarf automatisch.

Die Sprachdateien im `lang`-Ordner werden automatisch dem Sprachkatalog hinzugefügt.

Der `files`-Ordner in der REDAXO-Root-Ebene wurde aufgeteilt, die Dateien des Medienpools liegen nun im `media`-Ordner, für die Dateien der AddOns/PlugIns gibt es den `assets`-Ordner. Dementsprechend muss der ehemalige `files`-Ordner innerhalb der Packages nun `assets` heißen.

Die `layout/top.php` und `layout/bottom.php` werden automatisch eingebunden.

Die Dateien im AddOn-, bzw. PlugIn-Ordner sollten nicht mehr verändert werden, um automatische Updates zu ermöglichen. Konfigurationswerte können über die neue `rex_config` in der Datenbank gespeichert werden (diese werden gecacht):

```
rex_config::set($addon, $key, $value);
$value = rex_config::get($addon, $key);

// alternativ über das Package-Objekt:
rex_addon::get($addon)->setConfig($key, $value);
$value = rex_addon::get($addon)->getConfig($key);

// oder falls das Package-Objekt über $this erreichbar ist (config.inc.php etc.):
$this->setConfig($key, $value);
$value = $this->getConfig($key);
```

Des Weiteren können Daten im Ordner `redaxo/data/addons/$addonName` abgelegt werden, der Pfad ist über `rex_path::addonData($addon)` und `rex_addon::get($addon)->getDataPath()`, bzw. `$this->getDataPath()` erreichbar.


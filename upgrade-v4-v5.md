# Upgradehinweise von REDAXO 4 zu REDAXO 5.x

* [Einleitung](#einleitung)
  + [Konvertierung einer Version < 4.6](#less46)
* [Erste Schritte](#1st)
* [YConverter installieren](#install)
* [Konvertierung der Daten](#convert)
  + [XForm konvertieren](#xform)
* [Übertragung der Datenbank zu REDAXO 5](#transfer)
* [Dateien kopieren](#copyfiles)
* [Nachbearbeitung, Fehlerbereinigung](#service)
* [$REX](#rex)
* [REX_VAR](#rex-var)
* [Funktionen und Klassen](#funktionen-klassen)
* [Extension Points](#extension-points)
* [rex_sql](#rex-sql)
* [Fehlermeldung in REDAXO 4](#fehler-rex4)
* [Fehlermeldung in REDAXO 5](#fehler-rex5)
* [rex_form](#rex)
* [Packages (AddOns/PlugIns)](#packages)

<a name="einleitung"></a>

## Einleitung

Voraussetzungen:

* Website REDAXO ab 4.6 / ***[Hinweis für ältere Versionen](#less46)***
* Eine frische REDAXO 5.x Installation, ggf. in einem separaten Webspace, unter einer Subdomain oder in einer lokalen Installation.
* Installiertes Adminer-AddOn in der REDAXO 5.x Instanz (falls noch nicht installiert -> ***Installer->Neue herunterladen*** und installieren)
* Die Templates sollten nicht per require oder include eingebunden sein, sondern direkt eingepflegt sein, andernfalls kann yconverter keine Konvertierung hier durchführen.

REDAXO 5 ist mit den Vorgängerversionen nicht vollständig kompatibel. Die Projekte (z. B. eine Website) müssen zum neuen System migriert werden. Dies erfolgt durch eine Datenbank-Konvertierung, Nachbearbeitung von Modulen und Templates sowie Verschieben von Dateien des files-Ordners.

> Daten zusätzlich installierter AddOns, außer yform, können nicht konvertiert werden und müssen ggf. separat migriert werden. Es empfiehlt sich vorher zu prüfen, welche AddOns in REDAXO 5 fortgeführt werden und ob diese eine Lösung zum Import älterer Versionen anbieten. Alternativ bieten sich ähnliche AddOns an, die die gewünschte Funktionalität wiederherstellen.
> Benutzerkonten werden nicht konvertiert und müssen in REDAXO 5 neu angelegt werden.

Wer Hilfe bei der Konvertierung benötigt oder diese beauftragen möchte, findet im ***[Slack-Channel](https://redaxo.org/support/community/#slack)*** sicher bereitwillige Helfer.

<a name="1st"></a>

## Erste Schritte

Vor Beginn sollten folgende Schritte durchgeführt werden.

* Deaktivieren der Redakteure um zu vermeiden, dass weitere Inhalte eingepflegt werden. **Benutzer** -> ***Benutzername anklicken*** -> ***Checkbox aktiv deaktivieren*** -> **speichern**
* Backup der Webpräsenz durchführen, z. B. mit dem Backup-AddOn oder mit den vom Hoster bereitgestellten Backuplösungen.

<a name="install"></a>

## YConverter installieren

YConverter ist nicht im Installer verfügbar und muss in GitHub heruntergeladen werden und dann in die REDAXO 4.x Installation hochgeladen werden.

* [Zum GitHub-Repo](https://github.com/yakamara/yconverter/tree/redaxo4)
* [Direkter Download](https://github.com/yakamara/yconverter/archive/redaxo4.zip)

Man erhält eine Zip-Datei mit der Bezeichnung `redaxo4.zip` . Die Datei muss lokal entpackt werden und der Ordner ggf. in yconverter umbenannt werden. Anschließend kopiert man den Ordner in den Ordner ***/redaxo/include/addons*** der REDAXO 4.x Installation. Danach lässt es sich in der AddOn-Verwaltung installieren.

> Tipp: Einige Hoster bieten Oberflächen (PLESK, CPANEL) an um die Zip-Datei direkt auf dem Server hochzuladen und zu entpacken.

<a name="convert"></a>

## Konvertierung der Daten

Nach erfolgter Installation findet man in der Navigation des REDAXO 4.x Projektes den Navigationspunkt YConverter.

Die nachfolgenden Tabellen werden in ihrer Struktur und Inhalte in die REDAXO 4 Datenbank dupliziert und für REDAXO 5 modifiziert. Die Tabellenspalten werden angepasst, nicht mehr genutzte Spalten gelöscht, Inhalte teilweise verschoben bzw. konvertiert.

***Tabellen die konvertiert werden***

* `rex_62_params` 
* `rex_62_type` 
* `rex_679_type_effects` 
* `rex_679_types` 
* `rex_action` 
* `rex_article` 
* `rex_article_slice` 
* `rex_clang` 
* `rex_file` 
* `rex_file_category` 
* `rex_module` 
* `rex_module_action` 
* `rex_template` 

> Hinweis: Die Konvertierung hat keinen Einfluss auf die Funktionalität der Webpräsenz. Die REDAXO 4.x-Tabellen bleiben erhalten. Es werden neue Tabellen mit dem Prefix ***yconverter_*** angelegt.

Nach Bestätigen mit ***Nun auf geht's!*** wird die Konvertierung durchgeführt.

Findet YConverter Stellen im konvertierten Quellcode, die später nachgearbeitet werden müssen zeigt YConverter diese im Protokoll an. Es empfiehlt sich diese Meldungen zu kopieren und für die spätere Nachbereitung zu sichern.

![Meldungen bei der Konvertierung](/assets/v5.6.3.yconverter_screen.png)

Meldungen bei der Konvertierung

<a name="xform"></a>

### XForm konvertieren

YConverter bietet auch die Konvertierung von XForm-Tabellen an. Auch hier werden die Tabellen wie oben beschrieben konvertiert und können mittels Formular in die neue Instanz migriert werden.

Nach der Übertragung der Daten installiert man in REDAXO 5.x YForm und die Tabellen sollten dann wie gewohnt erscheinen.

<a name="transfer"></a>

## Übertragung der Datenbank zu REDAXO 5

### Variante 1

Die konvertierten Tabellen können mit dem Formular direkt in die REDAXO 5 Präsenz übertragen werden.

> Hinweis: Nach der Übertragung wird keine Meldung angezeigt. Es sollte in der REDAXO 5 Präsenz geprüft werden ob die Daten übertragen wurden.

### Variante 2; Manueller Weg

Ist eine direkte Übertragung nicht möglich, da man z. B. keinen Zugriff auf die externe Datenbank von extern hat, ist eine manuelle Übertragung der Daten erforderlich. Hierzu wird in YConverter Adminer mitgeliefert.

> **Hinweis** Es ist ggf. erforderlich, dass in der REDAXO 5 Präsenz vorab z. B. Metainfo-Felder oder sonstige Tabellenspalten von AddOns, die in der REDAXO 4 Präsenz existieren, vorab angelegt werden müssen. Hierbei sollte man auf die SQL-Fehlermeldungen achten.

1. Den Adminer in REDAXO 4 in neuem Tab aufrufen.
2. Im Adminer von REDAXO 4 oben links auf `Exportieren` klicken.
3. Alle Tabellen und Daten wegklicken (im Tabellenkopf).
4. Nur die `Daten` auswählen deren Tabelle mit `yconverter_` beginnen. ***Es darf keine Checkbox bei Tabelle aktiviert werden***.
5. Button `Exportieren` klicken.
6. Erstellte Daten in die Zwischenablage kopieren
7. Im Adminer von REDAXO 5 oben links SQL-Kommando klicken und das Kopierte in das Textfeld einfügen.
8. Nach `yconverter_` im Textfeld suchen und löschen. (ggf. in einem Texteditor per suchen und Ersetzen)
9. Den Button Ausführen klicken.

<a name="copyfiles"></a>

## Dateien kopieren

Da sich die Dateistruktur in REDAXO 5 geändert hat, müssen die Dateien aus dem `/files` -Ordner in den neuen media-Ordner `/media/` in REDAXO 5 kopiert werden. Unterordner, die durch AddOns erstellt wurden, werden nicht benötigt.

Eigene Ordner, die Assets für die Darstellung beinhalten (z. B. für CSS und JS) können in ihre ursprüngliche Position kopiert werden.

> Sollten Assets in Unterordnern von /files angelegt sein, z. B. /files/styles/ könnte es zu Problemen bei der Verwendung in Verbindung von Rewrite-AddOns und dem Media-Manager kommen. Eine Verschiebung in einen anderen Ordner z. B: `/assets/styles/` und Anpassung der Templates und Module sorgt für Abhilfe.  

<a name="service"></a>

## Nachbearbeitung, Fehlerbereinigung

Nach erfolgreichem Import den Cache unter System in REDAXO 5 löschen und somit neu anlegen lassen.

Nach der Übertragung der Daten ist die Präsenz meist noch nicht voll einsatzfähig.

Sofern es Warnmeldungen bei der Konvertierung gab, sollten diese Stellen als erste abgearbeitet werden. Die entsprechenden Zeilennummern und Codestellen in Modulen und Templates wurden hierfür angegeben.

REDAXO hilft bei der Suche der Fehler. Die REDAXO-Whoops-Meldung liefert die nötigen Informationen und Codestellen in denen eine Überarbeitung erforderlich ist. Damit dies geschehen kann, muss man im Backend eingeloggt sein.
Soweit wie möglich einfach die Website und das Backend absurfen und schauen ob ein Fehler erscheint. Des weiteren sollte man regelmäßig das ***Systemlog*** von REDAXO aufsuchen und nach gefundenen Fehlern Ausschau halten.

Häufig sind die gefundenen Fehler Codefragmente, die bereits in REDAXO 4.x als veraltet angesehen wurden und ausgetauscht werden sollten. Bei der Korrektur des Codes könnte folgende Seiten hilfreich sein:

* [Weiterführende Tipps nach Konvertierung von REDAXO 4.x zu 5 in den FOR Tricks](https://friendsofredaxo.github.io/tricks/howto/redaxo_4_5_upgrade)

<a name="less46"></a>

## Konvertierung einer Version < 4.6

Es ist nicht nötig ein vollständiges Update der Webpräsenz auf eine aktuelle 4er-Installation durchzuführen. Nur die Datenbank muss auf den aktuellen Stand gebracht werden. Ein Upgrade auf eine aktuelle Version (z. B: 4.7.3) kann daher wie folgt durchgeführt werden:

* Export der Datenbank mittels Import-/Export-AddOn
* Separate, leere Installation einer geeigneten REDAXO 4.x Version (z. B. 4.7.3)
* Installation von YConverter wie [oben](#install) beschrieben in dieser aktuellen Installation
* Import der exportierten Datenbank in der neuen Installation, dadurch wird diese konvertiert und ist geeignet für die Bearbeitung durch YConverter.
* Überprüfen ob die Umlaute der Module im Backend korrekt sind. War es zuvor eine Installation mit ISO-Format (bei Versionen vor 4.5), sollte folgender Tipp berücksichtigt werden und die Daten müssen konvertiert werden: [Inhalte von Iso auf Utf-8 konvertieren](https://redaxo.org/doku/4.6/convert-iso-utf8)
* Anschließend die Datenbank mit YConverter konvertieren: [Konvertierung der Daten](#convert) und nach REDAXO 5.x entsprechend der Anleitung übertragen

> **Tipp**: Beim späteren Kopieren der Dateien des /files-Ordners darauf achten, dass dort befindliche Cache-Files nicht kopiert werden müssen. (Ältere Versionen von REDAXO erstellen im Files-Ordner Cache-Dateien, die nicht benötigt werden). Ggf. den Cache vor dem Kopieren der Dateien unter **System** löschen.

<a name="rex"></a>

## $REX

> *Hinweis:* Die Listen sind nicht vollständig.

Die globale Variable `$REX` wurde entfernt. Im Wesentlichen wurde sie ersetzt durch die statische Klasse `rex` , viele Dinge aus `$REX` werden nun aber auch an anderen Stellen gelagert. AddOn-spezifische Dinge sollten zum Beispiel direkt in den neuen AddOn-Objekten gelagert werden (siehe unten). Möchte man aber Daten modulübergreifend zwischenlagern o.ä., kann man dafür durchaus die Methoden `rex::setProperty()` [siehe hier](https://redaxo.org/doku/main/eigenschaften#set-property) und `rex::getProperty()` [siehe hier](https://redaxo.org/doku/main/eigenschaften#get-property)  verwenden.

| REDAXO 4 | REDAXO 5 |
| ------------- | ------------- |
| `$REX['KEY']` etc. | `rex::getProperty('key')`  `rex::setProperty('key', $value)` |
| `$REX['SERVER']` | `rex::getServer()` |
| `$REX['SERVERNAME']` | `rex::getServerName()` |
| `$REX['REDAXO']` | `rex::isBackend()` zusätzlich `rex::isFrontend()` um zu prüfen ob Frontend|
| `$REX['CUR_CLANG']` | `rex_clang::getCurrentId()` <br>Erste Sprache = 1 |
| `$REX['ARTICLE_ID']` | `rex_article::getCurrentId()` |
| `$REX['START_ARTICLE_ID']` | `rex_article::getSiteStartArticleId()` |
| `$REX['NOTFOUND_ARTICLE_ID']` | `rex_article::getNotfoundArticleId()` |
| `$REX['CLANG']` | `rex_clang::getAll()` |
| `$REX['MOD_REWRITE']` | Existiert nicht mehr |
| `$REX['TABLE_PREFIX']` | `rex::getTablePrefix()` <br> `rex::getTable($table)` (ergibt: `'rex_'.$table` ) |
| `$REX['DB']` | `rex::getProperty('db')` |
| `$REX['USER']` <br> `$REX['USER']->hasPerm('myperm[]')` | `rex::getUser()` <br> `rex::getUser()->hasPerm('myperm[]')` |
| `$REX['PERM'][] = 'myperm[]'` | `rex_perm::register('myperm[]', $name = null)` <br>Zweiter (optionaler) Parameter ist ein Bezeichner, der in der Rechteverwaltung erscheint |
| `$REX['EXTPERM'][] = 'myperm[]'` | `rex_perm::register('myperm[]', $name = null, rex_perm::OPTIONS)` |
| `$REX['EXTRAPERM'][] = 'myperm[]'` | `rex_perm::register('myperm[]', $name = null, rex_perm::EXTRAS)` |
| `$REX['HTDOCS_PATH']` <br> `$REX['INCLUDE_PATH']` <br> `$REX['FRONTEND_PATH']` <br> `$REX['MEDIAFOLDER']` <br> `$REX['FRONTEND_FILE']` | `rex_path` [siehe hier](/{{path}}/{{version}}/pfade) |
| `$REX['ADDON']` | `rex_addon` , bzw. `rex_plugin` (siehe weiter unten) |

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
| `OOArticle` <br> `OOCategory` <br> `OOMedia` <br> `OOMediaCategory` <br> `OOArticleSlice` | `rex_article` <br> `rex_category` <br> `rex_media` <br> `rex_media_category` <br> `rex_article_slice` |
| `rex_article` | `rex_article_content` |
| `OOArticle::getArticleById()` <br> `OOCategory::getCategoryById()` <br> `OOMedia::getMediaByFilename()` <br> `OOMediaCategory::getCategoryById()` | `rex_article::get()` <br> `rex_category::get()` <br> `rex_media::get()` <br> `rex_media_category::get()` |
| `OOArticle::isValid()` <br> `OOCategory::isValid()` <br> `OOMedia::isValid()` <br> `OOMediaCategory::isValid()` | Entfernt, stattdessen:<br> `$art instanceof rex_article` etc. |
| `$article->getDescription` ()<br> `$article->isStartPage()` | `$article->getValue('art_description')` <br> `$article->isStartArticle()` |
| `rex_register_extension()` <br> `rex_register_extension_point()` <br> `REX_EXTENSION_EARLY` <br> `REX_EXTENSION_LATE` | `rex_extension::register()` <br> `rex_extension::registerPoint()` <br> `rex_extension::EARLY` <br> `rex_extension::LATE` |
| `rex_title()` <br> `rex_info()` <br> `rex_warning()` <br>, etc. | `rex_view::title()` <br> `rex_view::info()` <br> `rex_view::warning()` <br>, etc. |
| `rex_put_file_contents()` | `rex_file::put()` <br> `rex_file::putCache()` (JSON-formatiert)<br> `rex_file::putConfig()` (YAML-formatiert) |
| `rex_get_file_contents()` | `rex_file::get()` <br> `rex_file::getCache()` <br> `rex_file::getConfig()` |
| `rex_replace_dynamic_contents()` | Entfernt, da dynamische Inhalte in eigenen Dateien gespeichert werden sollen |
| `rex_deleteDir()` <br> `rex_deleteFiles()` <br> `rex_createDir()` <br> `rex_copyDir()` | `rex_dir::delete()` <br> `rex_dir::deleteFiles()` <br> `rex_dir::create()` <br> `rex_dir::copy()` |
| `rex_absPath()` | `rex_path::absolute()` |
| `rex_send_file()` <br> `rex_send_resource()` <br> `rex_send_article()` <br> `rex_send_content()` | `rex_response::sendFile()` <br> `rex_response::sendResource()` <br> `rex_response::sendArticle()` <br> `rex_response::sendContent()` |
| `rex_generateAll()` <br> `rex_deleteAll()` | `rex_delete_cache()` |
| `rex_call_func()` <br> `rex_check_callable()` | Entfernt, stattdessen: `call_user_func()` / `call_user_func_array()` <br />Entfernt, stattdessen: `is_callable()` |
| `rex_split_string()` | `rex_string::split()` |
| `rex_addslashes()` | Entfernt, stattdessen: `addslashes()` / `addcslashes()` |
| `rex_highlight_string` ()<br> `rex_highlight_file()` | `rex_string::highlight()` |
| `rex_tabindex()` | Entfernt |
| `rex_hasBackendSession()` | `rex_backend_login::hasSession()` |
| `$I18N->msg` ()<br> `rex_translate()` | `rex_i18n::msg()` <br> `rex_i18n::translate()` |
| `rex_lang_is_utf8()` | Entfernt, da REDAXO 5 immer UTF8 verwendet |
| `rex_create_lang()` | Entfernt, da rex_i18n nun statisch ist |
| `OOAddOn::getProperty($addon, $property)` <br> `OOAddOn::isAvailable($addon)` <br> `OOPlugin::isInstalled($addon, $plugin)` etc. | `rex_addon::get($addon)->getProperty($property)` <br> `rex_addon::get($addon)->isAvailable()` <br> `rex_plugin::get($addon, $plugin)->isInstalled()` etc. |
| `rex_install_dump()` <br> `rex_organize_priorities()` | `rex_sql_util::importDump()` <br> `rex_sql_util::organizePriorities()` |
| `rex_getAttributes()` <br> `rex_setAttributes()` | In der Form entfernt, stattdessen `rex_sql::getArrayValue()` und `rex_sql::setArrayValue()` |
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

Die Methoden `setQuery()` , `insert()` , `update()` etc. liefern keine boolschen Werte mehr zurück, sondern das aktuelle rex_sql-Objekt.

| REDAXO 4 | REDAXO 5 |
| ------------- | ------------- |
| `$sql->setWhere('myid="35" OR abc="zdf"')` | `$sql->setWhere('myid = :id OR abc = :abc', array(':id' => 3, ':abc' => 'zdf'))` <br>oder<br> `$sql->setWhere(array(array('id' => 3, 'abc' => 'zdf')))` |
| `$sql->setQuery('UPDATE rex_table SET a="$i" WHERE myid="35" ')` | `$sql->setQuery('UPDATE rex_table SET a=? WHERE myid="35" ', array($i))` |
| `$sql->setQuery('SELECT * FROM rex_table WHERE col_str = "$adf" and col_int = "4"')` | `$sql->setQuery('SELECT * FROM rex_table WHERE col_str = :mystr and col_int = :myint', array(':mystr' => $adf, ':myint' => 4))` |

 Bei Fehlern wird eine `rex_sql_exception` geworfen.

<a name="fehler-rex4"></a>

### Fehlermeldung in REDAXO 4

``` php
<?php
if ($sql->update()) {
    $info = 'Success';
} else {
    $error = $sql->getError();
}
```

<a name="fehler-rex5"></a>

### Fehlermeldung in REDAXO 5

``` php
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
| `$form = rex_form::factory('table', 'legend', 'id="'.$id.'"', 'post', false, 'my_form_class');` | `$form = new my_form_class('table', 'legend', 'id="'.$id.'"', 'post', false);` <br>oder<br> `$form = my_form_class::factory('table', 'legend', 'id="'.$id.'"', 'post', false);` |

<a name="packages"></a>

## Packages (AddOns/PlugIns)

Package ist der neue gemeinsame Oberbegriff für AddOns und PlugIns.

| REDAXO 4 | REDAXO 5 |
| ------------- | ------------- |
| `(un)install.inc.php` | `(un)install.php` |
| `config.inc.php` | `package.yml` <br> `boot.php` |
| `classes/` | `lib/` <br> `vendor/` (für externe Klassen) |
| `files/` | `assets/` |
| `pages/index.inc.php` | `pages/index.php` |

Die statischen Package-Informationen, wie Version, Autor etc. sollten statt in der `boot.php` (ehemals `config.inc.php` ), in der neuen `package.yml` stehen. In dieser Datei kann auch angegeben werden, welche REDAXO-Version, welche PHP-Extensions oder welche AddOns und PlugIns benötigt werden (wird automatisch überprüft). Beispiel:

``` yaml
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

Es können aber auch weiterhin Package-Informationen in der `boot.php` gesetzt werden, aber nicht mehr über `$REX['ADDON']` , sondern über die neue Package-api. Das aktuelle Objekt ( `rex_addon` oder `rex_plugin` ) ist in den Dateien ( `boot.php` , `install.php` , `pages/index.php` etc.) über `rex_addon::get('addonkey')` erreichbar.

```php
// Beispiel boot.php
rex_addon::get('addonkey')->setProperty('author', 'Vorname Nachname');

// Beispiel install.php
$error = '';

// Überprüfungen
if($error)
  rex_addon::get('addonkey')->setProperty('installmsg', $error);
else
  rex_addon::get('addonkey')->setProperty('install', true);
```

Außer der `package.yml` sind alle Dateien ( `boot.php` , `install.php` , `uninstall.php` etc.) optional. Die `package.yml` benötigt auf jeden Fall die "package"- und "version"-Angabe.

Dadurch, dass die Dateien aus den Objekten heraus eingebunden werden, sind globale Variablen nicht mehr automatisch verfügbar.

Der Klassenordner `classes` heißt jetzt `lib` . Die Klassen in diesem Ordner (und in den Unterordnern) müssen nicht mehr manuell über `include/require` eingebunden werden, dies übernimmt das "Autoloading" bei Bedarf automatisch.

Die Sprachdateien im `lang` -Ordner werden automatisch dem Sprachkatalog hinzugefügt.

Der `files` -Ordner in der REDAXO-Root-Ebene wurde aufgeteilt, die Dateien des Medienpools liegen nun im `media` -Ordner, für die Dateien der AddOns/PlugIns gibt es den `assets` -Ordner. Dementsprechend muss der ehemalige `files` -Ordner innerhalb der Packages nun `assets` heißen.

Die `layout/top.php` und `layout/bottom.php` werden automatisch eingebunden.

Die Dateien im AddOn-, bzw. PlugIn-Ordner sollten nicht mehr verändert werden, um automatische Updates zu ermöglichen. Konfigurationswerte können über die neue `rex_config` in der Datenbank gespeichert werden (diese werden gecacht):

``` php
rex_config::set($addon, $key, $value);
$value = rex_config::get($addon, $key);

// alternativ über das Package-Objekt:
rex_addon::get($addon)->setConfig($key, $value);
$value = rex_addon::get($addon)->getConfig($key);

// oder
rex_addon::get('addonkey')->setConfig($key, $value);
$value = rex_addon::get('addonkey')->getConfig($key);
```

Des Weiteren können Daten im Ordner `redaxo/data/addons/$addonName` abgelegt werden, der Pfad ist über `rex_path::addonData($addon)` und `rex_addon::get($addon)->getDataPath()` , bzw. `rex_addon::get('addonkey')->getDataPath()` erreichbar.

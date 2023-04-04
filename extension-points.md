# Extension Points

- [Einsatz eines Extension Points](#einsatz)
  - [Beispiel für den Einsatz eines Extension Points](#beispiel)
- [Eigene Extension Points definieren](#definieren)
- [Liste der Extension Points](#liste)
  - [Core](#core)
  - [Structure](#structure)
  - [Structure Content](#structure_content)
  - [Medienpool](#medienpool)
  - [Backup](#backup)
  - [Metainfo](#metainfo)
  - [BE Style](#bestyle)
  - [Media Manager](#mediamanager)

Extension Points sind Stellen im REDAXO-Programmcode, an denen eigener Code eingeklinkt und ausgeführt werden kann. Dadurch lässt sich auch das Core-System erweitern und anpassen, ohne den Core selbst zu verändern. Extension Points ermöglichen die Manipulation eines bestimmten Wertes, der von der Funktion zurückgegeben wird, die man am Extension Point ausführen lässt. Extension Points stehen im Frontend und im Backend zur Verfügung.

Die Funktion bekommt an der Stelle der Codeausführung relevante Parameter als Übergabewerte, die sich von Extension Point zu Extension Point unterscheiden.

Im Rahmen einer REDAXOHour ist eine Video Einführung entstanden, die viele Punkte dieses Kapitels erklärt.

<a class="button-secondary" href="https://www.youtube.com/watch?v=jJP8aJ391eo">Zum Video bei YouTube</a>

<a name="einsatz"></a>

## Einsatz eines Extension Points

Zunächst sucht man sich den Extension Point, der für den eigenen Einsatz geeignet erscheint. Dann ordnet man dem Extension Point den Aufruf für die eigene Erweiterung zu. Diese Zuordnung muss an einer Stelle im Code erfolgen, an dem der Extension Point noch nicht durchlaufen wurde. Am einfachsten geschieht dies beispielsweise in der `boot.php` eines eigenen AddOns.

Beispiele:

**Aufruf einer Methode einer Klasse**

```php
rex_extension::register('SLICE_SHOW', array('myclass', 'myfunction'), rex_extension::LATE);
```

*Alternativ: Aufruf einer Funktion*

```php
rex_extension::register('SLICE_SHOW', 'myfunction', rex_extension::LATE);
```

Dies löst am Extension Point `SLICE_SHOW` die Methode `myclass::myfunction` aus.

Die Funktion, die am Extension Point aufgerufen wird, bekommt ein Objekt vom Typ `rex_extension_point` übergeben, welches ausgewertet werden kann.

Am Beispiel des Extension Point `MEDIA_UPDATED`:

```php
rex_extension::register('MEDIA_UPDATED', "meineUpdateFunction");

function meineUpdateFunction($ep) {
    # dump($ep); // auskommentieren, um alle Informationen des EP-Objekts zu erhalten
    $name = $ep->getName();
    $subject = $ep->getSubject();
    $params = $ep->getParams();
    $filename = $ep->getParam('filename');

    return $subject;
}
```

Methode | Beschreibung | Beispiel
---------- | ---------- | ----------
`getName` | Liefert den Namen des Extensionpoints | `echo $ep->getName()` ergibt z.B. "SLICE_SHOW"
`getSubject` | Liefert den Inhalt | `echo $ep->getSubject()` liefert den Inhalt des aktuellen Extensionpoints, der bearbeitet und verändert wieder zurückgegeben werden kann.
`getParams` | Liefert zusätzliche Umgebungsparameter als Array, z.B. `article_id`, `clang`, `ctype`, `module_id`, `slice_id`, `function`, `function_slice_id` | `dump($ep->getParams())`
`getParam` | Liefert einen einzelnen Wert aus params. | `echo $ep->getParam('article_id')` gibt die Artikel Id aus.

Die Registrierung eines Extension Points mit der Methode `rex_extension::register` kann mit dem Parameter `rex_extension::EARLY` (-1), `rex_extension::NORMAL` (0) oder `rex_extension::LATE` (1) aufgerufen werden. Standard ist NORMAL (0). Dadurch kann die Reihenfolge gesteuert werden, in der die Erweiterungen abgearbeitet werden.

<a name="beispiel"></a>

### Beispiel für den Einsatz eines Extension Points

Im aktuellen Beispiel soll die Sidebar im Backend bei der Artikelbearbeitung um ein Infofeld erweitert werden. Hierfür kann der Extensionpoint `STRUCTURE_CONTENT_SIDEBAR` genutzt werden.

In die Datei boot.php des AddOns kommt folgender Code:

```php
// Die Funktion wird nur im Backend aufgerufen, wenn ein User eingeloggt ist
if (rex::isBackend() && rex::getUser()) {
 // Am Extensionpoint wird die Funktion be_helper::addfield aufgerufen.
    rex_extension::register('STRUCTURE_CONTENT_SIDEBAR', ['be_helper','addfield'], rex_extension::LATE); 
}
```

> Tipp: Füge diesen Code in die boot.php des project AddOns. Das ist der richtige Ort, um eigene Erweiterungen für REDAXO abzulegen, ohne ein eigenes AddOn programmieren zu müssen.

Anschließend wird die aufzurufende Funktion  im Verzeichnis lib des AddOns z.B. in der Datei be_helper.php definiert

```php
class be_helper {
    public static function addfield($ep) {

        // den aktuellen Inhalt auslesen
        $subject = $ep->getSubject();

        // Beispielinhalt
        $text = '<p>In diesem Beispiel wird in der Sidebar des Backends ein zusätzliches Feld eingeblendet.</p>';

        // den Inhalt in einem Fragment ausgeben
        $fragment = new rex_fragment();
        $fragment->setVar('title', 'Beispiel', false);
        $fragment->setVar('body', $text, false);
        $fragment->setVar('collapse', true); // das Feld erhält eine Akkordeon-Funktion
        $fragment->setVar('collapsed', true); // das Feld ist erstmal zusammengeklappt, bei false ist es ausgeklappt
        $content = $fragment->parse('core/page/section.php');

  // Der Inhalt des Fragmentes wird an der geeigneten Stelle eingesetzt
        return preg_replace('~</section>~','</section>'.$content,$subject,1);
    }
}
```

> Tipp: Füge diesen Code in den /lib/-Ordner des project AddOns. Das ist der richtige Ort, um eigene Erweiterungen für REDAXO abzulegen, ohne ein eigenes AddOn programmieren zu müssen.

<a name="definieren"></a>

## Eigene Extension Points definieren

Im eigenen Programmcode von AddOns lassen sich eigene Extension Points setzen, die dann wiederum von anderen Entwicklern genutzt werden können.

Beispiel:

```php
$meine_var = rex_extension::registerPoint(new rex_extension_point(
    'MEIN_EXTENSION_POINT',
    $meine_var,
    [$sinnvolle, $parameter, ... ]
));
```

<a name="liste"></a>

## Liste der Extension Points

<a name="core"></a>

### Core

```
CACHE_DELETED
: Daten: rex_i18n::msg('delete_cache_message')
: Parameter: keine

CLANG_ADDED
: Daten: keine
: Parameter: ['id' => $clang->getId(), 'name' => $clang->getName(), 'clang' => $clang]

CLANG_DELETED
: Daten: keine
: Parameter: ['id' => $clang->getId(), 'name' => $clang->getName(), 'clang' => $clang]

CLANG_FORM_ADD
: Daten: keine
: Parameter: keine

CLANG_FORM_BUTTONS
: Daten: keine
: Parameter: ['id' => $clang_id, 'sql' => $sql]

CLANG_FORM_EDIT
: Daten: keine
: Parameter: ['id' => $clang_id, 'sql' => $sql]

CLANG_UPDATED
: Daten: keine
: Parameter: ['id' => $clang->getId(), 'name' => $clang->getName(), 'clang' => $clang]

COMPLEX_PERM_REMOVE_ITEM
: Daten: keine
: Parameter: ['key' => $key, 'item' => $item]

COMPLEX_PERM_REPLACE_ITEM
: Daten: keine
: Parameter: ['key' => $key, 'item' => $item, 'new' => $new]

FE_OUTPUT
: Daten: $CONTENT
: Parameter: keine

I18N_MISSING_TRANSLATION
: Daten: $msg
: Parameter: ['key' => $key, 'args' => $args]

META_NAVI
: Daten: $list_items
: Parameter: keine

OUTPUT_FILTER
: Daten: $content
: Parameter: keine

PACKAGES_INCLUDED
: Daten: keine
: Parameter: keine

PAGES_PREPARED
: Daten: rex_be_controller::getPages()
: Parameter: keine

PAGE_BODY_ATTR
: Daten: $body_attr
: Parameter: keine

PAGE_CHECKED
: Daten: $page
: Parameter: ['pages' => $pages]
: **Hinweis** der Wert ist schreibgeschützt

PAGE_HEADER
: Daten: keine
: Parameter: keine

PAGE_HEADER
: Daten: keine
: Parameter: keine

PAGE_SIDEBAR
: Daten: keine
: Parameter: keine

PAGE_TITLE
: Daten: $head
: Parameter: keine

PAGE_TITLE_SHOWN
: Daten: keine
: Parameter: keine

RESPONSE_SHUTDOWN
: Daten: $content
: Parameter: []

REX_FORM_CONTROL_FIELDS
: Daten: $controlFields
: Parameter: ['form' => $this]

REX_FORM_DELETED
: Daten: $deleted
: Parameter: ['form' => $this, 'sql' => $deleteSql]

REX_FORM_GET
: Daten: $this
: Parameter: []

REX_FORM_INPUT_ATTRIBUTES
: Daten: []
: Parameter: ['inputType' => $inputType]

REX_FORM_INPUT_CLASS
: Daten: keine
: Parameter: ['inputType' => $inputType]

REX_FORM_INPUT_TAG
: Daten: keine
: Parameter: ['inputType' => $inputType]

REX_FORM_SAVED
: Daten: $saved
: Parameter: ['form' => $this, 'sql' => $sql]

REX_LIST_GET
: Daten: $this
: Parameter: []

```

<a name="structure"></a>

### Structure

```
ART_ADDED
: Daten: $message
: Parameter: ['id' => $id, 'clang' => $key, 'status' => 0, 'name' => $data['name'], 'parent_id' => $data['category_id'], 'priority' => $data['priority'], 'path' => $path, 'template_id' => $data['template_id'], 'data' => $data]

ART_DELETED
: Daten: $message
: Parameter: ['id' => $article_id, 'clang' => $clang, 'parent_id' => $parent_id, 'name' => $Art->getValue('name'), 'status' => $Art->getValue('status'), 'priority' => $Art->getValue('priority'), 'path' => $Art->getValue('path'), 'template_id' => $Art->getValue('template_id')]

ART_IS_PERMITTED
: Daten: true
: Parameter: ['element' => $this]

ART_PRE_DELETED
: Daten: $message
: Parameter: ['id' => $id, 'parent_id' => $parent_id, 'name' => $ART->getValue('name'), 'status' => $ART->getValue('status'), 'priority' => $ART->getValue('priority'), 'path' => $ART->getValue('path'), 'template_id' => $ART->getValue('template_id')]

ART_STATUS
: Daten: null
: Parameter: ['id' => $article_id, 'clang' => $clang, 'status' => $newstatus]

ART_STATUS_TYPES
: Daten: $artStatusTypes
: Parameter: keine

ART_TO_CAT
: Daten: keine
: Parameter: ['id' => $art_id, 'clang' => $clang]

ART_TO_STARTARTICLE
: Daten: keine
: Parameter: ['id' => $neu_id, 'id_old' => $alt_id, 'clang' => $clang]

ART_UPDATED
: Daten: $message
: Parameter: ['id' => $article_id, 'article' => clone $EA, 'article_old' => clone $thisArt, 'status' => $thisArt->getValue('status'), 'name' => $data['name'], 'clang' => $clang, 'parent_id' => $data['category_id'], 'priority' => $data['priority'], 'path' => $data['path'], 'template_id' => $data['template_id'], 'data' => $data]

CAT_ADDED
: Daten: $message
: Parameter: ['category' => clone $AART, 'id' => $id, 'parent_id' => $category_id, 'clang' => $key, 'name' => $data['catname'], 'priority' => $data['catpriority'], 'path' => $path, 'status' => $data['status'], 'article' => clone $AART, 'data' => $data]

CAT_DELETED
: Daten: $message
: Parameter: ['id' => $category_id, 'parent_id' => $parent_id, 'clang' => $_clang, 'name' => $row->getValue('catname'), 'priority' => $row->getValue('catpriority'), 'path' => $row->getValue('path'), 'status' => $row->getValue('status')]

CAT_FORM_ADD
: Daten: keine
: Parameter: ['id' => $category_id, 'clang' => $clang, 'data_colspan' => ($data_colspan + 1)]

CAT_FORM_BUTTONS
: Daten: keine
: Parameter: ['id' => $category_id, 'clang' => $clang]

CAT_FORM_EDIT
: Daten: keine
: Parameter: ['id' => $edit_id, 'clang' => $clang, 'category' => $KAT, 'catname' => $KAT->getValue('catname'), 'catpriority' => $KAT->getValue('catpriority'), 'data_colspan' => ($data_colspan + 1)]

CAT_IS_PERMITTED
: Daten: true
: Parameter: ['element' => $this]

CAT_STATUS
: Daten: null
: Parameter: ['id' => $category_id, 'clang' => $clang, 'status' => $newstatus]

CAT_STATUS_TYPES
: Daten: $catStatusTypes
: Parameter: keine

CAT_TO_ART
: Daten: keine
: Parameter: ['id' => $art_id, 'clang' => $clang]

CAT_UPDATED
: Daten: $message
: Parameter: ['id' => $category_id, 'category' => clone $EKAT, 'category_old' => clone $thisCat, 'article' => clone $EKAT, 'parent_id' => $thisCat->getValue('parent_id'), 'clang' => $clang, 'name' => isset($data['catname']) ? $data['catname'] : $thisCat->getValue('catname'), 'priority' => isset($data['catpriority']) ? $data['catpriority'] : $thisCat->getValue('catpriority'), 'path' => $thisCat->getValue('path'), 'status' => $thisCat->getValue('status'), 'data' => $data]

PAGE_STRUCTURE_HEADER
: Daten: keine
: Parameter: ['category_id' => $category_id, 'clang' => $clang]

PAGE_STRUCTURE_HEADER_PRE
: Daten: keine
: Parameter: ['context' => $context]

URL_REWRITE
: Daten: keine
: Parameter: ['id' => $id, 'clang' => $clang, 'params' => $params, 'separator' => $separator]
```

<a name="structure_content"></a>

### Structure Content

```
ART_CONTENT
: Daten: $CONTENT
: Parameter: ['ctype' => $curctype, 'article' => $this]

ART_INIT
: Daten: keine
: Parameter: ['article' => $this, 'article_id' => $article_id, 'clang' => $this->clang]

ART_SLICES_COPY
: Daten: keine
: Parameter: ['article_id' => $to_id, 'clang_id' => $to_clang, 'slice_revision' => $revision]

ART_SLICES_QUERY
: Daten: $query
: Parameter: ['article' => $this]

GENERATE_FILTER
: Daten: $article_content
: Parameter: ['id' => $article_id, 'clang' => $_clang, 'article' => $CONT]

SLICE_ADD
: Daten: keine
: Parameter: ['article_id' => $article_id, 'clang_id' => $clang, 'slice_revision' => $slice_revision]

SLICE_ADDED
: Daten: $info
: Parameter: $epParams

SLICE_DELETE
: Daten: keine
: Parameter: ['slice_id' => $slice_id, 'article_id' => $curr->getValue('article_id'), 'clang_id' => $curr->getValue('clang_id'), 'slice_revision' => $curr->getValue('revision')]

SLICE_DELETED
: Daten: $global_info
: Parameter: $epParams

SLICE_MOVE
: Daten: keine
: Parameter: ['direction' => $direction, 'slice_id' => $slice_id, 'article_id' => $article_id, 'clang_id' => $clang, 'slice_revision' => $slice_revision]

SLICE_OUTPUT
: Daten: $artDataSql->getValue(rex::getTablePrefix() . 'module.output')
: Parameter: ['article_id' => $this->article_id, 'clang' => $this->clang, 'slice_data' => $artDataSql]

SLICE_SHOW
: Daten: $slice_content
: Parameter: ['article_id' => $this->article_id, 'clang' => $this->clang, 'ctype' => $sliceCtypeId, 'module_id' => $sliceModuleId, 'slice_id' => $sliceId, 'function' => $this->function, 'function_slice_id' => $this->slice_id]

SLICE_UPDATE
: Daten: keine
: Parameter: ['slice_id' => $slice_id, 'article_id' => $article_id, 'clang_id' => $clang, 'slice_revision' => $slice_revision]

SLICE_UPDATED
: Daten: $info
: Parameter: $epParams

STRUCTURE_CONTENT_AFTER_SLICES
: Daten: keine
: Parameter: ['article_id' => $article_id, 'clang' => $clang, 'function' => $function, 'slice_id' => $slice_id, 'page' => rex_be_controller::getCurrentPage(), 'ctype' => $ctype, 'category_id' => $category_id, 'article_revision' => &$article_revision, 'slice_revision' => &$slice_revision]

STRUCTURE_CONTENT_ARTICLE_UPDATED
: Daten: keine
: Parameter: ['id' => $article_id, 'clang' => $clang]

STRUCTURE_CONTENT_BEFORE_SLICES
: Daten: keine
: Parameter: ['article_id' => $article_id, 'clang' => $clang, 'function' => $function, 'slice_id' => $slice_id, 'page' => rex_be_controller::getCurrentPage(), 'ctype' => $ctype, 'category_id' => $category_id, 'article_revision' => &$article_revision, 'slice_revision' => &$slice_revision]

STRUCTURE_CONTENT_HEADER
: Daten: keine
: Parameter: ['article_id' => $article_id, 'clang' => $clang, 'function' => $function, 'slice_id' => $slice_id, 'page' => rex_be_controller::getCurrentPage(), 'ctype' => $ctype, 'category_id' => $category_id, 'article_revision' => &$article_revision, 'slice_revision' => &$slice_revision]

STRUCTURE_CONTENT_MODULE_SELECT
: Daten: $select
: Parameter: ['page' => rex_be_controller::getCurrentPage(), 'article_id' => $this->article_id, 'clang' => $this->clang, 'ctype' => $this->ctype, 'slice_id' => $sliceId]

STRUCTURE_CONTENT_SIDEBAR
: Daten: keine
: Parameter: ['article_id' => $article_id, 'clang' => $clang, 'function' => $function, 'slice_id' => $slice_id, 'page' => rex_be_controller::getCurrentPage(), 'ctype' => $ctype, 'category_id' => $category_id, 'article_revision' => &$article_revision, 'slice_revision' => &$slice_revision]

STRUCTURE_CONTENT_SLICE_ADDED
: Daten: $info
: Parameter: $epParams

STRUCTURE_CONTENT_SLICE_DELETED
: Daten: $global_info
: Parameter: $epParams

STRUCTURE_CONTENT_SLICE_MENU
: Daten: $menu_items_ep
: Parameter: ['article_id' => $this->article_id, 'clang' => $this->clang, 'ctype' => $sliceCtype, 'module_id' => $moduleId, 'slice_id' => $sliceId, 'perm' => rex::getUser()->getComplexPerm('modules')->hasPerm($moduleId)]

STRUCTURE_CONTENT_SLICE_UPDATED
: Daten: $info
: Parameter: $epParams

```

<a name="medienpool"></a>

### Medienpool

```
MEDIA_ADD
: Daten: $ERROR_MSG
: Parameter: ['file' => $FILE, 'title' => $FILEINFOS['title'], 'filename' => $NFILENAME, 'old_filename' => $FILENAME, 'is_upload' => $isFileUpload 'category_id' => $rex_file_category, 'type' => $FILETYPE]

MEDIA_ADDED
: Daten: keine
: Parameter: $RETURN

MEDIA_DELETED
: Daten: keine
: Parameter: ['filename' => $filename]

MEDIA_FORM_ADD
: Daten: keine
: Parameter: keine

MEDIA_FORM_EDIT
: Daten: keine
: Parameter: ['id' => $file_id, 'media' => $gf]

MEDIA_IS_IN_USE
: Daten: $warning
: Parameter: ['filename' => $filename]

MEDIA_IS_PERMITTED
: Daten: true
: Parameter: ['element' => $this]

MEDIA_LIST_FUNCTIONS
: Daten: $opener_link
: Parameter: ['file_id' => $files->getValue('id'), 'file_name' => $files->getValue('filename'), 'file_oname' => $files->getValue('originalname'), 'file_title' => $files->getValue('title'), 'file_type' => $files->getValue('filetype'), 'file_size' => $files->getValue('filesize'), 'file_stamp' => $files->getDateTimeValue('updatedate'), 'file_updateuser' => $files->getValue('updateuser')]

MEDIA_LIST_QUERY
: Daten: $qry
: Parameter: ['category_id' => $rex_file_category]

MEDIA_LIST_TOOLBAR
: Daten: $toolbar
: Parameter: ['subpage' => $subpage, 'category_id' => $rex_file_category]

MEDIA_TOIMAGE
: Daten: keine
: Parameter: ['filename' => &$filename, 'params' => &$params]

MEDIA_UPDATED
: Daten: keine
: Parameter: $return

MEDIA_URL_REWRITE
: Daten: keine
: Parameter: ['media' => $this]

PAGE_MEDIAPOOL_HEADER
: Daten: keine
: Parameter: ['subpage' => $subpage, 'category_id' => $rex_file_category]

```

<a name="backup"></a>

### Backup

```
BACKUP_AFTER_DB_EXPORT
: Daten: $content
: Parameter: keine

BACKUP_AFTER_DB_IMPORT
: Daten: $msg
: Parameter: ['content' => $conts, 'filename' => $filename, 'filesize' => $filesize]

BACKUP_AFTER_FILE_EXPORT
: Daten: $tar
: Parameter: keine

BACKUP_AFTER_FILE_IMPORT
: Daten: $tar
: Parameter: keine

BACKUP_BEFORE_DB_EXPORT
: Daten: keine
: Parameter: keine

BACKUP_BEFORE_DB_IMPORT
: Daten: $msg
: Parameter: ['content' => $conts, 'filename' => $filename, 'filesize' => $filesize]

BACKUP_BEFORE_FILE_EXPORT
: Daten: $tar
: Parameter: keine

BACKUP_BEFORE_FILE_IMPORT
: Daten: $tar
: Parameter: keine

```

<a name="metainfo"></a>

### Metainfo

```
ART_META_UPDATED
: Daten: keine
: Parameter: $params

METAINFO_CUSTOM_FIELD
: Daten: [$field, $tag, $tag_attr, $id, $label, $labelIt, 'values' => $dbvalues, 'rawvalues' => $dbvalues, 'type' => $typeLabel, 'sql' => $sqlFields]
: Parameter: keine

METAINFO_TYPE_FIELDS
: Daten: [REX_METAINFO_FIELD_SELECT, REX_METAINFO_FIELD_RADIO, REX_METAINFO_FIELD_CHECKBOX, REX_METAINFO_FIELD_REX_MEDIA_WIDGET, REX_METAINFO_FIELD_REX_MEDIALIST_WIDGET, REX_METAINFO_FIELD_REX_LINK_WIDGET, REX_METAINFO_FIELD_REX_LINKLIST_WIDGET]
: Parameter: keine

```

<a name="bestyle"></a>

### BE Style

```
BE_STYLE_PAGE_CONTENT
: Daten: keine
: Parameter: []

BE_STYLE_SCSS_FILES
: Daten: [$this->getPath('scss/master.scss')]
: Parameter: keine
```

<a name="mediamanager"></a>

### Media Manager

```
MEDIA_MANAGER_FILTERSET
: Daten: $set
: Parameter: ['rex_media_type' => $type]

```

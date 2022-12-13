# File-Handling

- [Einleitung](#einleitung)
- [rex_file](#rexfile)
  - [get](#rexfile_get)
  - [getConfig](#rexfile_getConfig)
  - [getCache](#rexfile_getCache)
  - [put](#rexfile_put)
  - [putConfig](#rexfile_putConfig)
  - [putCache](#rexfile_putCache)
  - [copy](#rexfile_copy)
  - [move](#rexfile_move)
  - [delete](#rexfile_delete)
  - [extension](#rexfile_extension)
  - [mimeType](#rexfile_mimeType)
  - [formattedSize](#rexfile_formattedSize)
  - [getOutput](#rexfile_getOutput)
- [rex_dir](#dir)
  - [create](#create)
  - [isWritable](#isWritable)
  - [copy](#copy)
  - [delete](#delete)
  - [deleteFiles](#deleteFiles)

<a name="Einleitung"></a>

## Einleitung

Für die Erstellung und Pflege von Dateien und Verzeichnissen stehen die PHP-Classes `rex_file` und `rex_dir` zur Verfügung. Nachfolgend werden die Aufgaben der darin enthaltenen Methoden gelistet.

In den Methoden müsen korrekte Pfade angegeben werden. Im Kapitel [Pfade (rex_path, rex_url)](/{{path}}/{{version}}/pfade) finden sich dazu alle erforderlichen Informationen.

<a name="rexfile"></a>

## rex_file

Die Class `rex_file` kümmert sich um das Handling einzelner Dateien. Hier stehen Methoden zum Einlesen, Schreiben und zur Ausgabe von Dateien aus und im Dateisystem zur Verfügung.

[Quellcode auf GitHub](https://github.com/redaxo/redaxo/blob/main/redaxo/src/core/lib/util/file.php)  

<a name="rexfile_get"></a>

### rex_file::get

Mit der Methode `get` wird eine Datei aus dem Dateisystem eingelesen. Ein weiterer Parameter erlaubt die Ausgabe eines Default-Wertes bzw. Fehlermedlung, wenn die Datei nicht gelesen werden kann (default: NULL).  

```php
rex_file::get($file, $default = null);
```

Beispiel:

```php
$data = rex_file::get(rex_path::frontend('/assets/styles.css'),'not available');
```

<a name="rexfile_getConfig"></a>

### rex_file::getConfig

Mit der Methode `getConfig` kann eine Config-Datei eingelesen werden. Kann die Datei nicht gelesen werden, kann ein Default-Wert zurückgegeben werden (default: NULL).  

> Diese Methode wird hauptsächlich vom Core verwendet. AddOns sollten auf die Möglichkeiten der package.yml, Properties und rex_config zurückgreifen.

```php
rex_file::getConfig($file, $default = []);
```

Beispiel: Einlesen der REDAXO Config

```php
$config = rex_file::getConfig('config.yml');
```

### rex_file::getCache

<a name="rexfile_getCache"></a>

Mit der Methode `getCache` wird eine Datei aus dem Cache eingelesen. Ein weiterer Parameter erlaubt die Ausgabe eines Default-Wertes bzw. Fehlermedlung (wenn nicht festgelegt NULL), wenn die Datei nicht gelesen werden kann.  

```php
rex_file::getCache($file, $default = []);
```

Beispiel:

```php
echo (rex_file::getCache(rex_path::addonCache('meinaddon').'blindtext.txt'));
```

### rex_file::put

<a name="rexfile_put"></a>

Die Methode `put` schreibt Content in eine Datei. Existiert die Datei noch nicht, wird sie erstellt. Die Rückgabe bei Erfolg ist TRUE, sonst FALSE. Vorhandene Inhalte der Datei werden überschrieben.  

```php
rex_file::put($file, $content);
```

Beispiel:

```php
$css = 'body { background: #eee;}
p { line-height: 1.2em;}
';
$success = rex_file::put(rex_path::frontend('/assets/new_styles.css'),$css);
```

### rex_file::putConfig

<a name="rexfile_putConfig"></a>

Die Methode `putConfig` schreibt Konfigurationsdaten in eine Config-Datei. Die Rückgabe bei Erfolg ist TRUE, sonst FALSE.

> Diese Methode wird hauptsächlich vom Core verwendet. AddOns sollten auf die Möglichkeiten der package.yml, Properties und rex_config zurückgreifen.

```php
rex_file::putConfig($file, $content);
```

### rex_file::putCache

<a name="rexfile_putCache"></a>

Die Methode `putCache` schreibt Daten in den Cache. Bei Erfolg TRUE, sonst FALSE.

```php
rex_file::putCache($file, $content);
```

Beispiel:

```php
$content = '
Dies ist ein Typoblindtext. An ihm kann man sehen, ob alle Buchstaben da sind und wie sie aussehen.
';
rex_file::putCache(rex_path::addonCache('meinaddon').'blindtext.txt',$content);
```

Der gecachte Inhalt kann dann mit `getCache` abgerufen werden:

```php
echo (rex_file::getCache(rex_path::addonCache('meinaddon').'blindtext.txt'));
```

<a name="rexfile_copy"></a>

### rex_file::copy

Die Methode `copy` ermöglicht das Kopieren einer einer Datei zu einem Verzeichnis oder Datei. Es müssen eine Quell- und ein Zielpfad eingegeben werden. Die Rückgabe bei Erfolg ist TRUE, sonst FALSE.

```php
rex_file::copy($srcfile, $dstfile);
```

<a name="rexfile_move"></a>

### rex_file::move

Die Methode `move` ermöglicht das Verschieben oder Umbenennen einer Datei. Es müssen ein Quell- und ein Zielpfad angegeben werden. Die Rückgabe bei Erfolg ist TRUE, sonst FALSE.

```php
rex_file::move($srcfile, $dstfile);
```

<a name="rexfile_delete"></a>

### rex_file::delete

Die Methode `delete` ermöglicht das Löschen einer einer Datei. Die Rückgabe bei Erfolg ist TRUE, sonst FALSE.

```php
rex_file::delete($file);
```

<a name="rexfile_extension"></a>

### rex_file::extension

Die Methode `extension` liefert als Rückgabe die Dateiendung einer Datei.

```php
rex_file::extension($file);
```

<a name="rexfile_mimeType"></a>

### rex_file::mimeType

Die Methode `mimeType` liefert den MimeType einer Datei.

```php
$extension = rex_file::mimeType($file);
```

z.B.:

- application/javascript
- image/svg+xml
- video/mpeg

<a name="rexfile_formattedSize"></a>

### rex_file::formattedSize

Die Methode `formattedSize` liefert eine benutzerfreundliche Ausgabe der Dateigröße einer Datei

```php
$filesize = rex_file::formattedSize($file);
```

<a name="rexfile_getOutput"></a>

### rex_file::getOutput

`getOutput` führt die angegebene Datei aus und gibt das Ergebnis aus.

```php
rex_file::getOutput($file);
```

<a name="rexdir"></a>

## rex_dir

Die Class `rex_dir` kümmert sich um das Handling von Verzeichnissen. Hier stehen Methoden zum Erstellen, Kopieren und Löschen von Verzeichnissen zur Verfügung.

[Quellcode auf GitHub](https://github.com/redaxo/redaxo/blob/main/redaxo/src/core/lib/util/dir.php)  

<a name="create"></a>

### rex_dir::create

`create` erstellt ein bzw. mehrere Verzeichnisse. Ist der Parameter $recursive auf true gestellt (Standard), wird der komplette Pfad inkl. angegebener Unterverzeichnisse erstellt. Bei false, müssen die angegebenen Unterverzeichnisse bereits bestehen. Rückgabe bei Erfolg ist TRUE, sonst FALSE.  

```php
rex_dir::create($dir, $recursive = true);
```

<a name="isWritable"></a>

### rex_dir::isWritable

`isWritable` prüft ob Schreibrechte für das Verzeichnis bestehen. Rückgabe bei Erfolg ist TRUE, sonst FALSE.  

```php
rex_dir::isWritable($dir);
```

<a name="copy"></a>

### rex_dir::copy

`copy` kopiert ein Verzeichnis zum angegebenen Ziel. Rückgabe bei Erfolg ist TRUE, sonst FALSE.

```php
rex_dir::copy($srcdir, $dstdir);
```

<a name="delete"></a>

### rex_dir::delete

`delete` löscht ein Verzeichnis rekursiv. Wird `$deleteSelf` auf `false` gesetzt werden nur die Unterverzeichnisse gelöscht.   Rückgabe bei Erfolg ist TRUE, sonst FALSE.

```php
rex_dir::delete($dir, $deleteSelf = true);
```

<a name="deleteFiles"></a>

### rex_dir::deleteFiles

`deleteFiles` löscht alle Deteien im angegeben Verzeichnis und der Unterverzeichnisse. Wird `$recursive` auf `false` gesetzt werden die Dateien der Unterverzeichnisse nicht gelöscht. Rückgabe bei Erfolg ist TRUE, sonst FALSE.

```php
rex_dir::deleteFiles($dir, $recursive = true);
```

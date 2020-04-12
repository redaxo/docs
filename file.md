# File-Handling

- [Einführung](#einfuehrung)
- [rex_file](#rexfile)
  - [get](#rexfile_get)
  - [getConfig](#rexfile_getConfig)
  - [getCache](#rexfile_getCache)
  - [put](#rexfile_put)
  - [putConfig](#rexfile_putConfig) 
  - [putCache](#rexfile_putCache)
  - [copy](#rexfile_copy) 
  - [rename](#rexfile_rename) 
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
  - [deleteIterator](#deleteIterator)
  
<a name="rexfile_get"></a>
## rex_file::get
Mit der Methode `get` wird eine Datei aus dem Dateisystem eingelesen. Ein weiterer Parameter erlaubt die Ausgabe eines Default-Wertes bzw. Fehlermedlung (wenn nicht festgelegt NULL), wenn die Datei nicht gelesen werden kann.  

```php
rex_file::get($file, $default = null)
```

Beispiel: 

```php
$data = rex_file::get(rex_path::frontend('/assets/styles.css'),'not available');
```


<a name="rexfile_getFonfig"></a>
## rex_file::getConfig

Mit der Methode `getConfig` kann eine Config-Datei eingelesen werden. Kann die Datei nicht gelesen werden, kann ein Default-Wert zurückgegeben werden.  

> Die Methode wird hauptsächlich vom Core verwendet. AddOns sollten auf die Möglichkeiten der package.yml und rex_config zurückgreifen. 

```php 
getConfig($file, $default = [])
```

Beispiel: Einlesen der REDAXO Config

```php
$config = rex_path::coreData('config.yml');
```

## rex_file::getCache
<a name="#rexfile_getCache"></a>

Mit der Methode `getCache` wird eine Datei aus dem Cache eingelesen. Ein weiterer Parameter erlaubt die Ausgabe eines Default-Wertes bzw. Fehlermedlung (wenn nicht festgelegt NULL), wenn die Datei nicht gelesen werden kann.  

```php
getCache($file, $default = [])
```


## rex_file::put
<a name="#rexfile_put"></a>

Mit der Methode `put` schreibt Content in eine Datei. Existiert die Datei noch nicht, wird sie erstellt. Rückgabe bei Erfolg: `true`, sonst `false`. Vorhandene Inhalte der Datei werden überschriben.  

```php
put($file, $content)
```

Beispiel: 

```php
$css = 'body { background: #eee;}
p { line-height: 1.2em;}
';
$success = rex_file::put(rex_path::frontend('/assets/new_styles.css'),$css)
```




## rex_file::putConfig
<a name="#rexfile_putConfig"></a>

Die Methode `putConfig` schreibt Konfigurationsdaten in eine Config-Dateit. 

> Die Methode wird hauptsächlich vom Core verwendet. AddOns sollten auf die Möglichkeiten der package.yml und rex_config zurückgreifen. 

```php
putConfig($file, $content)
```



## rex_file::putCache
<a name="#rexfile_putCache"></a>

Die Methode `putCache` schreibt Daten in den Cache

```php
putCache($file, $content)
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

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
$data = rex_file::get(rex_path::frontend('/assets/styles.css'),'not awailable');
```





# Assets

## Speicherort

Assets werden in REDAXO im /assets-Ordner des AddOn abgelegt. Bei Installation, Reinstallation und Update ein Addon, werden die Dateien aus `assets` in den öffentlich zugänglichen Ornder `ROOT/assets/addons/addonname/` kopiert. 

> Werden Anderungen an den Dateien durchgeführt, muss ein neuer Kopiervorgang per Reinstallation angestoßen werden.  

## Dateien einbinden

Auf die Dateien eines Addons zeigt die Variable `$this` über die Class [rex_addon](http://www.redaxo.org/docs/master/class-rex_addon.html).

Dateien können in der Datei `boot.php` eingebunden werden. Hierfür lifert die Class [rex_view](http://www.redaxo.org/docs/master/class-rex_view.html) die Methoden `addCssFile` und `addJsFile`.

```
//CSS-Datei einbinden
rex_view::addCssFile( /*Pfad zur Datei*/ );

//JS-Datei einbinden
rex_view::addJSFile( /*Pfad zur Datei*/ );
```
Da die assets nach der Addon-Installation im asset-Verzeichnis gespeichert werden, kann man den Pfad ganz einfach mit folgender Funktion ausgeben:

```
$this->getAssetsUrl('styles.css') // wird zu /assets/addons/addonname/styles.css

rex_view::addCssFile( $this->getAssetsUrl('styles.css') );
rex_view::addJsFile( $this->getAssetsUrl('script.js') );
```

## Sass

Es ist mäglich `.scss` Dateien zu kompilieren. … 



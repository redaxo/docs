# Assets

Assets sind statische Dateien, wie CSS-Files, Javascripte, Fonts oder Bilder die öffentlich zugänglich für den Browser sein müssen. Hierzu gehören auch CSS und Javascripte für Editoren und für die Frontendausgabe oder Modifikationen für das Backend.   

## Speicherort

Assets werden in REDAXO im `assets`-Ordner des AddOn abgelegt. Bei Installation, Reinstallation und Update eines AddOn, werden die Dateien aus `assets` in den öffentlich zugänglichen Ornder `ROOT/assets/addons/addonname/` kopiert. 

> Werden während der Entwicklung Änderungen an den Dateien durchgeführt, muss ein neuer Kopiervorgang per Reinstallation angestoßen werden.   

## Dateien einbinden

Auf die Dateien eines Addons zeigt die Variable `$this` über die Class [rex_addon](http://www.redaxo.org/docs/master/class-rex_addon.html).

Die Dateien können in der Datei `boot.php` eingebunden werden. Hierfür liefert die Class [rex_view](http://www.redaxo.org/docs/master/class-rex_view.html) die Methoden `addCssFile` und `addJsFile`.

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

Es ist mäglich `.scss` Dateien mit der Class `rex_scss_compiler()` zu kompilieren. Für solche Dateien bietet sich an, diese in einem separaten Ordner anzulegen und diese in den assets-ordner beim kompilieren abzulegen. Kompilierte Versionen der Dateien sollten bei Bereitstellung des AddOns bereis im Assets-Ordner vorliegen. Die scss-Dateien sollten nur für Anpaasungen oder Fehlerbehebungen durch REDAXO neu kompiliert werden. 

Der nachfolgend kommentierte Code für die `boot.php` zeigt, wie man die Kompilierung bei aktiviertem DEBUG-Mode ausführt. 

```php
// Befinden wir uns im Backend und ist ein User angemeldet?
if (rex::isBackend() && rex::getUser())
    {
        // Prüft ob der DebugMode in System aktiviert ist und ein Request erfolgte
        if (rex::isDebugMode() && rex_request_method() == 'get')
        {
            // compiler
            $compiler = new rex_scss_compiler();
            // Haptverzeichnis des AddOn
            $compiler->setRootDir($this->getPath());
            // Festlegen des SCSS-Files
            $compiler->setScssFile($this->getPath('scss/meinestile.scss'));
            // Kompilierung starten
            $compiler->compile();
            // kopiere das kompilierte css in den öffentlichen assets-Ordner
            rex_file::copy($this->getPath('assets/uploader.css'), $this->getAssetsPath('meinestile.css'));
        }

```

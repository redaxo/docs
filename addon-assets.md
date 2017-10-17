# Assets

- [Über](#plugin)
- [Speicherort](#speicherort)
- [Dateien einbinden](#einbinden)
- [Sass](#sass)

<a name="ueber"></a>
## Über 

Assets sind statische Dateien, wie CSS-Files, Javascripte, Fonts oder Bilder die öffentlich zugänglich für den Browser sein müssen. Hierzu gehören u.a. auch CSS und Javascripte für Editoren im Backend, Dateien für die Frontendausgabe oder Modifikationen für das Backend.   

<a name="speicherort"></a>
## Speicherort

Assets werden in REDAXO im `assets`-Ordner des AddOn abgelegt. Bei Installation, Reinstallation und Update eines AddOn, werden die Dateien aus `assets` in den öffentlich zugänglichen Ordner `/assets/addons/addonname/` kopiert. 

> Werden während der Entwicklung Änderungen an den Dateien durchgeführt, muss ein neuer Kopiervorgang per Reinstallation angestoßen werden.   

<a name="einbinden"></a>
## Dateien einbinden

Auf die Dateien eines Addons zeigt die Variable `$this` über die Class [rex_addon](http://www.redaxo.org/docs/master/class-rex_addon.html).

Die Dateien können in der Datei `boot.php` eingebunden werden. Hierfür liefert die Class [rex_view](http://www.redaxo.org/docs/master/class-rex_view.html) die Methoden `addCssFile` und `addJsFile`.

```php
//CSS-Datei einbinden
rex_view::addCssFile( /*Pfad zur Datei*/ );

//JS-Datei einbinden
rex_view::addJSFile( /*Pfad zur Datei*/ );
```
Den Pfad zu den Dateien erhält man per `getAssetsUrl`.

```php
$this->getAssetsUrl('styles.css') // wird zu /assets/addons/addonname/styles.css
```

Beispiel:

```php
rex_view::addCssFile( $this->getAssetsUrl('styles.css') );
rex_view::addJsFile( $this->getAssetsUrl('script.js') );
```

<a name="sass"></a>
## Sass

Es ist möglich `.scss` Dateien mit der Class `rex_scss_compiler()` zu kompilieren. Für solche Dateien bietet sich an, diese in einem separaten Ordner anzulegen. Kompilierte Versionen der Dateien sollten bei Bereitstellung des AddOns bereis im Assets-Ordner vorliegen. Die scss-Dateien sollten nur für Anpassungen oder Fehlerbehebungen durch REDAXO neu kompiliert werden. 

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
            // Wohin soll die kompilierte Version erstellt werden?
            $compiler->setCssFile($this->getPath('assets/meinestile.css'));
            // Kompilierung starten
            $compiler->compile();
            // kopiere das kompilierte css in den öffentlichen assets-Ordner
            rex_file::copy($this->getPath('assets/meinestile.css'), $this->getAssetsPath('meinestile.css'));
        }
    }
```

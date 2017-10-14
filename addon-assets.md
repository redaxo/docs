# Assets

In den Dateien eines Addons zeigt die Variable `$this` auf die Klasse [rex_addon](http://www.redaxo.org/docs/master/class-rex_addon.html).

## Speicherort

Assets werden in R5 neu in das assets-Verzeichnis im Addon selbst abgelegt. Ältere Redaxo-Versionen nutzten dafür das Verzeichnis `files`. Wird ein Addon über den Addon-Manager installiert bzw. reinstalliert, werden die Dateien aus `assets` in `ROOT/assets/addons/addonname/` gespeichert.

## Dateien einbinden

Dateien können in der Datei `boot.php` hinzugefügt werden. Dazu verwenden wir die Klasse [rex_view](http://www.redaxo.org/docs/master/class-rex_view.html) und die Methoden `addCssFile` und `addJsFile`.

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

## CSS, Less, Sass

Im Backend ist es möglich `.scss` Dateien zu speichern und einmalig zu kompilieren. Das Addon `be_style` lädt hierzu die nötige [Sass-Library](https://github.com/leafo/scssphp). Da der Compiler enorm Performance benötigt, ist es ratsam die Dateien nur einmalig zu passen und Sass dann zu deaktivieren.

Um eine Datei an den Sass-Parser zu übergeben bietet `be_style` den extension point [BE_STYLE_SCSS_FILES](http://book.redaxo.org/5.0/advanced/create_addon/extension_points/BE_STYLE_SCSS_FILES.html)

Mit dem Addon [assets](https://github.com/factorylabs/redaxo_assets) wird es zusätzlich möglich, Sass-, Less- und normale CSS-Dateien für das Backend und Frontend zu parsen. Dafür bietet das Addon die extension points `BE_ASSETS` und `FE_ASSETS`.

# Assets

* [Über](#plugin)
* [Speicherort](#speicherort)
* [Dateien einbinden](#einbinden)
  + [Assets nur dort einbinden wo gebraucht](#sparsam)
  + [Cachebuster](#buster)
  + [Javascripte / JS_IMMUTABLE, Async, JS_DEFERED](#javascripte)
* [Javascript im Backend / rex:ready](#rexready)
* [PHP-Werte an Javascript übergeben](#phpJs)
* [Sass](#sass)
* [Backend-Themes](#themes)

<a name="ueber"></a>

## Über Asssets

Als Assets bezeichnet man statische Dateien wie CSS-Files, Javascripte, Fonts oder Bilder, die für den Browser öffentlich zugänglich sein müssen. Hierzu gehören u.a. auch CSS und Javascripte für Editoren im Backend, Dateien für die Frontendausgabe oder Modifikationen für das Backend.

<a name="speicherort"></a>

## Speicherort

Assets werden innerhalb von REDAXO im `assets` -Ordner des AddOns abgelegt. Eine Installation, Reinstallation und Update eines AddOns kopiert die Dateien aus `assets` in den öffentlich zugänglichen Ordner `/assets/addons/addonname/` .

> Werden während der Entwicklung Änderungen an den Dateien innerhalb des AddOn-Ordners durchgeführt, muss ein neuer Kopiervorgang per Reinstallation angestoßen werden.

<a name="einbinden"></a>

## Dateien einbinden

Auf die Dateien eines AddOns oder PlugIns zeigt das jeweilige Package-Objekt der Klassen [rex_addon](https://friendsofredaxo.github.io/phpdoc/classes/rex-addon.html) oder [rex_plugin](https://friendsofredaxo.github.io/phpdoc/classes/rex-plugin.html).

Die Dateien können in der Datei `boot.php` eingebunden werden. Hierfür liefert die Klasse [ `rex_view` ](https://friendsofredaxo.github.io/phpdoc/classes/rex-view.html) die Methoden `addCssFile` und `addJsFile` .

``` php
//CSS-Datei einbinden
rex_view::addCssFile( /*Pfad zur Datei*/ );

//JS-Datei einbinden
rex_view::addJSFile( /*Pfad zur Datei*/ );
```

Den Pfad zu den Dateien erhält man per `getAssetsUrl` .

``` php
rex_addon::get('mein_addonkey')->setConfig($key, $value);
rex_addon::get('mein_addonkey')->getAssetsUrl('styles.css') // wird zu /assets/addons/addonname/styles.css
```

Beispiel:

``` php
$addon = rex_addon::get('mein_addonkey');
rex_view::addCssFile($addon->getAssetsUrl('styles.css') );
rex_view::addJsFile($addon->getAssetsUrl('script.js') );
```
<a name="sparsam"></a>
### Assets nur dort einbinden wo gebraucht 

Die Assets sollten möglichst "sparsam" eingebunden werden. Werden diese nur auf einer bestimmten Seite gebraucht, kann dies auf der gewünschen Seite wie hier beschrieben erfolgen: 

``` php
// Ermitteln welche Backendseite aufgerufen ist:
if (rex::isBackend() && rex_be_controller::getCurrentPage() == 'addonkey/unterseite') {

// Hier z.B. Assets einbinden

}
```

<a name="buster"></a>

### Cachebuster

REDAXO liefert selbst einen Cachebuster. Eigene Lösungen hierfür sind nicht erforderlich. Der Buster wird automatisch gesetzt. Beispiel: `index.php?asset=../assets/addon/skript.min.js&amp;buster=1566304624` 

<a name="javascripte"></a>

### Javascripte (JS_IMMUTABLE, Async, JS_DEFERED)

`rex_view::addJsFile bietet weitere Funktionen um das Caching sowie das Ladeverhalten der Javascripte zu beeinflussen.

Hier ein Beispiel mit allen möglichen Optionen:

``` js
rex_view::addJsFile(
    rex_url::addonAssets('my_addon', 'js/myscript.min.js'),
    [rex_view::JS_IMMUTABLE => false, rex_view::JS_ASYNC => true, rex_view::JS_DEFERED => true]
);
```

<a name="rexready"></a>

## Javascript im Backend / Das Event: rex:ready

Da REDAXO im Backend PJAX nutzt, verwendet es ein eigenes Event um den ready-Status zu liefern. Daher sollte anstelle des JQuery- `document:ready` Events das `rex:ready` event als Auslöser für eigene Skripte verwendet werden.
Das `rex:ready` -Event greift auch, wenn PJAX nicht im Einsatz ist und kann daher immer verwendet werden.

Anwendung:

``` js
$(document).on('rex:ready', function() {
    // eigener Code
});
```

Beispiel:

Das findet sich so zum Beispiel im be_style-Plugin. `container` ist immer der Container, der ausgetauscht wurde. Initial bei `document:ready` ist es der `<body>` .

```js
$(document).on('rex:ready', function(event, container) {
    container.find('.selectpicker').selectpicker();
});
```


<a name="phpJs"></a>

## PHP-Werte an Javascript übergeben

Per `rex_view::setJsProperty('key',$value)` können Variablen im Backend-Javascript gesetzt werden, die global als `rex.key` zur Verfügung stehen und somit auch in eigenen Javascripten zur Verfügung stehen. 

### Beispiel

// Übergabe einer URL an das eigene AddOn Javascript

```php
rex_view::setJsProperty('myicons', rex_url::addonAssets('myaddon') . 'icons.svg');
```

Die Variable steht dann im Javascript als `rex.myicons` zur Verfügung. 


## Sass

Es ist möglich `.scss` Dateien mit der Klasse `rex_scss_compiler()` zu kompilieren. Es bietet sich an, solche Dateien in einem separaten Ordner anzulegen. Kompilierte Versionen der Dateien sollten bei Bereitstellung des AddOns bereits im Assets-Ordner vorliegen. Die scss-Dateien sollten nur für Anpassungen oder Fehlerbehebungen durch REDAXO neu kompiliert werden.

Der nachfolgend kommentierte Code für die `boot.php` zeigt, wie man die Kompilierung bei aktiviertem Debug-Modus ausführt.

```php
// Befinden wir uns im Backend und ist ein User angemeldet?
if (rex::isBackend() && rex::getUser())
    {
        // Prüft ob der DebugMode in System aktiviert ist und ein Request erfolgte
        if (rex::isDebugMode() && rex_request_method() == 'get')
        {
            // Compiler
            $compiler = new rex_scss_compiler();
            // Hauptverzeichnis des AddOns
            $compiler->setRootDir($this->getPath());
            // Festlegen des SCSS-Files
            $compiler->setScssFile($this->getPath('scss/meinestile.scss'));
            // Wo soll die kompilierte Version erstellt werden?
            $compiler->setCssFile($this->getPath('assets/meinestile.css'));
            // Kompilierung starten
            $compiler->compile();
            // Kopiere das kompilierte css in den öffentlichen assets-Ordner
            rex_file::copy($this->getPath('assets/meinestile.css'), $this->getAssetsPath('meinestile.css'));
        }
    }
```

<a name="themes"></a>

## Backend-Themes

Seit Version 5.13 bietet REDAXO zwei Themes an, »Hell« (`light`) und »Dunkel« (`dark`). Verwenden AddOns lediglich Standardelemente von REDAXO und Bootstrap, sind sie üblicherweise bereits kompatibel mit beiden Themes. Nutzen sie jedoch individuelle Styles mit Farbangaben, liegt es an den Entwickelnden, diese für beide Themes zu liefern.

Die Themeauswahl erfolgt auf der Profilseite der Benutzer oder wird innerhalb der `config.yml` für alle Nutzer fest vorgegeben. Es gibt einen zusätzlichen Modus »Automatisch«, der die Voreinstellung für alle neuen Nutzer ist, und der es dem Browser überlässt, anhand der Systemeinstellungen der Nutzer das passende Theme auszuwählen.

Das Styling erfolgt deshalb sowohl über eine Klasse am `<body>` als auch mittels der Media Query `prefers-color-scheme` (für den automatischen Modus):

```css
body.rex-theme-dark {
	…
}

@media (prefers-color-scheme: dark) {
	body.rex-has-theme:not(.rex-theme-light) {
		…
	}
}
```

Beim Styling muss also beachtet werden, dass jeder Selektor zweimal angesprochen wird. Mit nativem CSS ist das leider etwas aufwendiger als beispielsweise mit Sass, bei dem _mixins_ verwendet werden können.

### CSS:

Alle Selektoren liegen doppelt vor und hängen sowohl an der `<body>`-Klasse und an der Media Query:

```css
/* Styles für den Dark Mode bei manueller Auswahl durch die Nutzer */
body.rex-theme-dark .addon-element-1 { … }
body.rex-theme-dark .addon-element-2 { … }

@media (prefers-color-scheme: dark) {
	/* Styles für den Dark Mode im Modus »Automatisch« */
	body.rex-has-theme:not(.rex-theme-light) .addon-element-1 { … }
	body.rex-has-theme:not(.rex-theme-light) .addon-element-2 { … }
}
```

### Sass:

Zunächst wird ein beispielhaftes Mixin `_addon-dark` definiert. Zu beachten ist dabei, dass Mixins üblicherweise global vorliegen. Um Konflikte zu vermeiden, bietet sich deshalb an, immer eindeutige Bezeichnungen zu verwenden. Der Unterstrich am Anfang ist nicht notwendig und soll lediglich vermitteln, dass es sich um ein privates Mixin handelt, das nicht global verwendet werden soll.

Innerhalb des Mixins werden alle Styles für das Dark-Theme notiert. Anschließend wird das Mixin in beiden Kontexten inkludiert.


```scss
@mixin _addon-dark {
	// Alle Styles für den Dark Mode werden hier notiert
	.addon-element-1 { … }
	.addon-element-2 { … }
}

body.rex-theme-dark {
	@include _addon-dark;
}

@media (prefers-color-scheme: dark) {
	body.rex-has-theme:not(.rex-theme-light) {
		@include _addon-dark;
	}
}
```

### Less:


```less
._addon-dark() {
	// Alle Styles für den Dark Mode werden hier notiert
	.addon-element-1 { … }
	.addon-element-2 { … }
}

body.rex-theme-dark {
	._addon-dark();
}

@media (prefers-color-scheme: dark) {
	body.rex-has-theme:not(.rex-theme-light) {
		._addon-dark();
	}
}
```

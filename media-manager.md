# # # Media Manager
- [Prinzip](#prinzip)
- [Effekte](#effekte)
- [Konfiguration des Media Managers](#konfiguration)
- [Beispiel: Einen Effekt definieren und anwenden](#beispiel)
- [Vordefinierte Medientypen](#vordefiniert)
- [Auslesen der Medieninformationen nach Anwendung der Effekte](#mediainfo)

<a name="prinzip"></a>
## Prinzip
Pronzip und Effekte
Der Media Manager ist ein Basis-AddOn von REDAXO, das bereits mit der Grundinstallation installiert und aktiviert wird.
Das AddOn dient zum Anpassen von Grafiken und Handling von Dateien anhand von Mediatypen. Die Mediatypen werden in der Verwaltung des AddOns erstellt und konfiguriert. Jeder Mediatyp kann beliebig viele Effekte enthalten, die auf das aktuelle Medium angewendet werden. Zum Einbinden eines Mediums muss dazu der Mediatyp in der URL notiert werden (Beispiel siehe unten).

Die durch den Media Manager erstellten Bilddateien werden in einem eigenen Cache abgelegt, der bei Bedarf auch für jeden einzelnen Bildtyp gelöscht werden kann.

Die am häufigsten benutzten Effekte für den Media Manager sind resize und crop. Damit können Bilder auf eine einheitliche Größe gebracht werden (siehe Beispiel unten).

<a name="effekte"></a>
## Effekte

Folgende Effekte stehen zur Verfügung:

Effekt| Beschreibung
------------- | -------------
convert2img | Konvertiert eine Quelldatei in ein Web-Format. Mögliche Formate für die Bildquelle: .pdf, .ps, .psd, .tif,     .tiff, .bmp, .eps, .ico. Mögliche Formate für das Ziel: .jpg, .png
crop | Beschneidet ein Bild auf die angegebene Größe (Angabe in Pixel)
filter_blur | Weichzeichnungsfilter
filter_colorize | Einfärben eines Bildes
filter_greyscale | Bild in Graustufen umwandeln
filter_sepia | Bild mit Sepiatönung versehen
filter_sharpen | Scharfzeichnen eines Bildes
flip | Kann ein Bild horizontal oder vertikal spiegeln
header | Das Medium wird nicht im Browser angezeigt, sondern als Download ausgegeben
insert_image | Ein Bild in ein anderes kopieren (z.B. für Wasserzeichen)
mediapath | Das Medium wird in einem von media abweichenden Pfad gesucht
mirror | Spiegelungseffekt unterhalb des Bildes
resize | Verkleinern / Vergrößern unter Angabe der gewünschten Breite, bzw. Höhe in Pixel. Die Werte können optional als minimal, maximal oder exakt angegeben werden
rotate | Effekt zum Drehen eines Bilds (90, 180 oder 270 Grad)
rounded_corners | runde Ecken
workspace | Hier kann eine Zeichenfläche inklusive Hintergrundfarbe definiert werden, auf der das Medium platziert wird.

Alle Effekte können kaskadiert, also hintereinander als "Bearbeitungskette" werden.

<a name="konfiguration"></a>
## Konfiguration des Media Managers

In der Konfiguration des Media Managers kann die gewünschte Komprimierung für die erzeugten jpg-Dateien angegeben werden. Ein hoher Wert ergibt ein besseres Ergebnis und größere Bilddateien, bei einem niedrigeren Wert gehen mehr Bilddetails verloren, es entstehen aber kleinere Bilddateien.

<a name="beispiel"></a>
## Beispiel: Einen Effekt definieren und anwenden

- Im AddOn-Menü auf den Menüpunkt `Media Manager` gehen
- In der Tabelle links oben das Plus-Zeichen (+) wählen
- Bei `Name` einen Namen schreiben, unter dem der Effekt verfügbar sein soll. Der Name wird für den Aufruf des Effekts über die URL verwendet (z.B. `thumb_small`)
- Eine kurze Beschreibung zum Effekt ergänzen (z.B. `Galerie Vorschaubilder 120 x 120 Pixel`)
- Den neuen Bildtyp speichern und dann `Effekt bearbeiten` wählen
- Einen Effekt mit dem kleinen Plus-Zeichen (+) hinzufügen. Z.B. `resize` wählen
- Als Zielbreite und als Zielhöhe jeweils `120` eingeben, den Modus `minimum` wählen und – wenn Bild zu klein – `enlarge`
- Den Effekt speichern
- Den Effekt `crop` hinzufügen. Zielbreite und Zielhöhe jeweils `120`. Horizontale Ausrichtung: `center`, vertikale Ausrichtung: `middle`
- Den Effekt speichern
    
Den Effekt kann man nun bereits prüfen, indem man im Browser die URL zum Bild eingibt:

http://example.com/index.php?rex_media_type=thumb_small&rex_media_file=bilddatei_aus_dem_medienpool.jpg

Die Bilddatei `bilddatei_aus_dem_medienpool.jpg` muss schon im Medienpool angelegt sein, bzw. im Verzeichnis `media` liegen.

<a name="vordefiniert"></a>
## Vordefinierte Medientypen

Bei der Installation von Redaxo werden bereits einige Medientypen definiert, die intern beispielsweise für den Medienpool verwendet werden.

Medientyp | Beschreibung
------------- | -------------
rex_mediabutton_preview | resize auf max. 246 x 246 px
rex_medialistbutton_preview | resize auf max. 246 x 246 px
rex_mediapool_detail | resize auf max. 200 x 200 px
rex_mediapool_maximized | resize auf max. 600 x 600 px
rex_mediapool_preview | resize auf max. 80 x 80 px

Diese Medientypen können auch für eigene Zwecke verwendet werden, beispielsweise um in Modulen im Backend eine Vorschau der Bilder anzuzeigen.

Beispiel einer Modulausgabe:

    <?php
    $imagelist = explode(',', "REX_MEDIALIST[1]");
    $mediatype = rex::isBackend() ? 'rex_mediabutton_preview' : 'mein_eigener_medientyp';
    ?>
    
    <ul class="meinebildgalerie">
    <?php foreach ($imagelist as $img) : ?>
        <li class="meinebildergalerie_li">
            <img src="<?= rex::getServer() ?>index.php?rex_media_type=<?= $mediatype ?>&rex_media_file=<?= $img ?>">
        </li>    
    <?php endforeach ?>
    </ul>

Dieses Beispielmodul gibt im Backend die Bilder aus der `REX_MEDIALIST[1]` in einer Größe von maximal 246 x 246 Pixel aus; im Frontend werden die Bilder mit dem selbst definierten Medientyp `mein_eigener_medientyp` ausgegeben.

<a name="mediainfo"></a>
## Auslesen der Medieninformationen nach Anwendung der Effekte

Zur korrekten Darstellung eines Mediums ist häufig die Angabe von Höhen und Breitenangaben in den Tags alls Attribute erfordelich. Die berechneten Werte erhält man, indem man das Medium über die create-Methode der rex_media_manager-Class erstellt.   

```php
// Erstellen der Mediendatei
$media = rex_media_manager::create($type, $file)->getMedia();
// Informationen zum Format ermitteln
$media->getFormat();
// Breite auslesen
$media->getWidth();
// Höhe auslesen
$media->getHeight();
// Header-Informationen auslesen
$media->getHeader();
```


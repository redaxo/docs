# Media Manager

* [Prinzip](#prinzip)
* [Erzeugung der URL](#url)
* [Effekte](#effekte)
* [Konfiguration des Media Managers](#konfiguration)
* [Beispiel: Einen Effekt definieren und anwenden](#beispiel)
* [Vordefinierte Medientypen](#vordefiniert)
* [Auslesen der Medieninformationen nach Anwendung der Effekte](#mediainfo)
* [Medien außerhalb des media-Ordners verarbeiten](#extmedia)

<a name="prinzip"></a>

## Prinzip

**Prinzip und Effekte**

Das AddOn erlaubt das Anpassen von Grafiken und Handling von Dateien anhand von Mediatypen. Die Mediatypen werden in der Verwaltung des AddOns erstellt und konfiguriert. Jeder Mediatyp kann beliebig viele Effekte enthalten, die auf das aktuelle Medium angewendet werden. Zum Einbinden eines Mediums muss dazu der Mediatyp in der URL notiert werden.

<a name="url"></a>

## Erzeugung der URL

### Mittels PHP-Methode (empfohlen)

``` php
$url = rex_media_manager::getUrl($type,$file);
```

> Der Pfad zum Medium muss nicht angegeben werden.

### Direkter Auruf per URL

``` php
index.php?rex_media_type=MediaTypeName&amp;rex_media_file=MediaFileName
```

> MediaTypeName = Der MediaManager-Typ, MediaFileName = Dateiname des Mediums. Der Pfad zum Medium muss nicht angegeben werden.  

Die durch den Media Manager erstellten Dateien, werden in einem eigenen Cache abgelegt, der bei Bedarf auch für jeden einzelnen Typ gelöscht werden kann.

Häufig benutzte Effekte für den Media Manager sind resize und crop. Damit können Bilder auf eine einheitliche Größe gebracht und zugeschnitten werden (siehe Beispiel unten).

<a name="effekte"></a>

## Effekte Bild: 
Folgende Effekte stehen zur Verfügung:

| Effekt           | Beschreibung                                                                                                                                                                                                                     |
|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| convert2img      | Konvertiert eine Quelldatei in ein Web-Format. Mögliche Formate für die Bildquelle: .pdf, .ps, .psd, .tif, .tiff, .bmp, .eps, .ico. Mögliche Formate für das Ziel: .jpg, .png **ImageMagick** sollte über *exec* verfügbar sein. |
| img2img          |  In JPEG/PNG/GIF/WEBP/AVIF konvertieren 
| crop             | Beschneidet ein Bild auf die angegebene Größe (Angabe in Pixel)                                                                                                                                                                  |
| filter_blur      | Weichzeichnungsfilter                                                                                                                                                                                                            |
| filter_colorize  | Einfärben eines Bildes                                                                                                                                                                                                           |
| filter_greyscale | Bild in Graustufen umwandeln                                                                                                                                                                                                     |
| filter_sepia     | Bild mit Sepiatönung versehen                                                                                                                                                                                                    |
| filter_sharpen   | Scharfzeichnen eines Bildes                                                                                                                                                                                                      |
| flip             | Kann ein Bild horizontal oder vertikal spiegeln                                                                                                                                                                                  |
| header           | Das Medium wird nicht im Browser angezeigt, sondern als Download ausgegeben                                                                                                                                                      |
| insert_image     | Ein Bild in ein anderes kopieren (z. B. für Wasserzeichen)                                                                                                                                                                       |
| mediapath        | Das Medium wird in einem von media abweichenden Pfad gesucht                                                                                                                                                                     |
| mirror           | Spiegelungseffekt unterhalb des Bildes                                                                                                                                                                                           |
| resize           | Verkleinern / Vergrößern unter Angabe der gewünschten Breite, bzw. Höhe in Pixel. Die Werte können optional als minimal, maximal oder exakt angegeben werden                                                                     |
| rotate           | Effekt zum Drehen eines Bilds (90, 180 oder 270 Grad)                                                                                                                                                                            |
| rounded_corners  | runde Ecken                                                                                                                                                                                                                      |
| workspace        | Hier kann eine Zeichenfläche inklusive Hintergrundfarbe definiert werden, auf der das Medium platziert wird.                                                                                                                     |

Alle Effekte können kaskadiert, also hintereinander als "Bearbeitungskette" verwendet werden.

<a name="konfiguration"></a>

## Konfiguration des Media Managers

In der Konfiguration des Media Managers kann die gewünschte Komprimierung für die erzeugten jpg-Dateien angegeben werden. Ein hoher Wert ergibt ein besseres Ergebnis und größere Bilddateien, bei einem niedrigeren Wert gehen mehr Bilddetails verloren, es entstehen aber kleinere Bilddateien.

<a name="beispiel"></a>

## Beispiel: Einen Effekt definieren und anwenden

* Im AddOn-Menü auf den Menüpunkt `Media Manager` gehen
* In der Tabelle links oben das Plus-Zeichen (+) wählen
* Bei `Name` einen Namen schreiben, unter dem der Effekt verfügbar sein soll. Der Name wird für den Aufruf des Effekts über die URL verwendet (z. B. `thumb_small` )
* Eine kurze Beschreibung zum Effekt ergänzen (z. B. `Galerie Vorschaubilder 120 x 120 Pixel` )
* Den neuen Bildtyp speichern und dann `Effekt bearbeiten` wählen
* Einen Effekt mit dem kleinen Plus-Zeichen (+) hinzufügen. Z. B. `resize` wählen
* Als Zielbreite und als Zielhöhe jeweils `120` eingeben, den Modus `minimum` wählen und – wenn Bild zu klein – `enlarge` 
* Den Effekt speichern
* Den Effekt `crop` hinzufügen. Zielbreite und Zielhöhe jeweils `120` . Horizontale Ausrichtung: `center` , vertikale Ausrichtung: `middle` 
* Den Effekt speichern

Den Effekt kann man nun bereits prüfen, indem man im Browser die URL zum Bild eingibt:

<http://example.com/index.php?rex_media_type=thumb_small&rex_media_file=bilddatei_aus_dem_medienpool.jpg>

Die Bilddatei `bilddatei_aus_dem_medienpool.jpg` muss schon im Medienpool angelegt sein, bzw. im Verzeichnis `media` liegen.

<a name="vordefiniert"></a>

## Vordefinierte Medientypen

Bei der Installation von REDAXO werden bereits einige Medientypen definiert, die intern beispielsweise für den Medienpool verwendet werden.
Die Effekte der nachstehenden Medientypen können nicht verändert werden. 

| Medientyp                   | Beschreibung                 |
|-----------------------------|------------------------------|
| rex_media_large             | resize auf max. 1200 x 1200 px |
| rex_media_medium            | resize auf max. 600 x 600 px |
| rex_media_small             | resize auf max. 200 x 200 px |


Diese Medientypen können auch für eigene Zwecke verwendet werden, beispielsweise um in Modulen im Backend eine Vorschau der Bilder anzuzeigen.

**Beispiel einer Modulausgabe:***

``` php
$imagelist = explode(',', "REX_MEDIALIST[1]");
$mediatype = rex::isBackend() ? 'rex_media_small' : 'mein_eigener_medientyp';
?>

<ul class="meinebildgalerie">
 <?php foreach ($imagelist as $img) : ?>
   <li class="meinebildergalerie_li">
       <img src="<?= rex_url::frontend().rex_media_manager::getUrl($mediatype,$img); ?>">
   </li>
<?php endforeach ?>
</ul>
```

Dieses Beispielmodul gibt im Backend die Bilder aus der `REX_MEDIALIST[1]` in einer Größe von maximal 200 x 200 Pixel aus; im Frontend werden die Bilder mit dem selbst definierten Medientyp `mein_eigener_medientyp` ausgegeben.

<a name="mediainfo"></a>

## Auslesen der Medieninformationen nach Anwendung der Effekte

Zur korrekten Darstellung eines Mediums ist häufig die Angabe von Höhen und Breitenangaben in den Tags als Attribute erforderlich. Die berechneten Werte erhält man, indem man das Medium über die create-Methode der rex_media_manager-Class erstellt.

``` php
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

<a name="extmedia"></a>

## Medien außerhalb des media-Ordners verarbeiten

Mit dem Effekt `Datei: Pfad anpassen` ist es möglich auf Dateien außerhalb des media-Ordners zuzugreifen und diese zu verarbeiten.

1. Im Media Manager einen neuen Mediatypen anlegen
2. Die gewünschten Effekte anlegen -> Wichtig: `Datei: Pfad anpassen` muss am Anfang stehen (Prio 1)
3. Beim Effekt "Datei: Pfad anpassen" im Feld Medienordner den Pfad eintragen (Bsp.: "assets/logos/")
4. Im AddOn auf den Mediatypen zugreifen: `$url = rex_media_manager::getUrl('medientyp','bild.jpg');` 

# Media Manager

Der Media Manager ist ein Basis Addon von Redaxo, welches bereits mit der Grundinstallation installiert und aktiviert wird.
Das Addon dient zum Anpassen von Grafiken und Handling von Dateien anhand von Mediatypen. Die Mediatypen werden in der Verwaltung des Addons erstellt und konfiguriert. Jeder Mediatyp kann beliebig viele Effekte enthalten, die auf das aktuelle Medium angewendet werden. Zum einbinden eines Mediums muss dazu der Mediatyp in der Url notiert werden (Beispiel siehe unten).

Die durch den Media Manager erstellten Bilddateien werden in einem eigenen Cache abgelegt, der bei Bedarf auch für jeden einzelnen Bildtyp gelöscht werden kann.

Die am häufigsten benutzten Effekte für den Media Manager sind resize und crop. Damit können Bilder auf eine einheitliche Größe gebracht werden (siehe Beispiel unten).

Folgende Effekte stehen zur Verfügung:

Effekt| Beschreibung
------------- | -------------
convert2img  |  konvertiert eine Quelldatei in ein Web-Format. Mögliche Formate für die Bildquelle: .pdf, .ps, .psd, .tif,     .tiff, .bmp, .eps, .ico. Mögliche Formate für das Ziel: .jpg, .png
crop  | beschneidet ein Bild auf die angegebene Größe (Angabe in Pixel)
filter_blur | Unschärfefilter
filter_colorize | Einfärben eines Bildes
filter_greyscale | Bild in Graustufen umwandeln
filter_sepia | Bild mit Sepiatönung versehen
filter_sharpen | Scharfzeichnen eines Bildes
flip | Kann ein Bild horizontal oder vertikal spiegeln
header | das Medium wird nicht im Browser angezeigt sondern als Download ausgegeben
insert_image | Ein Bild in ein anderes kopieren (z.B. für Wasserzeichen)
mediapath | das Medium wird in einem von media abweichenden Pfad gesucht
mirror | Kann irgendeinen Spiegelungseffekt (muss ich mir noch anschauen)
resize | verkleinern / vergrößern unter Angabe der gewünschten Breite bzw. Höhe in Pixel. Die Werte können optional als minimal, maximal oder exakt angegeben werden
rotate | Effekt um ein Bild zu drehen (90, 180 oder 270 Grad)
rounded_corners | braucht kein Mensch, dafür gibt es CSS
workspace | Hier kann eine Zeichenfläche inkl. Hintergrundfarbe definiert werden auf der das Medium platziert wird.

Alle Effekte können kaskadiert werden.

### Konfiguration des Media Managers

In der Konfiguration des Media Managers kann die gewünschte Komprimierung für die erzeugten jpg-Dateien angegeben werden. Ein hoher Wert ergibt ein besseres Ergebnis und größere Bilddateien, bei einem niedrigeren Wert gehen mehr Bilddetails verloren, es entstehen aber kleinere Bilddateien.

### Beispiel - Einen Effekt definieren und anwenden

- Gehe im Addon-Menü auf den Menüpunkt "Media Manager"
- Wähle in der Tabelle links oben das Plus-Zeichen (+)
- Schreibe bei Name einen Namen, unter dem der Effekt verfügbar sein soll. Der Name wird für den Aufruf des Effekts über die Url verwendet (z.B. thumb_small)
- Schreibe eine kurze Beschreibung zum Effekt (z.B. Galerie Vorschaubilder 120 x 120 Pixel)
- Speichere den neuen Bildtyp und wähle dann "Effekt bearbeiten"
- Füge einen Effekt mit dem kleinen Plus-Zeichen (+) hinzu. Wähle z.B. "resize"
- Gebe als Zielbreite und als Zielhöhe jeweils 120 ein, wähle Modus "minimum" und Wenn Bild zu klein "enlarge"
- Speichere den Effekt
- Füge den Effekt "crop" hinzu. Zielbreite und Zielhöhe jeweils 120. Horizontale Ausrichtung: center, vertikale Ausrichtung: middle
- Speichere den Effekt
    
Den Effekt kannst Du nun bereits prüfen, indem Du im Browser die Url zum Bild eingibst:

http://example.com/index.php?rex_media_type=thumb_small&rex_media_file=bilddatei_aus_dem_medienpool.jpg

Die Bilddatei bilddatei_aus_dem_medienpool.jpg muss schon im Medienpool angelegt sein bzw. im Verzeichnis media liegen.

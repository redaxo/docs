# Caching

* [Prinzip und Bestandteile](#prinzip)
* [System-Cache löschen](#system-cache)
* [Media Manager-Cache löschen](#media-manager-cache)
* [Hinweise für Entwickler](#hinweise)
* [Anmerkung für Anwender](#anmerkung)

<a name="prinzip"></a>

## Prinzip und Bestandteile

Der Cache von REDAXO dient einer besseren Performance des Gesamtsystems, da so die Zahl der Datenbank-Abfragen minimiert wird.

Folgende Bestandteile werden im Cache gespeichert:

* Autoload (Einbindung von Klassen aus AddOns)
* Templates
* Kategorien
* Artikel
* Medien

<a name="system-cache"></a>

## System-Cache löschen

Der Cache des Gesamtsystems kann über den Menüpunkt `System` mit einem Klick auf den roten Button `Cache löschen` gelöscht werden. Dies sollte jedoch nur im Ausnahmefall notwendig sein. Im normalen Betrieb erkennt REDAXO automatisch, welche Teile des Cache erneuert werden müssen.

**Hinweis** Die Systemfunktion `Cache löschen` löscht auch den Cache des Media Managers. Der Cache baut sich jeweils beim Aufruf einer Seite neu auf. Daher dauert der erste Aufruf einer Seite nach dem Löschen des Cache je nach Serverleistung und Serverbelastung länger, als wenn die Seite bereits gecacht ist – insbesondere wenn die im Media Manager definierten Bilder neu generiert werden müssen.

<a name="media-manager-cache"></a>

## Media Manager-Cache löschen

Die im Media Manager definierten Medientypen werden beim ersten Aufruf des Mediums erstellt und im Media Manager Cache abgelegt. Bei jedem weiteren Aufruf wird das Bild dann direkt aus der Cache-Datei ausgeliefert.

Der Media Manager Cache kann für jeden Medientyp separat gelöscht werden. Um den Cache des Media-Managers zu löschen, muss man als Administrator eingeloggt sein oder das Recht `Media Manager` haben.
Der Medien-Cache kann im Media Manager-AddOn auch komplett gelöscht werden.

Wenn ein Medientyp geändert wird, muss man den Cache des Media-Managers nicht löschen. Das System erkennt, wenn ein Medientyp geändert wurde und löscht die entsprechenden Dateien automatisch.

<a name="hinweise"></a>

## Hinweise für Entwickler

Folgende REDAXO-Klassen werden automatisch gecacht:

* rex_category
* rex_article
* rex_media_category
* rex_media

Nicht gecached wird:

* rex_article_slice

Eigene Cache Dateien können im REDAXO Cache so angelegt werden:

```php
    if (!rex_file::put(rex_path::addonCache('meinaddon', $filename), $filecontent)) {
        echo 'Cachefile für mein AddOn konnte nicht geschrieben werden!';
    }
```

In diesem Beispiel wird geprüft, ob das Verzeichnis `redaxo/cache/addons/meinaddon` vorhanden ist und legt es gegebenenfalls an (`rex_file::put(..)` übernimmt das). `rex_path::addonCache('meinaddon', $filename)` erzeugt den passenden Pfad. Für die Verwaltung und die Entscheidung, wann und ob eine Cache-Datei neu geschrieben werden muss, ist der Entwickler verantwortlich.

In AddOns kann es manchmal notwendig sein, den Cache zu löschen. Dies kann durch Aufruf der global zur Verfügung stehenden Funktion `rex_delete_cache()` ausgeführt werden. Das sollte jedoch nur in Ausnahmefällen notwendig sein.

<a name="anmerkung"></a>

## Anmerkung für Anwender

Der System-Cache von REDAXO ist nicht zu verwechseln mit dem Cache des Browsers. Beim Aufruf einer Seite werden in der Regel alle Elemente im Browser-Cache gespeichert. Auch hier kommt es vor, dass dieser Cache gelöscht werden muss, insbesondere wenn unerwartete Erscheinungen bei der Darstellung einer Seite auftreten oder Änderungen nicht angezeigt werden.

# Caching

Der Cache von Redaxo dient einer besseren Performance des Gesamtsystems.

Folgende Bestandteile werden im Cache gespeichert:

- Autoload (Einbindung von Klassen aus Addons)
- Templates
- Kategorien
- Artikel
- Medien

## System Cache löschen

Der Cache des Gesamtsystems kann über den Menüpunkt "System" mit einem Klick auf den roten Button "Cache löschen" gelöscht werden. Dies sollte nur im Ausnahmefall notwendig sein. Im normalen Betrieb erkennt Redaxo automatisch welche Teile des Cache erneuert werden müssen.

**Hinweis** Die Systemfunktion "Cache löschen" löscht auch den Cache des Media Managers. Der Cache baut sich jeweils beim Aufruf einer Seite neu auf. Daher dauert der erste Aufruf einer Seite nach dem Löschen des Cache je nach Serverleistung und Serverbelastung länger, als wenn die Seite bereits gecached ist.

## Media Manager Cache löschen

Die im Media Manager definierten Medientypen werden beim ersten Aufruf des Mediums erstellt und im Media Manager Cache abgelegt. Bei jedem weiteren Aufruf wird das Bild direkt aus dem Cache ausgeliefert. Der Media Manager Cache kann für jeden Medientyp separat gelöscht werden. Um den Cache des Media Managers zu löschen, muss man als Administrator eingeloggt sein oder das Recht "Media Manager" haben.
Der Mediencache kann im Media Manager AddOn auch komplett gelöscht werden.

Wenn ein Medientyp geändert wird, so muss der Cache des Media Managers nicht gelöscht werden. Das System erkennt, wenn ein Medientyp geändert wurde und löscht die entsprechenden Dateien automatisch.

## Hinweise für Entwickler

Folgende Redaxo Klassen werden automatisch gecached:

- rex_category
- rex_article
- rex_media_category
- rex_media

Nicht gecached wird

- rex_article_slice

In AddOns kann es manchmal notwendig sein den Cache zu löschen. Dies kann durch Aufruf der global zur Verfügung stehenden Funktion rex_delete_cache() ausgeführt werden. Dies sollte jedoch nur in Ausnahmefällen notwendig sein.

## Anmerkung für Anwender

Der Systemcache von Redaxo ist nicht zu verwechseln mit dem Cache des Browsers. Beim Auruf einer Seite werden in der Regel alle Elemente im Browsercache gespeichert. Auch hier kommt es vor, dass dieser Cache gelöscht werden muss, insbesondere wenn unerwartete Erscheinungen bei der Darstellung einer Seite auftreten oder Änderungen nicht angezeigt werden.
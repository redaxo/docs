# Benutzerverwaltung

Durch das Anlegen verschiedener Benutzer-Accounts regeln Sie die Rechtevergabe in REDAXO. Mit der Konfiguration des Accounts geben Sie Programmteile und Funktionen in REDAXO frei und können so auch sensible Bereiche verstecken und sperren.

### Beispiele für die Rechtevergabe beziehungsweise für ihre Einschränkung können sein

**REDAXO-Navigation**

So können zu Beispiel die Bereiche Templates und Module für Redakteure ohne Programmierkenntnisse gesperrt und der Bereich Medienpool freigeschaltet werden.

**Kategorien und Artikel**

Sie können innerhalb der Strukturverwaltung bestimmte Kategorien und Artikel freigeben oder durch Nicht-Freigabe die Bearbeitung bestimmter anderer Seiten sperren.

**Module**

Über die Vergabe von Zugriffsrechten auf Module können die Modullisten und Blöcke in den Artikeln frei oder gesperrt geschaltet werden

###Benutzer anlegen

Es können beliebig viele Nutzer definiert werden. Der Administrator wird normalerweise bei der REDAXO-Installation automatisch angelegt.

Um einen neuen Benutzer anzulegen, klickt man auf das Symbol oben links in der Rubrik “Benutzer”. Dann bekommt man eine Maske angezeigt, die sämtliche Optionen enthält, die man einem Benutzer zuweisen kann.

Benutzer neu anlegen
Hier werden zunächst Benutzername und Passwort festgelegt, welche der Benutzer beim Login angeben muss. Name und Beschreibung dienen nur zur Übersichtlichkeit im Backend, falls mehrere Benutzer angelegt werden. Sie sind nicht zwingend erforderlich.

Durch Setzen eines Häkchens bei “Admin (Alle Rechte / Alles sichtbar)” kann man pauschal alle Rechte an diesen Nutzer vergeben. Ansonsten können einzelne Rechte durch Selektieren der Listenpunkte mit gedrückter Strg-Taste (Windows) / Apfel-Taste (Mac) gezielt ausgewählt werden.

Das Häkchen bei “User ist aktiv” ist standardmäßig gesetzt. Durch Deaktivierung kann man den User sperren, ohne ihn gleich löschen zu müssen.

Ist eine Seite in mehreren Sprachen angelegt, kann der Zugriff auf einzelne Sprachen beschränkt werden.

**Allgemein**

Der Bereich “Allgemein” regelt den Zugriff auf die Bereiche im REDAXO-Backend.

- ```import[ ]``` Er darf die import/export-Funktionen nutzen.
- ```image_manager[ ]``` Er darf die image_manager-Funktionen nutzen.

> **Hinweis ab Version 4.2**
> 
> Ab Version 4.2 sind die folgenden Rechte nicht mehr verfügbar.
> Diese Rechte sind gruppiert und eingebunden als “Admin”.
> 
> - ```addon[ ]``` Der Benutzer erhält Zugriff auf den Bereich Addons.
> - ```module[ ]``` Er kann Module erstellen oder verändern.
> - ```mediapool[ ]``` Er erhält Zugriff auf den Bereich Medienpool. Berechtigung zum Zugriff wird über die Auswahl der Rechte “Medienordner” gesetzt. Ist keine Medienordner ausgewählt, so wird der “Medienpool” nicht angezeigt.
> template[ ]``` Er erhält die Möglichkeit, Templates zu erstellen oder zu verändern.
> - ```user[ ]``` Er kann andere Benutzer anlegen und verändern.
> - ```metainfo[ ]``` Er darf eigene Metadatenfelder definieren.
> - ```specials[ ]``` Er darf Einstellungen am System vornehmen oder neue Sprachen verwalten.

**Optionen**

Der Bereich “Optionen” regelt bestimmte Einstellungen für Redakteur-Funktionen. Hier wird festgelegt, ob dieser Benutzer

- ```accesskeys[ ]``` Accesskeys im Backend verwenden darf. Ein Erklärung zu Accesskeys finden Sie hier: http://www.barrierefreies-webdesign.de/knowhow/accesskey/accesskey.html
- ```advancedMode[ ]``` die Metadaten zu den Artikeln sehen und bearbeiten darf.
- ```article2category[ ]``` (ab Version 4.3) einen Artikel zur Kategorie umwandeln kann.
- ```article2startpage[ ]``` einen Artikel in einen Startartikel umwandeln kann.
- ```be_search[medienpool]``` im Medienpool die Suchfunktion verwenden darf.
- ```be_search[structure]``` in den Kategorien oder Artikeln die Suchfunktion verwenden darf.
- ```category2article[ ]``` (ab Version 4.3) eine Kategorie zu einem Artikel umwandeln kann.
- ```copyArticle[ ]``` Artikel in eine andere Kategorie kopieren darf. Ist diese Berechtigung aktiviert, wird die Option zum Kopieren bei den Metadaten angezeigt.
- ```copyContent[ ]``` den Inhalt eines Artikels von einer Sprachversion in eine andere Sprache kopieren darf. Ist diese Berechtigung aktiviert, wird die Option zum Kopieren bei den Metadaten angezeigt.
- ```moveArticle[ ]``` “normale” Artikel in eine andere Kategorie verschieben darf. Ist diese Berechtigung aktiviert, wird die Option zum Verschieben bei den Metadaten angezeigt. Dies erfolgt nur bei normalen Artikeln. Für Startartikel gilt die Entsprechung “moveCategory”.
- ```moveCategory[ ]``` durch Verschieben eines Startartikels die komplette Kategorie in andere Kategorien verschieben darf. Diese Option wird bei den Metadaten nur bei Startartikeln angezeigt.
- ```moveSlice[ ]``` Blöcke/Slices im Artikel verschieben darf.
- ```publishArticle[ ] ``` Artikel online/offline stellen darf.
- ```publishCategory[ ]``` Kategorien online/offline stellen darf.

**Kategorien**

Durch Anklicken der Checkbox bei “Alle Kategorien” kann man pauschalen Zugriff auf alle Kategorien und Artikel gewähren. Ansonsten kann man einzelne Kategorien selektieren.

**Medienordner**

Es kann ein Zugriff auf alle oder auf einzelne “Medienordner” gewährt werden. Ebenso ist es möglich den Zugriff auf den Medienpool zu verweigern, indem kein “Medienordner” ausgewählt wird.

**Module**

Hier wird festgelegt, mit welchen Modulen der Benutzer die Inhalte bearbeiten darf.

**Extras**

Das Feld “Extras” dient für alle Rechte, die man per Addon/Modul/Template einbauen und verwenden kann. Falls Extras festgelegt wurden, kann hier der Zugriff darauf gewährt werden.

- ```editContentOnly[ ]``` Benutzer mit dieser “Berechtigung”, die eigentlich eine Einschränkung ist, dürfen nur Inhalte verändern, nicht aber Änderungen an der Struktur vornehmen.


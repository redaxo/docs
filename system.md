# System

- [Einstellungen](#einstellungen)
- [Sprachen](#sprachen)
- [mod_rewrite](#mod_rewrite)

<a name="einstellungen"></a>
## Einstellungen


###Cache löschen und Setup

Die Ansicht Einstellungen bietet die Features Cache löschen und Setup. Außerdem werden allgemeine Systemeinstellungen gelistet, die teilweise hier auch editiert werden können.

**Cache löschen**

Informationen zu Kategorien und Artikeln werden bei Redaxo nicht über SQL-Anfragen ermittelt, sondern aus generierten Dateien gelesen. Die Informationen werden in REDAXO automatisch angelegt und für eine schnelle Ausgabe bereitgestellt. Die Dateien werden in den Ordnern “articles”, “files” und “templates” im Ordner “redaxo/include/generated/” gespeichert. REDAXO nutzt bei der Ausgabe von Webseiten diese Informationen für eine schnelle und datenbankunabhängige Darstellung.

Über die Funktion “Cache löschen” werden die Informationen zu Artikeln, Dateien und Templates neu erstellt. Dazu werden die gecachten Dateien gelöscht.

**Setup**

Hier können Sie das Setup neu starten.

**Einstellungen (rechte Spalte)**

Es wird eine Liste allgemeiner Systemeinstellungen angezeigt.

Sie sehen zunächst Angaben zur installierten Redaxo-Version und zu der Datenbank.

Ein paar der Angaben können Sie in dieser Maske ändern.

**$REX['START_ARTICLE_ID']**

Der Startartikel ist der Artikel, der beim Aufruf einer Webpräsentation als erster angezeigt wird. Hier kann dieser durch die Auswahl über die Linkmap (linker Button; s.Abb. unten) festgelegt werden. Standardmäßig ist hier “Home” (=ArtikelID=1) voreingestellt.

**$REX['NOTFOUND_ARTICLE_ID']**

Sollte ein Seite nicht mehr existieren oder ein fehlerhaft verlinkter Artikel aufgerufen werden, kann hier angegeben werden, welcher Artikel stattdessen angezeigt werden soll, um mögliche Besucher nicht ins Leere laufen zu lassen.

**$REX['LANG']**

Sie können die Backend-Sprache wählen. Aktuell können Sie zwischen Deutsch, Englisch, Deutsch (utf-8) & Englisch (utf-8) wählen. Weitere Sprachen finden Sie im Downloadbereich unter dem Punkt Sprachpakete und können nach der Installation hier ausgewählt werden.

**$REX['MOD_REWRITE']**

Wollen Sie “sprechende Links”, die die entsprechenden Artikelnamen und nicht nur die Artikel_IDs in der URL anzeigen, müssen Sie für diese Variable “TRUE” einstellen.






<a name="sprachen"></a>
## Sprachen


<a name="mod_rewrite"></a>
## mod_rewrite
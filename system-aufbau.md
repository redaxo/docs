# Allgemeiner Aufbau / System

* [Terminologie](#terminologie)
* [Artikel und Kategorien](#artikel-kategorien)
* [Templates](#templates)
* [Module](#module)
* [Hauptmenüpunkte in REDAXO](#hauptmenupunkte)
* [Standard-AddOns in REDAXO](#standard-addons)

<a name="terminologie"></a>

## Terminologie

Wir verwenden in dieser Dokumentation die Begriffe Frontend und Backend. Das Backend ist der Verwaltungsbereich von REDAXO, in den man nach dem Einloggen in REDAXO gelangt. Das Backend ist erreichbar über die Adresse <http://www.domain.de/redaxo/.>
Das Frontend dagegen ist das, was der Besucher der Website zu sehen bekommt, also die von REDAXO generierten Seiten.

Jedes CMS hat seine eigene Terminologie, sodass Begriffe wie Template, Artikel oder Navigation in den einzelnen Systemen unterschiedliches bedeuten können.

<a name="artikel-kategorien"></a>

## Artikel und Kategorien

In REDAXO legt man einzelne HTML-Seiten als Artikel oder als Kategorie an. Kategorien nutzt man üblicherweise dann, wenn man eine hierarchische Struktur schaffen will. Kategorien sind also wie Ablagefächer oder Ordner, sodass man mehrstufige Navigationen im Normalfall mit Kategorien aufbauen wird.

Artikel dagegen sind der Container für Inhalt - quasi das Blatt Papier, das Texte oder Bilder enthält. Artikel bieten sich also eher an, wenn man hierarchisch gleichwertige Seiten anlegen will, zum Beispiel einen auf mehrere Seiten aufgeteilten Text zum Weiterblättern. Man muss sich Kategorien und Artikel einfach als zwei unterschiedliche Wege vorstellen, um in REDAXO Seiten anzulegen und Navigationen zu schaffen.

<a name="templates"></a>

## Templates

Dass überhaupt Inhalte wie Texte oder Bilder auf einer HTML-Seite erscheinen, steuert das Template. Das Template wirkt sich nur auf die Frontend-Ausgabe aus; dort wird üblicherweise die HTML-Struktur der Website, die eingebundenen CSS- und Javascript-Dateien hinterlegt, aber auch einige PHP-Befehle, die die Inhalte des jeweiligen Artikels auslesen. Sofern man mit mehreren Inhaltsbereichen (auch Spalten oder ctypes genannt) arbeitet, kann man in einem Template beliebig viele dieser "Bereiche" anlegen. Bei der Pflege eines Artikels erscheinen daraufhin im REDAXO-Backend Links, um in den jeweiligen Bereich zu wechseln und dort Inhalte hinzuzufügen.

<a name="module"></a>

## Module

Die Inhalte selbst werden in REDAXO mit Modulen gepflegt. Diese Module können - im Gegensatz zu den meisten anderen CMS - sehr leicht selbst erstellt und erweitert werden, um sie dem jeweiligen Anwendungszweck perfekt anpassen zu können. Man kann - in jedem Inhaltsbereich - beliebig viele dieser Module auf einer Seite untereinander setzen. Module lassen sich optional nur bestimmten Templates und/oder bestimmten Bereichen und/oder bestimmten Kategorien zuweisen.

Zusammenfassend muss man sich den Aufbau und die Ausgabe einer einzelnen Seite in REDAXO also folgendermaßen vorstellen:

* Das **Template** bildet den Rahmen, quasi die Matrize für einen Artikel und steuert das Aussehen sowie die Struktur der Seite. Auch eine Navigation würde man normalerweise in einem Template speichern.
* Der **Artikel** dient als Container zum Verwalten der Inhalte, ggf. in Bereichen. Diese Inhalte pflegt man üblicherweise über Module. Um artikelspezifische Informationen zu verwalten, eignen sich dagegen die sogenannten Metafelder - typische Beispiele wären etwa ein Headerbilder oder HTML-Metatags wie Description oder Opengraph.
* **Module** dienen meist zur Pflege von Texten und Bildern. Module werden in einem Artikel als Blöcke beliebig untereinander gesetzt und bestehen aus einem Ein- und einem Ausgabebereich. Der Eingabebereich wird nur im Backend angezeigt und enthält Felder, um Texte eingeben und Bilder auswählen zu können. Der Ausgabebereich wird im Backend und vor allem im Frontend, also für den Besucher sichtbar und zeigt diese Texte und Bilder an der im Template definierten Position an. Da Module als einzelne Blöcke mehrfach verwendet werden können, kann man eine Seite beliebig erweitern.

Die üblichen Schritte zur Erstellung einer neuen Webseite mit REDAXO wären folgende:

* Erstellen eines oder mehrerer Templates
* Definition der Kategorien und Artikel
* Erstellen eines Stylesheets (CSS-Datei)
* Zuweisung der seitenspezifischen Inhalte zu den Artikeln mit selbst definierten Modulen
* Festlegung eines Startartikels. Der als Erstes angelegte Artikel wird automatisch der Startartikel. Man kann diese jedoch ändern unter dem Menüpunkt "System".

<a name="hauptmenupunkte"></a>

## Hauptmenüpunkte in REDAXO

* **Struktur:** Dies ist die Einstiegsseite nach dem Login und der eigentliche Verwaltungsbereich für die Seitenstruktur und Inhalte
* **Medienpool:** der Bereich dient zur Verwaltung von allen Dateien (Medien), die vom Redakteur auf den Server geladen werden: Bilder, PDF, Word-Dokumente, etc.
* **Templates:** wichtig für den Entwickler. Templates speichern den HTML-Rahmen der Webseite.

* **Module:** wichtig für Entwickler: Hier entstehen die Module, mit denen die Redaktion die Inhalte pflegt.
* **Benutzer:** In diesem Bereich erstellt der Administrator weitere Benutzer-Logins und steuert deren jeweilige Rechte.
* **AddOns:** sind besondere Erweiterungen für REDAXO, die man sich wie kleine Applikationen vorstellen muss. Beispiele wären etwa eine Suche, ein Gästebuch oder ein Mechanismus zum Erzeugen von schönen URLs. AddOns können auch weitere Hauptmenüpunkte oder Systemfunktionen hinzufügen.
* **System:** Auf dieser Seite kann man einige der während der Installation getätigten Einstellungen noch nachträglich ändern, zum Beispiel den Servernamen oder die Error-E-Mail-Adresse. Ebenso kann man aber dort den Startartikel, das Standard-Template oder den "Fehler-Artikel" festlegen, der bei einer fehlerhaft eingegebenen URL angezeigt werden soll. Ein sehr wichtiger Punkt im Systembereich ist die Mehrsprachigkeit für das Frontend - man kann hier unkompliziert beliebig viele Sprachen anlegen. Und ein System-Log informiert über eventuelle Fehler.
* **Installer:** AddOns lassen sich hier direkt online neu installieren oder bestehende updaten. Selbst der REDAXO-Code selbst kann upgedatet werden.

<a name="standard-addons"></a>

## Standard-AddOns in REDAXO

* **Backup:** Hier kann man Backup-Sicherungen der Website erstellen und auch wieder zurückspielen.
* **Media Manager:** Diese REDAXO-Funktion dient für Bildanpassungen und kann Bildbearbeitungsketten ausführen. Vom Redakteur hochgeladene Bilder können beispielsweise verkleinert, beschnitten, geschärft und mit einem Wasserzeichen überlagert werden.
* **Meta Infos:** Mit Meta-Infos kann man spezifische Felder für Artikel, Kategorien, Medien und Sprachen erstellen. Während die Module Datenbank-Felder für Inhalte bereitstellen, wird man in **Artikel-Metafeldern** zum Beispiel Headerfotos speichern, ob eine Seite zugangsgeschützt sein soll oder ob sie einer Zeitsteuerung unterliegen soll. **Kategorie-Metafelder** werden analog gern für Zusatzfunktionen in Navigationen genutzt, um z. B. für Unterkategorien Teaser-Fotos und -Texte zu verwalten. **Medien-Metafelder** könnte man beispielsweise einsetzen, um bei einem Bild Copyright-Hinweise zu vermerken. **Sprach-Metafelder** eignen sich zum Beispiel für das Datumsformat der jeweiligen Sprache.

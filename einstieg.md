# Einstieg in Redaxo

REDAXO basiert auf PHP und MySQL. Kenntnisse in dieser Sprache und im Umgang mit der Datenbank sind zwar zu empfehlen, aber nicht unbedingt erforderlich. 

Die Flexibilität von REDAXO erlaubt es, weitergehende Anpassungen an spezielle Anforderungen problemlos vorzunehmen. Dies setzt dann allerdings PHP und/oder HTML/CSS-Kenntnisse voraus.

Viele Fragen und Probleme können mit Hilfe des **Forums** in **SLACK** oder dieser **Dokumentation** geklärt werden. 

## REDAXO-Begriffe

Bei der Arbeit mit Redaxo werden Ihnen die folgenden Begriffe immer wieder begegnen:

* Kategorie
* Artikel
* Template
* Modul
* Block/Slice

Sie werden hier kurz erläutert. Eine ausführliche Beschreibung findet man in den spezifischen Kapiteln zu den Begriffen.

## Frontend/Backend

Loginmaske
Bei der Arbeit mit einem CMS unterscheidet man zwischen dem Frontend und dem Backend. Das Frontend ist die für jeden sichtbare Internetseite. Das Backend ist der Bearbeitungsbereich für die Inhalte. Zu diesem gelangt man über folgende Adresse:

http://www.meine-adresse.tld/redaxo.

“www.meine-adresse.tld” ist durch die eigene Adresse der Webseite zu ersetzen. Es erscheint nun die Login-Maske für das Backend.

Backend
Nach erfolgreichem Einloggen gelangt man in das Backend. Alles, was nun in dieser Doku beschrieben wird, spielt sich hier ab.

--

## Erstellen einer Webseite mit REDAXO 

Wenn man REDAXO auf seinem Server [installiert](/{{path}}/{{version}}/installation) hat und nun eine Webpräsentation erstellen möchte, sind die folgenden Schritte durchzuführen. Diese Beschreibung ist nur eine Kurzfassung. Die Details sind in den Folgekapiteln dieser Dokumentation beschrieben.

**Schritte zur Erstellung einer Webseite mit REDAXO**

1. [Definition der Kategorien und Artikel](#defkatart)
2. [Erstellen eines Templates](#template)
3. [Erstellen eines Stylesheets](#styles)
4. [Zuweisung der seitenspezifischen Inhalte zu den Artikeln](#zuweisung)
5. [Festlegung eines Startartikels](#startartikel)


<a name="defkatart"></a>**1. Definition der Kategorien und Artikel**

Die einzelnen Seiten einer Präsentation werden bei REDAXO Artikel genannt. Diese müssen unter der [Strukturverwaltung] erzeugt und benannt werden. Zur besseren Gliederung und um die Navigation zu steuern, können Artikel unterschiedlichen Kategorien zugewiesen werden. Dazu definiert man zunächst die Kategorie und legt dann in den Kategorien die zugehörigen Artikel an.

<a name="template"></a>
**2. Erstellen eines Templates**

Damit ein Artikel angezeigt werden kann, braucht er ein [Template](/{{path}}/{{version}}/templates), das ihm zugewiesen wird. Ein Template legt das Layout des Artikels fest. Templates werden in der eigenen Rubrik Templates definiert und gespeichert. Die Zuweisung zu einem Artikel erfolgt in der Strukturverwaltung. Dazu muss das Template als aktiv gekennzeichnet sein.

<a name="styles"></a>
**3. Erstellen eines Stylesheets**

Üblicherweise wird die komplette Formatierung einer Webseite in einem Stylesheet ausgelagert. Das wird auch für die Arbeit mit REDAXO empfohlen. Das Stylesheet wird – wie sonst auch in HTML-Seiten – in den head-Bereich des Templates eingebunden.

Beispiel für das Einbinden eines Stylesheets in ein Redaxo-Template:

	<link rel="stylesheet" type="text/css" href="/assets/css/main.css" media="screen" />

<a name="zuweisung"></a>
**4. Erstellen der seitenspezifischen Inhalte für einen Artikel**

Die Seiteninhalte werden in einzelnen Blöcken (auch Slices genannt) eingegeben. Die Anzahl der Blöcke auf einer Seite ist beliebig. Bei dem Anlegen eines Blocks müssen Sie ein Modul auswählen, mit dem der Block editiert werden soll. Module sind Minitemplates, die den jeweiligen Inhaltsbereich formatieren. Die Eingabe von Inhalten mittels Modulen erleichtert die Einhaltung eines durchgängigen Layouts.

Nach der Installtion von REDAXO sind noch keine [Module](/{{path}}/{{version}}/module) enthalten. Erste Module findet man in den DEMOS im Installer und in den weiteren dort gelistetetn Addons. 

<a name="startartikel"></a>
**5. Festlegung eines Startartikels**

Wenn diese Schritte erledigt sind, das heißt: die Struktur ist festgelegt, Templates und Stylesheet sind erstellt und zugewiesen und die Blöcke der Artikel sind mit Inhalten gefüllt, muss nur noch ein Startartikel für die Webpräsenz festgelegt werden. Dies geschieht unter der Rubrik “System”.  Hier kann über die Linkmap der gewünschte Startartikel selektiert & übernommen werden. Danach klickt man auf „ändern“, um die neue Einstellung zu speichern. Wenn jetzt Ihre URL aufgerufen wird, wird der ausgewählte Artikel als Startartikel angezeigt.


>**Anmerkung** Diese Beschreibung gibt die einzelnen Arbeitsschritte nur in groben Zügen wieder, um einen kurzen Überblick zu geben.

> Die detaillierten Informationen zu jedem einzelnen Schritt findet man in den weiteren Kapiteln dieser Dokumentation.

Im Tutoral [Quickstart: Website in 15 Minuten] findet man eine kurze Anleitung zum Aufbau einer Webpräsenz mit REDAXO. 

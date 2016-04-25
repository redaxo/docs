# Einstieg in Redaxo

REDAXO basiert auf PHP und MySQL. Kenntnisse in dieser Sprache und im Umgang mit der Datenbank sind zwar zu empfehlen, aber nicht unbedingt erforderlich. Wenn Sie sich die mitgelieferte Demo ansehen, können Sie anhand dieses Beispiels lernen, Webseiten mit Redaxo zu erstellen.

Die Flexibilität von REDAXO erlaubt es Ihnen, weitergehende Anpassungen an spezielle Anforderungen problemlos vorzunehmen. Dies setzt dann allerdings PHP und/oder HTML/CSS-Kenntnisse voraus.

Viele Fragen und Probleme können mit Hilfe des **Forums**, des **Wikis** oder dieser **Dokumentation** bearbeitet werden. Sie können hier auf einen umfangreichen Fundus an Problemlösungen zurückgreifen.

## REDAXO-Begriffe

Bei der Arbeit mit Redaxo werden Ihnen die folgenden Begriffe immer wieder begegnen:

* Kategorie
* Artikel
* Template
* Modul
* Block/Slice

Sie werden hier kurz erläutert. Eine ausführliche Beschreibung finden Sie dann in den spezifischen Kapiteln zu den Begriffen.

## Frontend/Backend

Loginmaske
Bei der Arbeit mit einem CMS unterscheidet man zwischen dem Frontend und dem Backend. Das Frontend ist die für jeden sichtbare Internetseite. Das Backend ist der Bearbeitungsbereich für die Inhalte. Zu diesem gelangt man über folgende Adresse:

http://www.meine-adresse.tld/redaxo.

“www.meine-adresse.tld” ist durch die eigene Adresse der Webseite zu ersetzen. Es erscheint nun die Login-Maske für das Backend.

Backend
Nach erfolgreichem Einloggen gelangen Sie in das Backend. Alles, was nun in dieser Doku beschrieben wird, spielt sich hier ab.

--

### Erstellen einer Webseite mit REDAXO (Blanko-Version)

Wenn man REDAXO ohne Demo-Versionen auf seinem Server installiert hat und nun eine Webpräsentation erstellen möchte, sind die folgenden Schritte durchzuführen. Diese Beschreibung ist nur eine Kurzfassung. Die Details sind in den Folgekapiteln beschrieben.

**Schritte zur Erstellung einer Webseite mit REDAXO**

1. [Definition der Kategorien und Artikel](#defkatart)
2. [Erstellen eines Templates](#template)
3. [Erstellen eines Stylesheets](#styles)
4. [Zuweisung der seitenspezifischen Inhalte zu den Artikeln](#zuweisung)
5. [Festlegung eines Startartikels](#startartikel)



<a name="defkatart"></a>**1. Definition der Kategorien und Artikel**

Die einzelnen Seiten einer Präsentation werden bei REDAXO Artikel genannt. Diese müssen unter der Rubrik Struktur erzeugt und benannt werden. Zur besseren Gliederung und um die Navigation zu steuern, können die Artikel unterschiedlichen Kategorien zugewiesen werden. Dazu definiert man zunächst die Kategorie und legt dann in den Kategorien die zugehörigen Artikel an.

<a name="template"></a>**2. Erstellen eines Templates**

Damit ein Artikel angezeigt werden kann, braucht er ein Template, das ihm zugewiesen wird. Ein Template ist eine html-Datei ohne seitenspezifischen Inhalt. Es legt das Layout des Artikels fest. Templates werden in der eigenen Rubrik Templates definiert und gespeichert. Die Zuweisung zu einem Artikel erfolgt in der Rubrik Struktur. Dazu muss das Template als aktiv gekennzeichnet sein.

<a name="styles"></a>**3. Erstellen eines Stylesheets**

Üblicherweise wird die komplette Formatierung einer Webseite in einem Stylesheet ausgelagert. Das wird auch für die Arbeit mit REDAXO empfohlen. Das Stylesheet wird – wie sonst auch in html-Seiten – in den head-Bereich des Templates eingebunden.

Beispiel für das Einbinden eines Stylesheets in ein Redaxo-Template:

	<link rel="stylesheet" type="text/css" href="<?php echo $REX['HTDOCS_PATH'] ?>files/main.css" media="screen" />

<a name="zuweisung"></a>**4. Erstellen der seitenspezifischen Inhalte für einen Artikel**

Die Seiteninhalte werden in einzelnen Blöcken (auch Slices genannt) eingegeben. Die Anzahl der Blöcke auf einer Seite ist beliebig. Bei dem Anlegen eines Blocks müssen Sie ein Modul auswählen, mit dem der Block editiert werden soll. Module sind Minitemplates, die den jeweiligen Inhaltsbereich formatieren. Die Eingabe von Inhalten mittels Modulen erleichtert die Einhaltung eines durchgängigen Layouts.

Bei der Blanko-Version von REDAXO sind noch keine Module enthalten. Sie können aber aus der Demoversion oder von der Download-Seite für Module übernommen werden.

<a name="startartikel"></a>**5. Festlegung eines Startartikels**

Wenn die genannten Schritte erledigt sind, das heißt, die Struktur ist festgelegt, Templates und Stylesheet sind erstellt und zugewiesen und die Blöcke der Artikel sind mit Inhalten gefüllt, dann brauchen Sie nur noch einen Startartikel zu benennen. Dies geschieht unter der Rubrik “System”. Standardmäßig ist der Artikel mit der Artikel-ID 1 als Startartikel vorgesehen. Hier können Sie über die Linkmap (siehe unten) den gewünschten Startartikel selektieren & übernehmen. Danach müssen Sie auf „ändern“ klicken, um die neue Einstellung zu speicher. Wenn nun Ihre URL aufgerufen wird, wird der ausgewählte Artikel als Startartikel angezeigt.


>**Anmerkung** Diese Beschreibung gibt die einzelnen Arbeitsschritte nur in groben Zügen wieder, um Ihnen erstmal einen Überblick zu geben.

> Die detaillierten Informationen zu jedem einzelnen Schritt finden Sie in den speziellen Kapiteln zu diesen Themen.

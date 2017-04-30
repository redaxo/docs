# Einstieg

## Erstellen einer Webseite mit REDAXO 

Wenn man REDAXO auf seinem Server [installiert](/{{path}}/{{version}}/installation) hat und eine Webpräsenz erstellen möchte, sind die folgenden Schritte durchzuführen. Diese Beschreibung ist nur eine Kurzfassung. Die Details sind in den Folgekapiteln dieser Dokumentation beschrieben.

**Schritte zur Erstellung einer Webseite mit REDAXO**

1. [Erstellen eines Templates](#template)
2. [Definition der Kategorien und Artikel](#defkatart)
3. [Zuweisung der seitenspezifischen Inhalte zu den Artikeln](#zuweisung)
4. [Festlegung eines Startartikels](#startartikel)


<a name="template"></a>
**1. Erstellen eines Templates**

Damit ein Artikel angezeigt werden kann, braucht er ein [Template](/{{path}}/{{version}}/templates), das ihm zugewiesen wird. Ein Template legt das Layout des Artikels fest. Templates werden in der eigenen Rubrik Templates definiert und gespeichert. Die Zuweisung zu einem Artikel erfolgt in der Strukturverwaltung. Dazu muss das Template als aktiv gekennzeichnet sein. Zur Auslagerung von Stylesheets und Javascript-Dateien bietet sich der /assets-Ordner an.
Siehe: [Templates](/{{path}}/{{version}}/templates)


<a name="defkatart"></a>
**2. Definition der Kategorien und Artikel**

Die einzelnen Seiten einer Präsentation werden bei REDAXO Artikel genannt. Diese müssen unter der [Strukturverwaltung] erzeugt und benannt werden. Zur besseren Gliederung und um die Navigation zu steuern, können Artikel unterschiedlichen Kategorien zugewiesen werden. Dazu definiert man zunächst die Kategorie und legt dann in den Kategorien die zugehörigen Artikel an.
Siehe: Strukturverwaltung](/{{path}}/{{version}}/strukturverwaltung)


<a name="zuweisung"></a>
**4. Erstellen der seitenspezifischen Inhalte für einen Artikel**

Die Seiteninhalte werden in einzelnen **Blöcken** (auch Slices genannt) eingegeben. Die Anzahl der Blöcke auf einer Seite ist beliebig. Bei dem Anlegen eines Blocks müssen Sie ein Modul auswählen, mit dem der Block editiert werden soll. Module sind Minitemplates, die den jeweiligen Inhaltsbereich formatieren. Die Eingabe von Inhalten mittels Modulen erleichtert die Einhaltung eines durchgängigen Layouts.

Nach der Installtion von REDAXO sind noch keine [Module](/{{path}}/{{version}}/module) enthalten. Erste Module findet man in den DEMOS im Installer und in den weiteren dort gelistetetn Addons. 

Mehr Informationen im Kapitel: [Redaktion](/{{path}}/{{version}}/redaktion)

<a name="startartikel"></a>
**5. Festlegung eines Startartikels**

Wenn diese Schritte erledigt sind, das heißt: die Struktur ist festgelegt, Templates und Stylesheet sind erstellt und zugewiesen und die Blöcke der Artikel sind mit Inhalten gefüllt, muss nur noch ein Startartikel für die Webpräsenz festgelegt werden. Dies geschieht unter der Rubrik “System”.  Hier kann über die Linkmap der gewünschte Startartikel selektiert & übernommen werden. Danach klickt man auf „ändern“, um die neue Einstellung zu speichern. Wenn jetzt Ihre URL aufgerufen wird, wird der ausgewählte Artikel als Startartikel angezeigt.


Die detaillierten Informationen zu jedem einzelnen Schritt findet man in den weiteren Kapiteln dieser Dokumentation.

> Im Tutoral [Quickstart: Website in 15 Minuten](/{{path}}/{{version}}/tutorial-quickstart) findet man eine kurze Anleitung zum Aufbau einer Webpräsenz mit REDAXO. 

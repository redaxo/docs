# Einstieg

## Erstellen einer Webseite mit REDAXO

Ist die [Installation](/{{path}}/{{version}}/installation) von REDAXO abgeschlossen, kann man mit dem Aufbau der Webpräsenz beginnen. Hierzu müssen die folgenden Schritte durchgeführt werden. Diese Beschreibung ist nur eine Kurzfassung. Für detallierte Informationen sollten die weiteren Kapitel der Dokumentation betrachtet werden.

**Schritte zur Erstellung einer Webseite mit REDAXO**

1. [Erstellen eines Templates](#template)
2. [Definition der Kategorien und Artikel](#defkatart)
3. [Zuweisung der seitenspezifischen Inhalte zu den Artikeln](#zuweisung)
4. [Festlegung eines Startartikels](#startartikel)

<a name="template"></a>
**1. Erstellen eines Templates**

Damit ein Artikel angezeigt werden kann, braucht er ein [Template](/{{path}}/{{version}}/templates), das ihm im nächsten Schritt zugewiesen wird. Ein Template legt das Layout des Artikels fest. Templates werden in der eigenen Rubrik Templates definiert und gespeichert. Die Zuweisung zu einem Artikel erfolgt in der [Strukturverwaltung](/{{path}}/{{version}}/strukturverwaltung). Dazu muss das Template als aktiv gekennzeichnet sein. Zur Auslagerung von Stylesheets und Javascript-Dateien bietet sich der /assets-Ordner an.
Siehe: [Templates](/{{path}}/{{version}}/templates)

<a name="defkatart"></a>
**2. Definition der Kategorien und Artikel**

Die einzelnen Seiten einer Präsentation werden bei REDAXO Artikel genannt. Diese werden in der [Strukturverwaltung](/{{path}}/{{version}}/strukturverwaltung) erzeugt, benannt und mit TEMPLATES versehen. Zur besseren Gliederung und um die Navigation zu steuern, können Artikel unterschiedlichen Kategorien zugewiesen werden. Dazu definiert man zunächst die Kategorie und legt dann in den Kategorien die zugehörigen Artikel an.
Siehe: [Strukturverwaltung](/{{path}}/{{version}}/strukturverwaltung)

<a name="zuweisung"></a>
**3. Erstellen der seitenspezifischen Inhalte für einen Artikel**

Die Seiteninhalte werden in einzelnen **Blöcken** eingegeben. Die Anzahl der Blöcke auf einer Seite ist beliebig. Sie werden durch die installierten [Module](/{{path}}/{{version}}/module) in REDAXO zur Verfügung gestellt. Die Eingabe von Inhalten mittels Blöcken erleichtert die Einhaltung eines durchgängigen Layouts.

> Nach der Installation von REDAXO sind noch keine [Module](/{{path}}/{{version}}/module) vorhanden. Erste Module findet man in den Addons im [Installer](/{{path}}/{{version}}/installer).

Mehr Informationen im Kapitel: [Redaktion](/{{path}}/{{version}}/redaktion)

<a name="startartikel"></a>
**4. Festlegung eines Startartikels**

Wenn diese Schritte erledigt sind, das heißt: die Struktur ist festgelegt, Templates und Stylesheet sind erstellt und zugewiesen und die Blöcke der Artikel sind mit Inhalten gefüllt, muss nur noch ein ***Startartikel*** für die Webpräsenz festgelegt werden. Dies geschieht unter der Rubrik **“System”**.  Hier kann über der gewünschte Startartikel selektiert & übernommen werden. Danach klickt man auf „ändern“, um die neue Einstellung zu speichern. Wenn jetzt Ihre URL aufgerufen wird, wird der ausgewählte Artikel als Startartikel angezeigt und die Website kann betrachtet werden.

Die detaillierten Informationen zu jedem einzelnen Schritt findet man in den weiteren Kapiteln dieser Dokumentation.

> Im Tutoral [Quickstart: Website in 15 Minuten](/{{path}}/{{version}}/tutorial-quickstart) findet man eine kurze Anleitung zum schnellen Aufbau einer Webpräsenz inkl. Template und Modulen mit REDAXO.

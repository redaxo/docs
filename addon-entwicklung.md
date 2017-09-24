# AddOn Entwicklung

* [Minimale Erfordernisse](#anker-minimal)
* [package.yml](#anker-package-yml)
  * [Erforderliche Angabe](#anker-yaml-required)
  * [Optionale Angabe](#anker-yaml-optional)
* [Optionale Dateien](#anker-files)
* [Weitere nützliche Dateien](#anker-useful-files)
* [Optionale Ordner](#anker-folders)
* [Weitere nützliche Ordner](#anker-useful-folders)
* [Software](#anker-software)
* [Fragen und Antworten](#anker-faq)
  * [Mardown](#anker-faq-markdown)
  * [Yaml](#anker-faq-yaml)


Für die Entwicklung von AddOns gibt es behilfliche AddOns, eine Liste dazu kann auf dieser Seite unter
[Software](#anker-software) gefunden werden.

<a name="anker-minimal"></a>
## Minimale Erfordernisse
Jedes Addon hat einen eigenen Ordner mit einem einzigartigem und möglichst beschreibendem Namen.  
  
[@TODO:][SCREENSSHOT ORDNER]  
  
AddOns werden bei der Installation in Redaxo registriert, dazu sind einige Basisinformationen notwendig.
Diese Basisinformationen werden in der Datei "package.yml" abgelegt. Prinzipiell sind mit dieser Datei
alle Erfordernisse erfüllt, dass Redaxo ein Addon installieren kann.  
  
[@TODO:][SCREENSSHOT ODER CODE VON PACKAGE.YML]  
  
Da in der Datei "package.yml" direkt Referenzen zu Dateien innerhalb des Addons notiert werden können, können in
der Folge weitere Dateien notwendig werden. Mehr dazu erforderlichen und optionalen Angaben in dieser Datei
unter [package.yml](#anker-package-yml).

<a name="anker-package-yml"></a>
## package.yml

Die Datei "package.yml" ist die einzige und erforderliche Kernkomponente eines AddOns.  
Bei Bedarf können dort weitere Komponenten referenziert werden.

<a name="anker-yaml-required"></a>
### Erforderliche Angaben

Die einzigen erforderlichen Angaben innerhalb der Datei sind Folgende:
```
package: test
version: '1.0'
```
Die Werte müssen natürlich angepasst werden, die unbedingt erforderlichen Angaben sind somit "package" und "version".

<a name="anker-yaml-optional"></a>
### Optionale Angaben
@TODO

<a name="anker-files"></a>
## Optionale Dateien
Redaxo bearbeitet einige Ordner und Dateien in AddOns automatisch, darüber hinaus ist jeder Entwickler natürlich
frei, beliebige Datein in einem AddOn bereit zu stellen.  
Nachfolgend werden die Dateien und Ordner gelistet, nach denen innerhalb eines installierten AddOns von Redaxo automatisch gesucht wird:
* **help.php**  
  Ist eine Datei "help.php" im AddOn-Ordner enthalten wird diese automatisch im AddOn-Manager eingebunden und die Ausgabe angezeigt.  
  Ist die Datei nicht enthalten wird im AddOn-Manager ein Hinweis angezeigt, daß die Datei fehlt.  
  Es sollten Hinweise zur Funktionalität des Addons enthalten sein, auch Versionshinweise bzw. Changelog können angezeigt werden.
* **install.php**  
  Ist eine Datei "install.php" im AddOn-Ordner enthalten wird diese automatisch bei der AddOn-Installation ausgeführt.  
  Die dort integrierte Funktionalität kann viele Aktionen umfassen und ist dem Entwickler somit vollkommen freigstellt.  
  Übliche Aktionen umfassen das Erstellen von Ordnern, das Kopieren bzw. Erstellen von Dateien und Datenbankoperationen.
* **install.sql**  
  Ist eine Datei "install.sql" im AddOn-Ordner enthalten wird diese automatisch bei der AddOn-Installation ausgeführt.  
  Entwickler sollten sicherstellen, daß möglicherweise vorhandene Daten nicht überschrieben oder gelöscht werden.  
  Übliche Aktionen sind die Erstellung von Tabellen in der Datenbank, aber es können auch Daten eingefügt werden oder alle erdenklichen SQL-Befehle integriert werden.
* **update.php**  
  Ist eine Datei "update.php" im AddOn-Ordner enthalten wird diese automatisch bei einem AddOn-Update ausgeführt.  
  Auslöser für die Anzeige eines verfügbaren Updates ist die Version in der Datei "package.yml" im Vergleich zu der in einem Upload oder Download.
* **uninstall.php**  
  Ist eine Datei "uninstall.php" im AddOn-Ordner enthalten wird diese automatisch bei der AddOn-Deinstallation ausgeführt.  
  Übliche Aktionen sind das Löschen von Dateien und Ordnern die zum Cachen angelegt wurden.  
  Einige AddOns führen beim Deinstallieren auch Datenbankaktionen durch.  
  Ein Entwickler sollte berücksichtigen, daß ein Löschen von Daten trotz Deinstallation des AddOns ungewünscht sein kann.
* **boot.php**  
  Ist eine Datei "boot.php" im AddOn-Ordner enthalten wird diese automatisch bei jedem Aufruf des AddOns ausgeführt, dies
  bezieht sich auf Frontend und Backend.  
  Übliche Verwendungen sind die Definition von Variablen und die Einbindung von Dateien.  
  Funktionell kommt dieser Datei eine hohe Wichtigkeit zu, dennoch ist die Einbindung optional und nicht unbedingt notwendig.
* **README.md**  
  Der Inhalt der Datei "README.md" wird durch Redaxo im AddOn-Manager ausgegeben, wenn die Datei "help.php" nicht vorhanden ist.  
  Ausserdem empfiehlt sich diese Datei, wenn das AddOn als Repository auf GitHub gehostet wird.

<a name="anker-useful-files"></a>
##Weitere nützliche Dateien
* **LICENSE.md**  
  Eine automatische Nutzung durch Redaxo ist nicht gegeben, allerdings empfiehlt sich diese Datei, wenn das AddOn als Repository auf GitHub gehostet wird.  
  Ausserdem ist natürlich der Zweck der Datei, über die Lizenz des AddOns zu informieren auch innerhalb von Redaxo wichtig,
  selbst wenn eine automatische Anzeige nicht vorgesehen ist.
* **CHANGELOG.md**  
  Eine automatische Nutzung durch Redaxo ist nicht gegeben, allerdings empfiehlt sich diese Datei, wenn das AddOn als Repository auf GitHub gehostet wird.  
  Ausserdem ist natürlich der Zweck der Datei, über Änderungen zwischen Versionen des AddOns zu informieren auch innerhalb von Redaxo wichtig,
  selbst wenn eine automatische Anzeige nicht vorgesehen ist.
* **config.yml**  
  Eine Datei "config.yml" kann einfach eingelesen werden und an gewünschter Stelle im AddOn eingebunden werden.  
  Hier können umfangreiche Definitionen notiert werden, das AddOn "markitup" ist ein gutes Beispiel.  
  Da das Einlesen der Datei nicht automatisch geschieht, ist die Namensgebung nicht festgelegt. Somit könnt man auch z.B. folgende Dateien anlegen:
  ```
  config_frontend.yml
  config_backend.yml
  ```
  Der PHP-Code um eine Datei einzulesen lautet beispielsweise:
  ```
  $markItUpButtons = rex_file::getConfig(rex_path::addon('markitup', 'config.yml'));
  ```
  
<a name="anker-folders"></a>
## Optionale Ordner
@TODO  

<a name="anker-useful-folders"></a>
## Weitere nützliche Ordner
@TODO

<a name="anker-software"></a>
## Software
@TODO  

<a name="anker-faq"></a>
## Fragen und Antworten
<a name="anker-faq-markdown"></a>
**Mardown**
* **Welches Dateiformat haben Dateien mit der Endung ".md" ?**  
  Dateien mit der Endung "md" enhalten Inhalt in der MarkDown-Syntax.  
  Es handelt sich dabei um normalen Text, der mit einigen wenigen Mitteln für eine formatierte Ausgabe vorbereitet werden kann.  
  Mehr Details dazu hier: [Wikipedia:Markdown](https://de.wikipedia.org/wiki/Markdown)
* Was ist der Unterschied zwischen MarkUp und MarkDown?  
  @TODO  
* Was ist der Unterschied zwischen MarkUp und MarkItUp?  
  @TODO  
* **Warum wird die Markdown-Syntax in so vielen Dateien verwendet, geht das nicht in Text-Dateien?**  
  Mardown hat sich zum defacto-Standard entwickelt, da es auf gihub.com verwendet wird, wo auch viele Redaxo-AddOns verwaltet werden.
  Auch innerhalb von Redaxo findet das Format in einigen optional installierbaren Editoren Verwendung.  
  Markdown erlaubt die Integration von Bildern und Hyperlinks, wie auch die lesefreundliche Formatierung von Text, und hat
  dem einfachen Text-Format gegenüber eine Menge Vorteile.
* **Warum wird die Markdown-Syntax in so vielen Dateien verwendet, geht das nicht im HTML-Format?**  
  Mardown hat sich zum defacto-Standard entwickelt, da es auf gihub.com verwendet wird, wo auch viele Redaxo-AddOns verwaltet werden.
  Auch innerhalb von Redaxo findet das Format in einigen optional installierbaren Editoren Verwendung.    
  Die Bereitstellung von Inhalten per HTML ist durchaus möglich und jedem freigestellt, allerdings tauchen dort Gestaltungsfragen auf,
  die bei Markdown nicht gegeben sind. HTML ist bei den Optionen umfangreicher aber auch schwieriger zu erlernen.
  Das Format Markdown stellt limitierte Bereicherungen für Dateien bereit, die gerne für Standard-Dateien wie README, LICENSE und CHANGELOG
  verwendet werden und zuvor üblicherweise als reine Text-Dateien bereitgestellt wurden.
* **Wo gibt es eine Erklärung zum Markdown-Standard?**  
  Eine Beschreibung in englischer Sprache vom Autor des Standards findet man hier: [Mardown:Syntax](https://daringfireball.net/projects/markdown/syntax).  
  [@TODO: besseren Link] Eine deutschsprachige Beschreibung vom Redaxo-Team findet man hier: [Mardown:Vorlage](https://redaxo.org/doku/master/_vorlage).  
* **Wo findet man die Backticks zur Auszeichnung von Kode in Markdown-Dateien?**  
  * Es handelt sich bei dem Backtick um den französischen Akzent "Gravis".
    Auf einer deutschen Tastatur findet man diesen rechts neben den Ziffern und dem "ß".
	Man drückt die Tasten "Umschalten" und die Akzent-Taste gleichzeitig und anschließend die Leerzeichen Taste.  
	[@TODO: Screenshot Keyboard mit markierten Tasten]
  * In manchen Editoren braucht man die Backticks nicht selbst zu schreiben, sondern kann sie über Buttons einfügen.  
    Es gibt auch spezielle Editoren für Mardown-Dateien.
  * Eine etwas umständliche, aber letztendlich einfache Methode ist, das Zeichen in einer Datei abzuspeichern und zu kopieren.  
    Meistens kann das Zeichen in SQL-Dateien oder fertigen Markdown-Dateien gefunden werden, hier kann das Zeichen natürlich auch kopiert werden, bitteschön: **`**
* **Welche Editoren für Markdown kann das Redaxo-Team empfehlen?**  
  * **Frei verfügbare Markdown-Editoren:**  
    @TODO  
  * **Kommerzielle Markdown-Editoren:**    
    @TODO  

<a name="anker-faq-yaml"></a>
**Yaml**
* **Welches Dateiformat haben Dateien mit der Endung ".yml" ?**  
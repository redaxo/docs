#  Templates
- [Über](#ueber)
- [Erstellen eines Templates](#ertellen)
- [Spalten  (CTYPES)](#ctype)
- [Kategorieberechtigungen](#catrights)
- [Ausgabe der Inhalte](#ausgabe)
- [Einbindung von Templates](#einbindung)
- [Einbindung von Artikeln](#artikeleinbindung)
- [Das aktuelle Template in Modulen abfragen.](#aktuelles-template)
- [Beispiele](#beispiele)
	- [Template mit nur einer Spalte](#1spalte)
	- [Erweitertes Template mit 2 Spalten, eingebundenem Template und Artikel](#2spalte)
	

<a name="ueber"></a>
## Über
Mit Hilfe von Templates wird das Layout der Artikel  festgelegt.

Redakteure wählen die zur Verfügung stehenden Templates bei der Erstellung eines Artikels aus. Templates definieren die generelle HTML-Struktur einer Artikelausgabe und binden die erforderlichen externen Dateien wie Stylesheets und Javascripte ein. Die Templates geben außerdem den Inhalt des Artikels auf der Website aus.

Templates können verschachtelt angelegt werden. Dadurch kann man Komponenten wie Header, Footer oder Navigation in eigene "Sub"-Templates auslagern, die im Haupt-Template eingebunden werden. Templates unterstützen PHP-Code und die [REDAXO-Variablen](/{{path}}/{{version}}/redaxo-variablen). 

<a name="erstellen"></a>
## Erstellen eines Templates
Templates werden im Menüpunkt `Templates` erstellt. 
Ein neues Template wird über das (+)-Symbol angelegt. Man legt einen Namen fest und definiert, ob das Template aktiv geschaltet werden soll. Im darauf folgenden Feld `Template` wird der eigentliche Code eingepflegt. 

<a name="ctype"></a>
## Spalten  (CTYPES) 
Eine Spalte oder auch `CTYPE` unterteilt in REDAXO ein Template in unterschiedlich voneinander getrennte Pflegebereiche. In den meisten Fällen sind dies tatsächlcih "Spalten", also z.B. Hauptspalte und Seitenspalte. CTYPES kann man aber auch ganz allgemein für Contentbereiche verwenden, wie Header, Slider, etc.

Spalten werden im Reiter `Spalten` angelegt und darin mit einem Namen versehen. Es ist dort auch möglich, für jede  Spalte festzulegen, welche Module in der Spalte verwendet werden dürfen. Denn es kann durchaus, dass ein Redakteur in Hauptspalte bestimmte Module benutzen darf, in der Seitenspalte dagegen nicht.

<a name="catrights"></a>
## Kategorieberechtigungen 
Die Verwendung eines Templates kann auf festgelegte Kategorien der Struktur eingeschränkt werden. Die Einstellung hierzu findet man im Reiter `Kategorieberechtigungen` der Template-Verwaltung. Dadurch kann der Administrator z.B. definieren, dass in bestimmten Kategorien nur ein einspaltiges Template verwendet, in anderen dagegen auch ein zweispaltiges.

<a name="ausgabe"></a>
## Ausgabe der Inhalte 
Die Artikelinhalte werden Wahlweise über die REDAXO-Variablen oder durch deren PHP-Alternativen ausgegeben. Die nachfolgenden Beispiele zeigen die Ausgabe der Inhalte über REDAXO-Variablen. Der Titel der Seite wird hier dagegen über PHP ausgelesen. In Templates können jedoch alle in REDAXO zur Verfügung stehenden REDAXO-Variablen und öffentliche Klassen und Funktionen verwendet werden. Ausführliche Informationen zu den Variablen findet man  im Kapitel [REDAXO-Variablen](/{{path}}/{{version}}/redaxo-variablen). 

<a name="einbindung"></a>
## Einbindung von Templates
Einige Bestandteile möchte man gegebenenfalls in mehreren Templates nutzen. Hierzu kann man einzelne Bestandteile der Struktur in andere Templates auslagern. Diese Templates können bestimmte Abschnitte oder Funktionen liefern, beispielsweise eine Navigation oder eine PHP-Funktion. 

Templates, die inkludiert werden sollen, sollen im Normalfall nicht den Redakteuren zur Verfügung stehen, daher sollte man sie in der Template-Verwaltung inaktiv schalten. Durch diese Einschränkung kann das Template dass nicht als Seiten-Template für einen Artikel ausgewählt werden.

Die Einbindung dieser inkludierten Templates erfolgt über die REDAXO-Variable REX_TEMPLATE und der ID des gewünschten Templates.
Beispiel: `REX_TEMPLATE[2]` 

<a name="artikeleinbindung"></a>
## Einbindung von Artikeln
In Templates können auch Artikel eingebunden werden. Das ermöglicht den Redakteuren, zum Beispiel einen Abschnitt des Templates selbst zu pflegen. Das können etwa eine immer darzustellende Liste der Öffnungszeiten sein oder eine feste Linkliste, die auf allen Seiten sichtbar sein soll. Die Einbindung erfolgt über die REDAXO-Variable `REX_ARTICLE` oder über den entprechenden PHP-Gegenpart.
Beispiel: `REX_ARTICLE[3]` 

<a name="aktuelles-template"></a>
## Aktuelles Template in Modulen abfragen
Manchmal ist es erforderlich, in Modulen das aktuell verwendete Template zu ermitteln und so die Ausgabe oder die Eingabe zu beeinflussen. Ein Beispiel könnte sein, dass ein Modul dem Redakteur in einem Einspalte-Template mehr Subspalten anbieten soll als wenn es in einem Zweispalten-Template verwendet wird. Diese Information erhält man über die REDAXO-Variable `REX_TEMPLATE_ID`.

<a name="beispiele"></a>
## Beispiele 
Die nachfolgenden Beispiele zeigen zwei einfache Templates, um mit dem Aufbau einer Website zu beginnen. 

<a name="1spalte"></a>
### Template mit nur einer Spalte
In diesem Beispiel wird der gesamte Artikelinhalt ungeachtet einer Spaltendefinition im DIV-Container mit der CSS-Klasse `.content` mittels der REDAXO-Variable `REX_ARTICLE[]` ausgegeben. Der Titel der Seite wird per PHP ausgelesen. 

```PHP
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title><?php echo htmlspecialchars($this->getValue('name')); ?></title>
    <link href="/assets/css/mein.css" rel="stylesheet">
</head>
<body>
    <div class="content">
    REX_ARTICLE[]
    <footer class="footer">
    <p>&copy;  Company, Inc.</p>
    </footer>
    </div> 
</body>
</html>
```

<a name="2spalte"></a>
### Erweitertes Template mit 2 Spalten, eingebundenem Template und Artikel
In diesem Beispiel werden Inhalte getrennt nach ihren Spalten ausgegeben. So könnte etwa eine Content-Spalte und eine Sidebar (Seitenspalte) gepflegt werden.

Über das eingebundene Template werden außerdem die Inhalte eines anderen Templates eingebunden, beispielsweise ein Brotkrumenpfad im Headerbereich. 
Zuletzt werden im Footer die Inhalte eines anderen Artikels ausgegeben.

Die Ausgabe der einzelnen Spalten erfolgt über die REDAXO-Variablen `REX_ARTICLE[ctype=1]` und `REX_ARTICLE[ctype=2] `.  Der Parameter `ctype` legt hierbei die ID der gewünschten Spalte fest. 
Die ID der jeweiligen Spalten findet man im Reiter `Spalten`. 


```PHP
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title><?php echo htmlspecialchars($this->getValue('name')); ?></title>
    <link href="/assets/css/mein.css" rel="stylesheet">
</head>
<body>
   REX_TEMPLATE[2]
   <div class="content">
   REX_ARTICLE[ctype=1]
   </div>  
   <div class="sidebar">
   REX_ARTICLE[ctype=2]
   </div> 
   <footer class="footer">
   REX_ARTICLE[3]
   </footer>
   </div> 
</body>
</html>
```



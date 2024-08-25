# Templates

* [Über](#ueber)
* [Erstellen eines Templates](#erstellen)
* [Content-Bereiche (C-Types)](#ctype)
* [Kategorieberechtigungen](#catrights)
* [Ausgabe der Inhalte](#ausgabe)
* [Einbindung von Templates](#einbindung)
* [Einbindung von Artikeln](#artikeleinbindung)
* [Das aktuelle Template in Modulen abfragen.](#aktuelles-template)
* [Beispiele](#beispiele)
  + [Template mit nur einem Bereich](#1bereich)
  + [Erweitertes Template mit 2 Bereichen, eingebundenem Template und Artikel](#2bereiche)

 
<a name="ueber"></a>

## Über

Mithilfe von Templates wird das Layout der Artikel festgelegt.

Redakteure wählen die zur Verfügung stehenden Templates bei der Erstellung eines Artikels aus. Templates definieren die generelle HTML-Struktur einer Artikelausgabe und binden die erforderlichen externen Dateien wie Stylesheets und Javascripte ein. Die Templates geben außerdem den Inhalt des Artikels auf der Website aus.

Templates können verschachtelt angelegt werden. Dadurch kann man Komponenten wie Header, Footer oder Navigation in eigene "Sub"-Templates auslagern, die im Haupt-Template eingebunden werden. Templates unterstützen PHP-Code und die [REDAXO-Variablen](/{{path}}/{{version}}/redaxo-variablen).

<a name="erstellen"></a>

## Erstellen eines Templates

Templates werden im Menüpunkt `Templates` erstellt.

Ein neues Template wird über das (+)-Symbol angelegt. Man legt einen Namen und Schlüssel (key) fest und definiert, ob das Template aktiv geschaltet werden soll. Im darauf folgenden Feld `Template` wird der eigentliche Code eingepflegt.

<a name="ctype"></a>

## Content-Bereiche  (C-Types)

Ein Content-Bereich (oder auch Content-Spalte, bzw. `C-Type`) unterteilt in REDAXO ein Template in unterschiedlich voneinander getrennte Pflegebereiche. In den meisten Fällen sind dies "Spalten", also z. B. Hauptspalte und Seitenspalte. C-Types kann man aber auch ganz allgemein für Content-Bereiche verwenden, wie Header, Slider, etc.

Content-Bereiche werden im Reiter `Bereiche (ctypes)` angelegt und darin mit einem Namen versehen. Es ist dort auch möglich, für jeden Bereich festzulegen, welche Module in dem Bereich verwendet werden dürfen. Denn es kann durchaus sein, dass ein Redakteur in Hauptspalte bestimmte Module benutzen darf, in der Seitenspalte dagegen nicht.

<a name="catrights"></a>

## Kategorieberechtigungen

Die Verwendung eines Templates kann auf festgelegte Kategorien der Struktur eingeschränkt werden. Die Einstellung hierzu findet man im Reiter `Kategorieberechtigungen` der Template-Verwaltung. Dadurch kann der Administrator z. B. definieren, dass in bestimmten Kategorien nur ein einspaltiges Template verwendet, in anderen dagegen auch ein zweispaltiges.

<a name="ausgabe"></a>

## Ausgabe der Inhalte

Die Artikelinhalte werden wahlweise über die REDAXO-Variablen oder durch deren PHP-Alternativen ausgegeben. Die nachfolgenden Beispiele zeigen die Ausgabe der Inhalte über REDAXO-Variablen. Der Titel der Seite wird hier dagegen über PHP ausgelesen. In Templates können jedoch alle in REDAXO zur Verfügung stehenden REDAXO-Variablen und öffentliche Klassen und Funktionen verwendet werden. Ausführliche Informationen zu den Variablen findet man  im Kapitel [REDAXO-Variablen](/{{path}}/{{version}}/redaxo-variablen).

<a name="einbindung"></a>

## Einbindung von Templates

Einige Bestandteile möchte man gegebenenfalls in mehreren Templates nutzen. Hierzu kann man einzelne Bestandteile der Struktur in andere Templates auslagern. Diese Templates können bestimmte Abschnitte oder Funktionen liefern, beispielsweise eine Navigation oder eine PHP-Funktion.

Templates, die inkludiert werden sollen, sollen im Normalfall nicht den Redakteuren zur Verfügung stehen, daher sollte man sie in der Template-Verwaltung inaktiv schalten. Durch diese Einschränkung kann das deaktivierte Template nicht als Seiten-Template für einen Artikel durch den Redakteur ausgewählt werden.

Die Einbindung dieser inkludierten Templates erfolgt über die REDAXO-Variable REX_TEMPLATE und dem Schlüssel(Key) oder ID des gewünschten Templates.

Beispiel (Ausgabe im HTML-Bereich): `REX_TEMPLATE[key=haupt]` oder `REX_TEMPLATE[2]` 

Innerhalb von PHP-Tags wird das Template so eingebunden: `echo 'REX_TEMPLATE[key=haupt]';` oder `echo 'REX_TEMPLATE[2]';` 

> Durch Schlüssel sind Templates leichter übertagbar in andere Präsenzen. Die Anpassung der IDs bei Projekten wo bereits Templates bestehen entfällt.

<a name="artikeleinbindung"></a>

## Einbindung von Artikeln

In Templates können auch Artikel eingebunden werden. Das ermöglicht den Redakteuren, zum Beispiel einen Abschnitt des Templates selbst zu pflegen. Das können etwa eine immer darzustellende Liste der Öffnungszeiten sein oder eine feste Linkliste, die auf allen Seiten sichtbar sein soll. Die Einbindung erfolgt über die REDAXO-Variable `REX_ARTICLE` oder über den entsprechenden PHP-Gegenpart.
Beispiel: `REX_ARTICLE[3]` 

<a name="aktuelles-template"></a>

## Aktuelles Template in Modulen abfragen

Manchmal ist es erforderlich, in Modulen das aktuell verwendete Template zu ermitteln und so die Ausgabe oder die Eingabe zu beeinflussen. Ein Beispiel könnte sein, dass ein Modul dem Redakteur in einem Einspalte-Template mehr Subspalten anbieten soll, als wenn es in einem Zweispalten-Template verwendet wird. Diese Information erhält man über die REDAXO-Variable `REX_TEMPLATE_ID`.

<a name="beispiele"></a>

## Beispiele

Die nachfolgenden Beispiele zeigen zwei einfache Templates, um mit dem Aufbau einer Website zu beginnen.

<a name="1bereich"></a>

### Template mit nur einem Bereich

In diesem Beispiel wird der gesamte Artikelinhalt ungeachtet einer Spaltendefinition im DIV-Container mit der CSS-Klasse `.content` mittels der REDAXO-Variable `REX_ARTICLE[]` ausgegeben. Der Titel der Seite wird per PHP ausgelesen.

``` PHP
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

<a name="2bereiche"></a>

### Erweitertes Template mit 2 Bereichen, eingebundenem Template und Artikel

In diesem Beispiel werden Inhalte getrennt nach ihren Bereichen ausgegeben. So könnte etwa eine Content-Spalte und eine Sidebar (Seitenspalte) gepflegt werden.

Über das eingebundene Template werden außerdem die Inhalte eines anderen Templates eingebunden, beispielsweise ein Brotkrumenpfad im Header-Bereich mit dem Schlüssel `bradcrumb`.

Zuletzt werden im Footer die Inhalte eines anderen Artikels ausgegeben.

Die Ausgabe der einzelnen Bereiche erfolgt über die REDAXO-Variablen `REX_ARTICLE[ctype=1]` und `REX_ARTICLE[ctype=2]`.  Der Parameter `ctype` legt hierbei die ID des gewünschten Bereichs fest.
Die ID des jeweiligen Bereichs findet man im Reiter `Bereiche`.

``` php
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

    REX_TEMPLATE[key=breadcrumb]

    <div class="content">
        REX_ARTICLE[ctype=1]
    </div>  

    <div class="sidebar">
        REX_ARTICLE[ctype=2]
    </div>

    <footer class="footer">
        REX_ARTICLE[3]
    </footer>

</body>
</html>
```

#  Templates



## Über
Mit Hilfe von Templates wird das Layout der Artikel  festgelegt. 
Redakteure wählen die zur Verfügung stehenden Templates bei der Erstellung eines Artikels aus. Templates definieren die generelle HTML-Struktur einer Artikelausgabe und binden die erforderlichen externen Dateien wie Stylesheets und Javascripte ein. Die geben den Inhalt des Artikels auf der Website aus. Templates können verschachtelt angelegt werden. Dadurch kann man Komponenten wie Header, Footer oder Navigation in eigene Templates auslagern, die im Haupt-Template eingebunden werden. auch ist es möglich über Templates eigene PHP-Funktionen einzubinden. 


## Erstellen eines Templates
Templates werden im Bereich **Templates** erstellt. 
Ein neues Template wird über das (+)-Symbol angelegt. Man legt einen Namen fest und definiert ob das Template aktivgeschaltet werden soll. Im darauf folgenden Feld **Template** wird der eigentliche Code eingepflegt. 

## Spalten  (CTYPES) 
Eine Spalte oder auch CTYPE  unterteilt in REDAXO ein Template in unterschiedlich voneinander getrennte Pflegebereiche.  Spalten werden im Reiter ***Spalten*** angelegt und darin mit einem Namen versehen. Es ist dort auch möglich für jede  Spalte festzulegen, welche Module darin verwendet werden dürfen.   

## Ausgabe der Inhalte 
Die Artikelinhalte werden Wahlweise über die REDAXO-Variablen oder durch deren PHP-Gegenparts ausgegeben.  Die nachfolgenden Beispiele zeigen die Ausgabe der Inhalte über REDAXO-Variablen. Der Titel der Seite wird hier über PHP ausgelesen. Ausführliche Informationen hierzu im Kapitel [REDAXO-Variablen](/redaxo-variablen). 

## Einbindung von Templates
Einige Bestandteile möchte man ggf. in mehreren Templates nutzen. Hierzu kann einzelne Bestandteile der Struktur in andren Templates auslagern. Diese Templates können bestimmte Abschnitte oder Funktionen liefern, beispielsweise eine Navigation oder eine PHP-Funktion. 
Templates, die inkludiert werden sollen, sollen nicht den Redakteuren zur Verfügung stehen, daher sollte man sie in der Templateverwaltung inaktiv schalten. Die Einbindung dieser Templates erfolgt über die REDAXO-Variable REX_TEMPLATE und die ID des gewünschten Templates.
z.B.: `REX_TEMPLATE[2]` 

## Einbindung von Artikeln
In Templates können auch Artikel eingebunden werden. Das ermöglicht den Redakteuren ggf. einen Abschnitt des Templates selbst zu pflegen. Das können beispielsweise eine immer darzustellende Liste der Öffnungszeiten sein oder eine feste Linkliste die auf allen Seiten zu sehen sein sollen. Die Einbindung erfolgt über die REDAXO_VARIABLE REX_ARTICLE oder über den entprechenden PHP-Gegenpart.  
z.B.: `REX_ARTICLE[3]` 

## Das aktuelle Template in Modulen abfragen. 
Manchmal ist es erforderlich in Modulen das aktuell verwendete Template zu ermitteln und so die Ausgabe oder die Eingabe zu beeinflussen. Diese Information erhält man über die REDAXO-Variable REX_TEMPLATE_ID.


## Beispiele 
Die nachfolgenden Beispiele ze

### Template mit nur einer Spalte
In diesem Beispiel wird der gesamte Artikelinhalt ungeachtet einer Spaltendefinition Im DIV mit der CSS-Class .content mittels der REDAXO-Variable  `REX_ARTICLE[]` ausgegeben. Der Titel der Seite wird per PHP ausgelesen. 

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


### Erweitertes Template mit 2 Spalten, eingebundenem Template und Artikel
In diesem Beispiel werden Inhalte getrennt nach ihren Spalten ausgegeben. In diesem Fall können eine Content-Spalte und eine Sidbar gepflegt werden. Über das eingebundene Template werden Inhalte eines anderen Templates eingebunden. Im Footer werden Inhalte eunes Artikels ausgegeben. 
Die Ausgabe der einzelnen Spalten erfolgt über die REDAXO-Variablen `REX_ARTICLE[ctype=1] ` und `REX_ARTICLE[ctype=2] `.  Der Parameter `ctype` legt hierbei die ID der gewünschten Spalte fest. 
Die ID der jeweiligen Spalten findet man im Reiter Spalten. 


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







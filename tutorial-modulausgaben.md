# Modulausgaben erweitern - REDAXO Variablen

Neben der einfachen Verwendung der REDAXO Variablen gibt es nützliche Erweiterungen für die Ausgabe der Modul-Eingaben. Die Übergabe von Werten zwischen der Eingabe und Ausgabe in Modulen erfolgt in der Regel so:

**Eingabe**

```HTML
<input type=text size=50 name=VALUE[1] value="REX_VALUE[1]">
```
**Ausgabe**

```HTML 
REX_VALUE[1]
```

**Das gleiche Ergebnis erhält man über:**

```HTML 
REX_VALUE[id="1"]
```

Nun kann man fehlende Eingaben und damit fehlerhafte Ausgaben z.B mit Aktionen bei der Eingabe überprüfen.

Will man die Ausgabe überprüfen und korrigieren, so kann man das über PHP, aber eben auch mit den erweiterten Möglichkeiten der REDAXO-Variablen:

```HTML
REX_VALUE[id="1" prefix="<h1>" suffix="</h1>" ifempty="Keine Headline"]
```

Ist die Eingabe leer wird der String “Keine Headline” ausgeben. Dazu wird vor der Eingabe ( oder des String ifempty ) der String von prefix und nach der Eingaben der String von suffix eingesetzt.

Ein Übersicht von möglichen “Handlern” bei den unterschiedlichen REDAXO Variablen:


```PHP
REX_VALUE[id="1" prefix="" suffix="" instead="" ifempty="" callback=""]

REX_LINK_BUTTON[id="" category=""]
REX_LINK[id="" prefix="" suffix="" instead="" ifempty="" callback=""]

REX_LINKLIST_BUTTON[id="" category=""]
REX_LINKLIST[id="" prefix="" suffix="" instead="" ifempty="" callback=""]


REX_TEMPLATE[id="" prefix="" suffix="" instead="" ifempty="" callback=""]
REX_ARTICLE[id="" prefix="" suffix="" instead="" ifempty="" callback=" ctype=""]
REX_CATEGORY[id="" prefix="" suffix="" instead="" ifempty="" callback=""]


REX_MEDIA_BUTTON[id="" category="" preview=""]
REX_MEDIA[id="" prefix="" suffix="" instead="" ifempty="" callback=" mimetype=""]

REX_MEDIALIST_BUTTON[id="" category=""]
REX_MEDIALIST[id="" prefix="" suffix="" instead="" ifempty="" callback=""]

```

In Kombination mit dem Meta-Infos-AddOn kann man die “Handler” auch erweitern, zum Beispiel:

```REX_ARTICLE[spaltenname]
```

## Beispiel Verwendung Callback

```PHP 
<?php 
function toUpper($str) {
return strtuoupper($str["subject"]);
}
?>

REX_VALUE[id="1" callback="toUpper"]
```



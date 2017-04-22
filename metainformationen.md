# Metainformationen
- [Über](#ueber)
- [Anwendungsbeispiel](#beispiel)
- [Meta Infos-AddOn](#addon)
- [Metafelder](#metafelder)
- [Feldattribute](#attribute)
- [Dynamische Metafelder](#dynamik)
- [Auslesen der Meta Infos](#auslesen)
	- [Artikel](#artikel)
	- [Kategorien](#kategorien)
	- [Medien](#medien)
	- [Sprachen](#sprachen)
- [Für AddOn-Developer](#developer)
	
<a name="ueber"></a>
## Über

REDAXO bietet die Möglichkeit, für jeden Artikel, jede Kategorie, jede Sprache spezifische Meta-Angaben bereitzustellen. Das können zum Bespiel Definitionen für die Hintergrunddarstellung eines Artikels sein, Einstellungen für Galerien, Downloads oder zusätzliche SEO-Angaben sein.  

Metadaten sind beschreibende Daten von Artikeln, Kategorien, Sprachen oder Medien. Über das System AddOn „MetaInfos“ (SystemAddOns sind immer in einer Standard REDAXO Installation vorhanden und können nicht gelöscht werden) lassen sich diese Daten erweitern.

Man kann darüber Felder in der Verwaltung hinzufügen. Neben einfachen Textfeldern, lassen sich auch die Linkmap und auch Datenbankabfragen verwenden, um eigene spezielle Werte einbauen zu können. Ein typischen Fall ist das Erweitern der Media-Metadaten mit einem Feld „Copyright“, oder bei den Kategorien ein Feld mit „Kategoriegrafik“. Diese Werte können können mittels PHP oder [REDAXO-Variablen]((/{{path}}/{{version}}/redaxo-variablen)) abgerufen werden.  

<a name="besipiel"></a>
## Anwendungsbeispiel

Möchte man eine Seite so aufbauen, dass Sie in manchen Artikeln nur eine Spalte und in anderen zwei Spalten verwenden will, kann eine Auswahl per Metainfos bereitgestellt werden. Das erspart die Verwendung oder Programmierung zusätzlicher Templates. 
Man leget unter MetaInfo (Artikel) ein Select mit den Optionen 1-spaltig, 2-spaltig an. Dieses Merkmal muß dann bei den Artikeln entsprechend selektiert werden. Im Template selbst wird dann das Merkmal “ein- oder zweispaltig” abgefragt und danach ggf. eine weitere Spalte ergänzt.

<a name="addon"></a>
## Meta Infos-AddOn

Im Meta Infos-Addon können die Metafelder für Artikel, Kategorien, Medien und Sprachen definiert und gestaltet werden.  
 Meta Infos  sind dafür vorgesehen, seiten- oder medienspezifische Informationen zu verwalten, wie beispielsweise Suchmaschinen-Keywords, ein individuelles Headerbild, ob als Newsteaser berücksichtigt, ob sie in bestimmten Navigationen auftauchen soll, Copyright-Infos zu bestimmten Fotos, usw. Sie können Metainfo-Felder für Artikel, Kategorien und/oder Medien definieren. Als Felder stehen alle üblichen Typen wie text, textarea, select, radio, checkbox und mehr zur Verfügung. 
 
 

 <a name="metafelder"></a>
## Metafelder

Die nachfolgenden Felder stehen zur Auswahl: 

* **Text:**  Einfaches einzeiliges Textfeld 
*  **textarea:** Mehrzeiliges Textfeld 
*  **select:** Formular-Auswahlmenü
*  **radio:** Radio-Buttons
*  **checkbox:** Checkbox-Feld 
*  **REX_MEDIA_WIDGET:** Auswahlfeld für ein Medium aus dem Medienpool
*  **REX_MEDIALIST_WIDGET:**  Auswahlfeld für mehrere Medien aus dem Medienpool
*  **REX_LINK_WIDGET:** Auswahlfeld für einen Artikel der Webpräsenz
*  **REX_LINKLIST_WIDGET:** Auswahlfeld für mehrere Artikel der Webpräsenz
* **date:** Datumsfeld
* **datetime:** Datums und Uhrzeit-Feld
* **time:** Auswahlfeld für eine Urhzeit
* **legend:** Dient zur Gruppierung der Metadaten in Fieldsets

<a name="attribute"></a>
## Feldattribute 
 
 Die Felder können über Attribute gestaltet und auch in den Rechten eingeschränkt werden. 

``` 
style="color:red;" multiple="multiple" class="my_css_class" perm="admin[]"
```

Über `perm="admin[]`ist es so z.B. möglich ein Feld nur dem Admin zur Verfügung zu stellen. 

<a name="dynamik"></a>
## Dynamische Metafelder

Select–, Checkbox– und Radio–Felder können mit Daten von Datenbanktabellen befüllt werden und diese zur Auswahl bereitgestellt werden. Der Abruf ist aus beiden in REDAXO möglichen Datenbanken möglich. 

**Mögliche Query-Abfragen**
a) SELECT label,id FROM my_table WHERE a=4
b) (DB2) SELECT label,id FROM my_table WHERE a=4

<a name="auslesen"></a>
## Auslesen der Meta Infos

<a name="artikel"></a>
### Artikel
Artikel-Metadaten werden vom Redakteur im Reiter Metadaten eines Artikels eingepflegt.   Die Daten können per PHP wie folgt ausgelesen werden: 

```
// Beispiel Titelbild
$titleimage  =  $this->getValue ('art_titleimage');
// oder: 
$titleimage  =  rex_article::getCurrent()->getValue('art_titleimage');
```

Die Daten können auch mittels REDAXO-Variable ausgelesen werden. 

```
REX_ARTICLE[field="art_titleimage"]
```

<a name="kategorien"></a>
### Kategorien

Kategorie-Metadaten werden von den Redakteuren in der Strukturverwaltung gepflegt.  Sie können per PHP mit folgenden Befehlen wie folgt ausgelesen werden: 


```PHP
// Metadaten der aktuellen Kategorie
rex_category::getCurrent()->getValue($field) 
// Metadaten eine bestimten Kategorie anhand der Kategorie-ID
rex_category::getId($id)->getValue($field)
```

**Beispiele:**

```PHP
$hintergrund = rex_category::getCurrent()->getValue('cat_background');
```
#### Abruf als REDAXO-Variable
```
// Kurze Schreibweise, Aktuelle Kategorie
REX_CATEGORY[cat_background]
// Ausführliche Schreibweise, beliebige Kategorie
REX_CATEGORY[id=i field=cat_background] 
REX_CATEGORY[id=i field=cat_background clang=i]
```


<a name="medien"></a>
### Medien
Metadaten für Medien werden in den Eigenschaften eines Mediums im Medienpool gepflegt. 

Die Medien-Metadaten können per PHP wie folgt ausgelesen werden. 

```PHP
// Datensatz des Mediums anhand des Dateinamens auslesen
$media = rex_media::get('dateiname.xyz');
// Meta-Info auslesen
$file_name = $media->getValue('med_copyright');
```

#### Abruf als REDAXO-Variable
Variante als REDAXO-Variable, hier wird die Meta Info eines Mediums des Media-Widgets ausgegeben. 
```
REX_MEDIA[id=i field=copyright]
```
<a name="sprachen"></a>
### Sprachen
Die Metadaten zur jeweiligen Sprache werden im System zu jeder Sprache eingepflegt. 
Die Metadaten für Sprachen erhält man per PHP wie folgt: 

```PHP
// Auslesen einer Meta Info der aktuellen Sprache
rex_clang::getCurrent()->getValue($field) 
// Auslesen der Meta Info einer bestimmten Sprache anhand der Sprach ID
rex_clang::getId($id)->getValue($field)
```

**Beispiel:**

```PHP
rex_clang::getCurrent()->getValue('clang_setlocale'));
```
#### Abruf als REDAXO-Variable

```
REX_CLANG[field=clang_setlocale]
REX_CLANG[id=2 field=clang_setlocale]
```
<a name="developer"></a>


## Für AddOn-Developer

Wenn ein Addon neue Meta-Felder benötigt, können diese bei der Installation mit der Funktion rex_metainfo_add_field hinzugefügt werden:

### Funktion

```PHP 
rex_metainfo_add_field($title, $name, $priority, $attributes, $type, $default, $params = null, $validate = null, $restrictions = '')
```
### Beispiel

```PHP
rex_metainfo_add_field('Nicht in der Copyrightliste ausgeben', 'med_no_copyright_out', '3','','5','','','','');
```

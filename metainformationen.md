# Metainformationen

## Über

REDAXO bietet die Möglichkeit, für jeden Artikel, jede Kategorie, jede Sprache spezifische Meta-Angaben bereitzustellen. Das können zum Bespiel Definitionen für die Hintergrunddarstellung eines Artikels sein, Einstellungen für Galerien, Downloads oder zusätzliche SEO-Angaben sein.  

Metadaten sind beschreibende Daten von Artikeln, Kategorien oder Medien. Über das System AddOn „MetaInfos“ (SystemAddOns sind immer in einer Standard REDAXO Installation vorhanden und können nicht gelöscht werden) lassen sich diese Daten erweitern.

Man kann darüber Felder in der Verwaltung hinzufügen. Neben einfachen Textfeldern, lassen sich auch die Linkmap und auch Datenbankabfragen verwenden, um eigene spezielle Werte einbauen zu können. Ein typischen Fall ist das Erweitern der Media-Metadaten mit einem Feld „Copyright“, oder bei den Kategorien ein Feld mit „Kategoriegrafik“. Diese Werte können wie die schon vorhandenen Metadaten wie „Name“ über nachfolgende Codes abgerufen werden.  

**Bei Kategorie-Meta Infos**

```PHP 
<?php echo $this->getValue("cat_name"); ?>
```
**Bei Artikel-Meta Infos**

```PHP 
<?php echo $this->getValue("art_name“); ?>
```

## Meta Infos-AddOn

Im Meta Infos-Addon können die Metafelder für Artikel, Kategorien, Medien und Sprachen definiert und gestaltet werden.  
 Meta Infos  sind dafür vorgesehen, seiten- oder medienspezifische Informationen zu verwalten, wie beispielsweise Suchmaschinen-Keywords, ein individuelles Headerbild, ob als Newsteaser berücksichtigt, ob sie in bestimmten Navigationen auftauchen soll, Copyright-Infos zu bestimmten Fotos, usw. Sie können Metainfo-Felder für Artikel, Kategorien und/oder Medien definieren. Als Felder stehen alle üblichen Typen wie text, textarea, select, radio, checkbox und mehr zur Verfügung. 
 
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

## Beispiele

### Artikel

### Kategorien

### Medien

### Sprachen


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

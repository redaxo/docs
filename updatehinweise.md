# Update von REX 3.x auf REX 4.0

## Datenbank


Die Datenbanktabellen wurde verändert. 
Im Setup kann ein Update der Datenbank automatisiert durchgeführt werden.
**Wichtig dabei ist, dass man zuvor die komplette Seite sichert!**

Beim Setup werden die vorhandenen Tabellenstrukturen an die neue Version 4 angepasst. Es werden jedoch nicht die vorhandenen Tabelleninhalte verändert, so dass bestimmte Angaben in den Templates, Modulen und so weiter von Hand angepasst werden müssen. Dabei sind folgende Punkte zu beachten.

## Templates
	
	alte Schreibweise, um ein Template einzubinden:
	<?php include($REX['INCLUDE_PATH'] .'/generated/templates/2.template'); ?>
	
	neue Schreibweise:
	// innerhalb von PHP Tags
	$navTemplate = new rex_template(2); 
	include $navTemplate->getFile();
	
	// ausserhalb von PHP Tags
	REX_TEMPLATE[2]

**CTYPES**

Alle Ctypes sind nun via Backend zu verwalten. 
Die Datei ctype.inc.php wurde komplett entfernt!
Ctypes können nun pro Template hinterlegt werden.

## Allgemeines

$REX['INCLUDE_PATH'], $REX['MEDIAFOLDER'] sind jetzt absolute Pfade!

**Umbenennungen** 

* Dateien:
	* function_rex_modrewrite.inc.php => function_rex_url.inc.php

* Klassen/Methoden/Funktionen:
	* Alte Klassenbezeichnung ab nun NICHT mehr verwenden!

* Klassen:

	* login => rex_login,
	* sql => rex_sql,
	* article => rex_article

* Methoden:

	* sql::query() => sql::setQuery(),
	* sql::get_array() => sql::getArray(),
	* sql::resetCounter() => sql::reset(),
	* sql::nextValue() => sql::next(),
	* sql::where() => sql::setWhere()

* Attribute:

	* sql->select => sql->query

* Funktionen:

	* title => rex_title(),
	* getUrlById => rex_getUrl()

* Rückwärtskompatibilität eingeschränkt durch Bugfixes

	*  OOCategory::getArticles()
		* 1. Parameter $ignore_offlines default-Wert von True auf False geändert.
* OOMediaCategory::getRootCategories()
	* 1. Parameter $ignore_offlines entfernt, da es kein status bei Medienkategorien gibt

# Updatehinweise
- [Empfohlene Vorgehensweise](#empfohlen)
	- [Update per DIFF-Dateien](#diff)
- [Update von REX 3.x auf REX 4.0](#3x)

<a name="empfohlen"></a>

## Empfohlene Vorgehensweise 

Um ein Update von einer älteren Version auf eine neuere Version durchzuführen, sollte die neue Version immer eigenständig installiert werden. Das Überspielen der alten Version ist nicht ratsam.

*** Anleitung: ***

- Sichere ein Export der alten Seite
- Spiele die neue Version in einen leeren Ordner auf dem Server und installiere sie
- Importiere den Export der älteren Version

<a name="diff"></a>
## Update per DIFF-Dateien
Die Dateien aus den Versionen mit der des Downloads ersetzen.

**REX 4.6.1 auf REX 4.6.2**
[rex_diff_4.6.1_4.6.2.zip](/media/rex_diff_4.6.1_4.6.2.zip)

**REX 4.6.0 auf REX 4.6.1**
[rex_diff_4.6_4.6.1.zip](/media/rex_diff_4.6_4.6.1.zip)

**REX 4.x auf REX 4.6.x oder 4.7.x**

> Da sich seit der Version 4.6 ein Großteil an Dateien geändert hat, bieten wir dafür keine speziellen DIFF Dateien an.
Es wird empfohlen ein reguläres Setup durchzuführen. Vorher sollten von der bestehenden Webseite sowohl ein Datei- als auch Datenbankexport angefertigt werden.

**Updatehinweise von REX 4.3.x auf REX 4.5.1**

Bitte folgende Datei herunterladen:

[rex_diff_4.3.1_4.5.1.zip](/media/rex_diff_4.3.1_4.5.1.zip)

[rex_diff_4.3.2_4.5.1.zip](/media/rex_diff_4.3.2_4.5.1.zip)

[rex_diff_4.3.3_4.5.1.zip](/media/rex_diff_4.3.3_4.5.1.zip)

[rex_diff_4.4.0_4.5.1.zip](/media/rex_diff_4.4.0_4.5.1.zip)

[rex_diff_4.4.1_4.5.1.zip](/media/rex_diff_4.4.1_4.5.1.zip)

[rex_diff_4.5.0_4.5.1.zip](/media/rex_diff_4.5.0_4.5.1.zip)

Die Dateien aus den Versionen mit der des Downloads ersetzen.
Im Ordner /redaxo/include/lang alle Dateien die auf _utf8.lang enden löschen.

<a name="3x"></a>
## Update von REX 3.x auf REX 4.0

### Datenbank


Die Datenbanktabellen wurde verändert. 
Im Setup kann ein Update der Datenbank automatisiert durchgeführt werden.
**Wichtig dabei ist, dass man zuvor die komplette Seite sichert!**

Beim Setup werden die vorhandenen Tabellenstrukturen an die neue Version 4 angepasst. Es werden jedoch nicht die vorhandenen Tabelleninhalte verändert, so dass bestimmte Angaben in den Templates, Modulen und so weiter von Hand angepasst werden müssen. Dabei sind folgende Punkte zu beachten.

### Templates
	
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

### Allgemeines

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

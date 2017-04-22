# Module / Aktionen


- [Module / Aktionen](#module)
- [Modul erstellen](#modul_erstellen)
- [REDAXO-Variablen](#redaxo_variablen)
- [Aktionen](#aktionen)



<a name="module"></a>
## Module

Module werden bei REDAXO gebraucht, um die Artikel mit Inhalt zu füllen.

Module bestehen normalerweise aus zwei Teilen, einem Eingabe- und einem Ausgabebereich. Der Redakteur, der eine Seite bearbeitet, sieht nur den Eingabebereich. Im Ausgabeteil wird festgelegt, wie die Eingaben des Redakteurs im Frontend angezeigt werden sollen. Hier können die Eingaben bearbeitet, ergänzt und formatiert werden.

Wenn Sie zum Beispiel im Backend der Demo auf “Module” klicken, bekommen Sie die Liste der vorhandenen Module angezeigt.

Das Modul “Headline” ermöglicht die Eingabe eines Textes, der auf der Seite als Überschrift formatiert wird. Mit Hilfe des Moduls “Bildergalerie” gibt der Redakteur eine Auswahl von Bildern vor, die in einer Bildergalerie angezeigt werden. Das Modul “Text [textile]” verwendet das Redaxo-AddOn “Textile”.

Für die Speicherung der verschiedenen Inhalte werden REDAXO-eigene Variablen verwendet (s. Redaxo-Variablen).

Bei einer “blanko”-Installation von REDAXO ist die Liste der Module leer. Das heißt, Sie müssen die Module, die Sie brauchen, entweder selbst erstellen oder fertige Module aus der Demo oder dem Downloadbereich in Ihre installierte leere Version kopieren.

## Aktionen

Aktionen werden in Verbindung mit Modulen genutzt. Mit einer Aktion können die in einem Modul eingegebenen Variablenwerte bearbeitet werden. Es sind beliebige Operationen möglich. Wollen Sie zum Beispiel beim Editieren eines Blocks die Eingabe eines Textfeldes überprüfen, dann können Sie dies mit Hilfe einer Aktion tun. Die Eingabe kann, je nach Definition und Programmierung der Aktion, überprüft, korrigiert und verändert werden.

Die Definition und Funktionen einer Aktion erfolgt in einer einfachen Eingabemaske. Stehen Aktionen zur Auswahl, so wird bei der Erstellung oder Bearbeitung eines Moduls diese Auswahl angezeigt und kann dem Modul hinzugefügt werden.


<a name="modul_erstellen"></a>
## Modul erstellen

Im Downloadbereich finden Sie zahlreiche fertige Module zu den unterschiedlichsten Themen. Es gibt Module für Texteingaben, für das Erstellen von Formularen und Artikellisten, zum Einbinden von Bildergalerien und viele mehr. Sie können sich diese Module in Ihre eigene REDAXO-Installation kopieren und damit arbeiten.

Sollten Sie spezifische Module benötigen, die noch nicht fertig vorliegen, ist es empfehlenswert sich zunächst einmal die Module der Demo-Version anzusehen, um etwas über den sinnvollen Aufbau von Modulen und die Verwendung von REDAXO-Variablen zu erfahren.

Wollen Sie ein neues Modul anlegen, klicken Sie auf das kleine Plus-Zeichen oben links über der Modulliste. Es erscheint eine Maske mit drei Eingabefeldern jeweils für den Modulnamen, die Moduleingabe und die Modulausgabe. In der Moduleingabe legen Sie fest, wie die Eingabemaske im Backend aussieht und welche Daten vom Redakteur eingegeben werden sollen. In dem Feld für die Modulausgabe legen Sie fest, wie die eingegebenen Daten verarbeitet und im Frontend angezeigt werden.

Am besten lernen Sie die Module kennen, wenn Sie sie sich im Detail ansehen und damit arbeiten. Um das grundlegende Prinzip zu verdeutlichen, folgt hier ein Beispiel für ein ganz einfaches Modul:

Moduleingabe

```
Für die Eingabe wird ein Textfeld definiert, in dem ein kurzer Text eingegeben werden kann.

<input type="text" size="20" name="VALUE[1]" value="REX_VALUE[1]" />
```

Modulausgabe

```
Der Text wird als Überschrift wiedergegeben.

<h1>REX_VALUE[1]</h1>
```


<a name="redaxo_variablen"></a>
## REDAXO-Variablen

Die REDAXO-Variablen werden verwendet, um die Daten einer Seite, einer Kategorie oder Systemangaben zunächst in der Datenbank zu speichern und sie anschließend natürlich auch wieder auszulesen, auszuwerten und anzuzeigen.

Es wird zwischen folgenden Variablentypen unterschieden:

- Konstanten
- Variablen für die Moduleingabe
- Variablen für die Modulausgabe
- Variablen für Aktionen
- Variablen für Systemangaben

Sie werden hier zunächst einmal gelistet. Ein ausführlichere Beschreibung wird folgen.

**Konstanten**

- REX_ARTICLE[..]
- REX_ARTICLE_ ID
- REX_ARTICLE_VAR[..]
- REX_CATEGORY_ ID
- REX_CLANG_ ID
- REX_CTYPE_ID
- REX_MODULE_ID
- REX_SLICE_ID
- REX_TEMPLATE[..]
- REX_ TEMPLATE_ID
- REX_ USER
- REX_ USER_ID
- REX_ USER_LOGIN

**Variablen für die Moduleingabe**

- INPUT_HTML
- INPUT_PHP
- REX_ HTML
- REX_LINK_BUTTON[..]
- REX_LINKLIST_BUTTON[..]
- REX_MEDIA_BUTTON[..]
- REX_MEDIALIST_BUTTON[..]
- REX_ PHP
- VALUE[..]

**Variablen für die Modulausgabe**

- REX_ HTML
- REX_ HTML_VALUE[..]
- REX_IS_VALUE[..]
- REX_LINK[..]
- REX_LINK_ID[..]
- REX_LINKLIST[..]
- REX_MEDIA[..]
- REX_MEDIALIST[..]
- REX_ PHP
- REX_VALUE[..]

**Variablen für Aktionen**

- $REX_ACTION['ARTICLE_ID']
- $REX_ACTION['CLANG_ID']
- $REX_ACTION['CTYPE_ID']
- $REX_ACTION['EVENT']
- $REX_ACTION['HTML']
- $REX_ACTION['LINK'][..]
- $REX_ACTION['MEDIA'][..]
- $REX_ACTION['MEDIALIST'][..]
- $REX_ACTION['MSG']
- $REX_ACTION['MODULE_ID']
- $REX_ACTION['PHP']
- $REX_ACTION['SAVE']
- $REX_ACTION['SLICE_ID']
- $REX_ACTION['VALUE'][..]

**Variablen für Systemangaben ($REX)**

- $REX[‘ACKEY‘][..]
- $REX[‘ADDON‘][..]
- $REX[‘CLANG‘]
- $REX[‘CUR_CLANG‘]
- $REX[‘DB‘][..]
- $REX[‘ERROR_EMAIL‘]
- $REX[‘EXTPERM‘]
- $REX[‘EXTRAPERM‘]
- $REX[‘FILEPERM‘]
- $REX[‘GG‘]
- $REX[‘HTDOCS_PATH‘]
- $REX[‘INCLUDE_PATH‘]
- $REX[‘INSTNAME‘]
- $REX[‘LANG‘]
- $REX[‘MAXLOGINS‘]
- $REX[‘MEDIAFOLDER‘]
- $REX[‘MINOR_VERSION‘]
- $REX[‘MOD_REWRITE‘]
- $REX[‘MYSQL_VERSION‘]
- $REX[‘NOFUNCTIONS‘]
- $REX[‘NOTFOUND_ARTICLE_ID‘]
- $REX[‘PERM‘]
- $REX[‘PSWFUNC‘]
- $REX[‘REDAXO‘]
- $REX[‘RELOGINDELAY‘]
- $REX[‘SETUP‘]
- $REX[‘SERVER‘]
- $REX[‘SERVERNAME‘]
- $REX[‘SESSION_DURATION‘]
- $REX[‘START_ARTICLE_ID‘]
- $REX[‘START_CLANG_ID‘]
- $REX[‘START_PAGE‘]
- $REX[‘SUBVERSION‘]
- $REX[‘SYSTEM_ADDONS‘]
- $REX[‘TABLE_PREFIX‘]
- $REX[‘TEMP_PREFIX‘]
- $REX[‘VARIABLES‘]
- $REX[‘VERSION‘]
- $REX[‘USE_ETAG‘]
- $REX[‘USE_GZIP‘]
- $REX[‘USE_LAST_MODIFIED‘]
- $REX[‘USE_MD5‘]


<a name="aktionen"></a>
## Aktionen

Mit einer Aktion können die in einem Modul eingegebenen Variablenwerte bearbeitet werden. Es sind beliebige Operationen möglich. Wollen Sie zum Beispiel beim Editieren eines Blocks die Eingaben von Daten überprüfen, dann können Sie dies mit Hilfe einer Aktion tun. Die Eingaben können, je nach Definition und Programmierung der Aktion, überprüft, korrigiert und verändert werden.

Die Definition und Funktionen einer Aktion erfolgt in einer einfachen Eingabemaske. Alle Aktionen werden im Bereich “Aktionen” aufgelistet. Bei der Erstellung oder Bearbeitung eines Moduls wird diese Liste zur Auswahl angezeigt und kann dem Modul hinzugefügt werden.

Die Liste sehen Sie, wenn Sie im Bereich “Module” auf den Link “Aktionen” klicken.

**Aktionen erstellen oder bearbeiten**

Zum Erstellen einer neuen Aktion klicken Sie auf das kleine Pluszeichen oberhalb der Liste. Zum Bearbeiten einer vorhandenen Aktion klicken Sie auf deren Namen. Es erscheint eine Eingabemaske, die mehrere Möglichkeiten zur Bearbeitung bietet.


**Es gibt drei Arten von Aktionen**

**Preview-Action:**
Die Aktion wird vor dem Anzeigen des Moduls ausgeführt.

**Presave-Action:**
Die Aktion wird vor dem Speichern des Moduls ausgeführt.

**Postsave-Action:**
Die Aktion wird nach dem Speichern des Moduls ausgeführt.

**Jeder Aktion können bis zu drei Events zugewiesen werden**

**ADD:**
Ausführen beim Hinzufügen des Moduls

**EDIT:**
Ausführen beim Bearbeiten des Moduls

**DELETE:**
Ausführen beim Löschen des Moduls

Bei einer Preview-Action hat man nur die Möglichkeit, das Event “EDIT” auszuwählen. Bei Pre- oder Postsave Action hat man alle drei Wahlmöglichkeiten.

**Aktionen einem Modul zuweisen**

Bei der Erstellung oder Bearbeitung eines Moduls wird in der Bearbeitungsmaske eine Liste aller Aktionen angezeigt, die dem Modul nun zugewiesen werden können

**Beispiel: Mehr als 10 REX_VALUEs**

Dies ist ein Beispiel aus dem Downloadbereich, das für die Version 4.0 erstellt wurde. (Herzlichen Dank an Martin R. Findert für die ausführliche und hilfreiche Beschreibung.)

```
<?php
/* Neue Version der "rexname"-Action, laeuft mit REX 4.0.
Diese muss nur als Presave-Action fuer ADD und EDIT 
eingetragen werden. Anschliessend wird sie einem Modul 
zugeordnet. In diesem muss dann bei Eingabe UND Anzeige 
als erstes Folgendes stehen:
<?php $rexname = split('~~', ""); 
$GLOBALS['rexname'] = $rexname; ?>

Damit stehen im Modul die Variablen $rexname[0] bis 
$rexname[98] zur Verfuegung. kann dann in 
diesem Modul nicht mehr fuer andere Zwecke verwendet 
werden (natuerlich laesst sich auch jeder andere 
REX_VALUE verwenden). 
Achtung: Werte, die in $rexname[n] gespeichert werden, 
duerfen nicht den Substring '~~' enthalten!
*/


// Sicherheitsabfrage: sollte noch nicht beschrieben sein
if ($REX_ACTION['VALUE'][1] == '') {
$newname = "";
// Anlegen eines Strings mit 99 Feldern, durch ~~ getrennt
for ( $c = 0; $c < 99; $c++ ) {
// Pruefen von $rexname[0] bis $rexname[98] - sind sie gesetzt,
// dann werden sie im String abgelegt. Anderenfalls wird nur
// das naechste '~~' angehaengt.
if (isset($rexname[$c])) { 
$newname .= $rexname[$c] . '~~'; 
}
else {
$newname .= '~~'; 
}
}
// Der Gesamtstring wird in abgespeichert
$REX_ACTION['VALUE'][1] = $newname;
}
?>
```




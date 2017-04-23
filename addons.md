# AddOns

- [AddOn-Struktur](#struktur)
- [AddOns erstellen](#erstellen)
- [Import/Export](#import_export)
- [Textile](#textile)

AddOns erweitern den Funktionsumfang von REDAXO. Sie ermöglichen zum Beispiel den Import und Export von Daten, die Skalierung von Grafiken oder den Mailversand. Andere AddOns dienen zum Einbinden von Editoren wie dem Textile und dem TinyMCE.

**System-AddOns**

Mit der Version 4 werden die oben gelisteten AddOns bereits mitgeliefert und müssen nur noch installiert und aktiviert werden. 
Wie man in der Liste sieht, handelt es sich bei den AddOns “import_export” und “metainfo” um sogenannte System-AddOns. Das heißt, sie sind fester Bestandteil des REDAXO-Kerns und können deshalb auch nicht gelöscht werden.

**Installation zusätzlicher AddOns**

Für das Setup zusätzlicher AddOns aus dem Downloadbereich laden Sie die erforderlichen Dateien in das Verzeichnis “redaxo/include/addon/”. Danach sollte im Bereich AddOn das neue AddOn verfügbar sein. Klicken Sie dann erst “installieren” und danach “aktivieren”. Nach der Meldung “AddOn aktiviert” sollte das AddOn in der Navigation des REDAXO-Backends erscheinen. Für weitere Hinweise gibt es für jedes AddOn eine Hilfedatei, falls der geneigte Entwickler diese Möglichkeit genutzt hat.


<a name="struktur"></a>
## AddOn-Struktur

Wir zeigen hier am Beispiel des Import/Export-AddOns, wie ein AddOn im Allgemeinen aufgebaut ist. Die folgende Abbildung zeigt die Struktur der Ordner und Dateien, die zu diesem AddOn gehören.

Es gibt hier vier Dateien “config.inc.php”, “help.inc.php”, “install.inc.php” und “uninstall.inc.php”.

Weiterhin gibt es die Ordner “classes”, “files”, “functions”, “lang” und “pages”. 
Die Funktion der einzelnen Dateien und Ordner soll nun ausführlich erläutert werden.


###Die vier Dateien

**config.inc.php**

Konfigurieren Sie Ihr AddOn in dieser Datei. Hier werden Einstellungen für die Sprachdateien, ID und Name sowie die verwendeten Rechte geschrieben. Diese Datei wird bei jedem Aufruf einer Seite (sowohl im Backend als auch im Frontend) in den Workflow mit eingebunden (sofern das AddOn aktiviert und installiert ist). Dies ist also der richtige Platz, um zum Beispiel Extensions zu registrieren.

```
<?php

// Name des Addons:
$mypage = 'import_export'; // only for this file

// Nur im Backend:
if ($REX['REDAXO'])

// Sprachobjekt anlegen:
$I18N_IM_EXPORT = new i18n($REX['LANG'],$REX['INCLUDE_PATH'].'/addons/'. $mypage .'/lang'); // CREATE LANG OBJ FOR THIS ADDON

$REX['ADDON']['rxid'][$mypage] = '1'; // unique id /

// Anlegen eines Navigationspunktes im REDAXO Hauptmenu:
$REX['ADDON']['page'][$mypage] = $mypage; // pagename/foldername

// Namensgebung für den Navigationspunkt:
$REX['ADDON']['name'][$mypage] = 'Import/Export'; // name

// Berechtigung für das Addon definieren:
$REX['ADDON']['perm'][$mypage] = 'import[]'; // permission

$REX['ADDON']['version'][$mypage] = "0.9";

$REX['ADDON']['author'][$mypage] = "Jan Kristinus";

// $REX['ADDON']['supportpage'][$mypage] = "";


// Berechtigung in die Benutzerverwaltung einfügen:
$REX['PERM'][] = 'import[]';

?>
```

Die Instanz für die Sprachversion Ihres AddOns wird bei der Programmierung der Seiten verwendet. Hier: #$#I18N_IM_EXPORT

Falls nötig, können im o.g. Abschnitt auch mehrere Rechte für die Benutzerverwaltung definiert werden.

Dies kann beispielsweise so aussehen:

```
<?php

$REX['PERM'][] = "import[]";
$REX['PERM'][] = "export[]";
$REX['PERM'][] = "export[files]";
$REX['PERM'][] = "export[db]";

?>
```

**help.inc.php**

In diese Datei können Sie eine Beschreibung des AddOns, Hilfen und Tipps sowie Version und Autor schreiben. 
Die Texte können mittels html-Code formatiert werden.

Diese Seite erscheint, wenn auf der Seite “AddOn” das (?) eines AddOns angeklickt wird.

```
<b>Import Export</b>

<br /><br />
Dieses Addon dient zur Sicherung der Inhalte und der Medienpool Dateien des Internetaufritts.
<br />
Die extrahierten Daten können in einer beliebigen REDAXO Installation (gleicher Version) wieder importiert werden.
```

**install.inc.php**

Über diese Datei können Sie alle nötigen Schritte durchführen, die für die Installation des AddOn benötigt werden. Dazu können Module installiert, Ordner angelegt, MySQL-Tabellen erstellt oder Seiten regeneriert werden. Diese Datei wird nur einmalig bei der Installation des AddOns verwendet.

```
<?php

$REX['ADDON']['install']['import_export'] = 1;

/* 
ggf. Ausgabe einer Fehlermeldung:

ERRMSG IN CASE: $REX[ADDON][installmsg]["import_export"] = "Leider konnte nichts installiert werden da....";
*/

?>
```

**uninstall.inc.php**

Über diese Datei können Sie alle nötigen Schritte durchführen, die für die Deinstallation des AddOns benötigt werden. Hier können Tabellen entfernt, Dateien gelöscht oder Ursprungszustände wiederhergestellt werden.

```
<?php

$REX['ADDON']['install']['import_export'] = 0;

/*
ggf. Fehlermeldung:

ERRMSG IN CASE: $REX['ADDON']['installmsg']['import_export'] = "Deinstallation fehlgeschlagen weil...";

*/
?>
```

**Klassen (classes)**

Über eigene Klassen können Sie beliebige abstrakte oder reale Gegenstände/Dinge modellieren und diese so zur Erweiterung von REDAXO nutzen.

> Der Dateiname einer Klasse sollte folgendes Format besitzen:
class.rex_.inc.php


**Funktionen (functions)**

Funktionen dienen dazu, verschiedene logische Abschnitte zu gliedern. Sie stellen so sicher, dass keine doppelten Codesegmente im Quellcode auftauchen. Dies hilft, den Quelltext wartbar zu halten.

> Der Dateiname einer Funktion sollte wie folgt aufgebaut sein:
function_rex_.inc.php


**Sprachdateien (lang)**

Über die Sprachdateien können Sie Ihr AddOn für die verschiedenen Sprachversionen im Backend anbieten.
Jede Sprache erhält dazu ihre eigene Datei – hier zum Beispiel für Deutsch, Englisch und Polnisch. Es wird auch zwischen Iso- und utf8-Codierung unterschieden.

In diesen Dateien können für die Seite/n des AddOns verwendete Elemente wie Titel, Funktionen, Bezeichnungen o.ä. in der entsprechenden definiert werden. Dies ist zum Beispiel ein Auszug aus der Sprachdatei de_de_utf8.lang.

```
# addon:import/export de_de
importexport = Im-/Export
file_deleted = Datei wurde gelöscht
no_import_file_chosen_or_wrong_version = keine Importdatei ausgewählt oder Version falsch
no_valid_import_file = Das ist keine korrekte Importdatei

usw.
```

So kann auf einer Seite die Sprachdefinition genutzt werden:

```
<div>
<?php echo $I18N_IM_EXPORT->msg('import'); ?>
</div>

Dabei wird die in der Datei install.inc.php definierte Sprachinstanz $I18N_IM_EXPORT verwendet.
```


**Seiten (pages)**

Bei der Auswahl des Menüpunktes des AddOns wird die Datei /pages/index.inc.php eingebunden. Von hier aus kann jetzt gegebenfalls eine Seite ausgegeben oder über eine switch() Bedingung die weiteren Seiten verknüpft werden.

Um im Layout von REDAXO die Seiten des Addons zu programmieren, stehen Ihnen für die Navigation sowie die Abschlussleiste folgende Befehle zur Verfügung:

Erstellen der Navigation und grauen Titelleiste einer Seite:

```
<?php

// Einbinden der REDAXO-Navigation:
include $REX['INCLUDE_PATH']."/layout/top.php";

// Titelliste mit REDAXO Logo ausgeben:
rex_title($I18N_IM_EXPORT->msg("importexport"), "");

......


// Ausgabe des Seitenfußes:
include $REX['INCLUDE_PATH']."/layout/bottom.php";

?>
```

**Ordner "files"**

Der Vollständigkeit halber soll auch noch der Ordner “files” erwähnt werden. Hier sind die Dateien gespeichert, die beim Datei-Export auf dem Server gespeichert werden sollten.

Hier wurde nun die Struktur des AddOns “Import/Export” beschrieben. Dadurch sollte das Prinzip erläutert werden, wie ein AddOn aufgebaut sein könnte. Bestimme Elemente, wie zum Beispiel der Ordner “files”, sind spezifisch für dieses AddOn. Andere, wie die Datei config.inc.php, sind grundsätzlicher Bestandteil eines jeden AddOns. Wer mehr über den Aufbau wissen möchte, sieht sich am besten andere AddOns im Detail an.


<a name="erstellen"></a>
## AddOns erstellen

Wenn Sie ein AddOn erstellen und zum Download anbieten wollen, sollten Sie zunächst unter myREDAXO Ihr Addon anlegen. Dazu müssen Sie über einen myREDAXO-Account verfügen und sich damit einloggen.

**AddOn Dateien bearbeiten**

Nach dem erfolgreichen Anlegen eines AddOns unter “Meine AddOns” erhalten Sie automatisch eine ID, welche Sie für die Entwicklung brauchen werden.

Durch Klicken auf “Dateien bearbeiten” können Sie anschließend die Dateien, die zu dem AddOn gehören, hochladen.

**AddOn Datei hnzufügen**

So, und jetzt noch mal auf “Datei hinzufügen” klicken. Dann haben Sie es fast geschafft.

**AddOn Details**

Bitte geben Sie hier eine Dateinamen an und wählen Sie die passende REDAXO-Version, für die dieses AddOn gedacht ist. Dann laden Sie die Datei über “Durchsuchen” hoch und setzen ein Häkchen bei “Status/Online”, damit es auch für alle verfügbar ist.

Submit klicken, das war's. 
Ein neues REDAXO-AddOn zeigt sich der Öffentlichkeit im Downloadbereich.


**Noch eine Bemerkung zur AddOn-ID**

Diese ID sollte zu Anfang in der config.inc.php des AddOns hinterlegt werden.
Dieser Schritt setzt voraus, dass Sie bereits über folgende Struktur verfügen:

```
<?php
$REX['ADDON']['rxid'][$mypage] = '<meineAddonIdHier>';
?>
```

Diese ID benötigen Sie weiterhin, wenn ihr AddOn mit Datenbanktabellen arbeitet. Für die Benennung von Tabellen sollten Sie wie folgt vorgehen:

```
<?php
$tblName = $REX['TABLE_PREFIX'].'<meineAddonIdHier>_meinTabellenName';
?>
```

Für ein Addon mit der ID 9999 und mit dem Tabellennamen “News” sollte das Ganze dann so aussehen:

```
<?php
$tblNews = $REX['TABLE_PREFIX'].'9999_news';
?>
```

Dabei sollten Sie darauf achten, dass der Tabellenname nur aus Kleinbuchstaben besteht und keine Sonderzeichen enthält.

Weiterhin sollte folgender Coding-Standard verwendet werden

- zwei Leerzeichen als Einrückung (keine Tabs!)
- geschweifte Klammern in einer eigenen Zeile

<a name="import_export"></a>
## Import/Export

Mit dem import_export-AddOn kann man – wer hätte es gedacht – Daten importieren und exportieren. Damit können die Daten der Datenbank und die Dateien der aktuellen Redaxo-Installation gesichert und später wieder verwendet werden.

Sobald dieses AddOn installiert und aktiviert wurde, erscheint der Bereich “Import/Export” in der AddOns-Navigationsleiste des Backends.

**Daten exportieren**

Die Daten der Datenbank und die Dateien werden jeweils separat gespeichert. Die exportierten Daten können direkt auf dem Server gespeichert oder als Dateien heruntergeladen werden, je nach Bedarf. Beim Testen von verschiedenen Varianten von Funktionen beispielsweise, kann zuvor eine Sicherung durchgeführt werden. Diese speichert den Ist-Zustand ab und kann auf dem Server belassen werden. Falls die Änderung sich als nicht sinnvoll erwiesen hat, kann direkt auf diese zurückgegriffen werden. Das Herunterladen als Datei ermöglicht das Sichern der Daten auf einem anderen Rechner.

Beim Datenbank-Export wird eine .sql-Datei erzeugt, die die Struktur und die Inhalte aller Tabelle dieser Redaxo-Installation enthält. Beim Dateiexport werden die ausgewählten Dateien und/oder Verzeichnisse in komprimierter Form gespeichert.

Redaxo schlägt automatisch einen Dateinnamen für die exportierten Daten vor. Dieser Name kann aber beliebig verändert werden.

Wählen Sie die Option “Auf dem Server speichern” wird die Datei auf dem Server gespeichert und hier unter Import angezeigt. Sie finden die auf dem Server gespeicherte Datei im Ordner “/redaxo/include/addons/import_export/files”.

**Daten importieren**


Unter “Datenbankimport” können Sie die Redaxo-Tabellen und deren Inhalte importieren. Sie haben die Möglichkeit, entweder eine extern gespeicherte, zuvor exportierte sql-Datei auszuwählen und zu importieren. Klicken Sie dazu auf “Durchsuchen”, wählen Sie eine sql-Datei von Ihrem Rechner aus und bestätigen Sie die Auswahl durch Klicken auf den “Import”-Button.

Oder Sie wählen eine der hier gelisteten, auf dem Server gespeicherten Import-Dateien aus, indem Sie auf das rot markierte “Import” klicken.

> In beiden Fällen werden die bisherigen Inhalte der Datenbank gelöscht und überschrieben! Dieser Vorgang kann nicht wieder rückgängig gemacht werden.

**Dateien-Import**

Danach können Sie unter Dateienimport die benötigten Dateien importieren. Hier gibt es wieder sowohl die Möglichkeit, eine lokal gespeicherte, exportierte Datei auszuwählen als auch auf eine der auf dem Server gespeicherten Dateien zurückzugreifen.

Nach erfolgreichem Import werden alle Artikel sowie der Cache neu generiert. Auch hier gilt wieder: alle “alten” Dateien werden gelöscht.

<a name="textile"></a>
## Textile

Das Textile-AddOn können Sie in Module einbinden und den Redakteuren so ein Textfeld zur Verfügung stellen, wo sie Texte formatiert eingeben können. Die Formatierung erfolgt nach einer vorgegebenen Konvention mittels bestimmter Abkürzungen oder Zeichen. So können Zeilenumbrüche, Absätze, Überschriften, Links und viele andere Formatierungen angegeben werden. Beim Speichern der Eingaben werden diese Formatierungen automatisch in HTML-Code umgewandelt.

Der grosse Vorteil gegenüber einem WYSIWYG-Editor, wie z. B. dem TinyMCE, ist, dass hier gültiger XHTML-Code erzeugt wird und der Entwickler/Designer eine größere Kontrolle über das Ergebnis hat. Während die vielen netten Buttons eines WYSIWYG-Editors die Redakteure schnell mal zum Spiel mit Farben und Schriftarten verleiten, ist dies bei einem Textile-Eingabefeld zwar auch möglich, aber mit deutlich mehr Aufwand verbunden. Vor allem wenn mehrere Redakteure die Inhalte einer Seite pflegen, ist diese Einschränkung für den Erhalt eines einheitlichen Layouts sehr vorteilhaft.

Zumindest früher war es auch so, dass der mit dem Textile-AddOn erzeugte Quellcode deutlich schlanker war, als der mit einem WYSIWYG-Editor erzeugte. Diese haben sich mittlerweile aber auch weiterentwickelt. Der Unterschied ist nicht mehr ganz so groß.

Ein Nachteil des Textile ist, dass es diese netten Buttons nicht gibt und Sie ihrem Kunden den Umgang mit den mitunter etwas kryptisch anmutenden Formatierungsangaben schmackhaft machen müssen. Das ist normalerweise aber problemlos möglich, da er nur einen kleinen Ausschnitt aus den gesamten Möglichkeiten auch wirklich nutzen wird. Mögliche Abhilfe schafft hier das AddOn markitup für REDAXO, dass die Formatierungen mittels Buttons einfügen kann.

**Textile in Modulen einsetzen**

Das Textile-AddOn ist in der REDAXO-Distribution bereits enthalten. Wenn Sie das AddOn installiert und aktiviert haben, erscheint es in der AddOns-Navigationsleiste des REDAXO-Backends.

Wenn Sie auf den Link “Textile” klicken, erhalten Sie Information zum Umgang mit dem AddOn. Sie erfahren hier, wie Sie eine Anleitung zum Textile in Module einbinden und wie Sie die Modulausgabe ausführen können.

Code für die Moduleingabe

Hier ein Beispiel, wie der Code für die Moduleingabe aussehen könnte:

```
<?php
if(OOAddon::isAvailable('textile'))
{
?>

<strong>Fliesstext</strong>:<br />
<textarea name="VALUE[1]" cols="80" rows="10" class="inp100">REX_HTML_VALUE[1]</textarea>
<br />

<?php
// Einbinden der Anleitung:
rex_a79_help_overview();

}else
{
echo rex_warning('Dieses Modul benötigt das "textile" Addon!');
}

?>
```

Zunächst wird geprüft, ob das AddOn installiert und aktiviert ist. Falls dies so ist, wird ein Textfeld für die Eingabe definiert und eine Tabelle mit einer Anleitung und Formatierungshinweisen eingebunden. Diese Hinweise werden dann unterhalb des Eingabefeldes angezeigt.


> Die Anleitung wird nur angezeigt, wenn das Optionalrecht textile[help] dem Benutzer zugewiesen wurde.


Neu in Version 4 und sehr benutzerfreundlich sind die neue Gliederung der Hilfe nach Themen und die “Akkordeon-Funktion”. Durch Klicken auf ein Thema, hier z. B. “Überschriften”, klappen nur die Hilfeanweisungen für dieses Thema auf. Bei einem erneuten Klick verschwinden sie wieder. So sieht man die Texte nur, wenn man sie auch wirklich braucht.

Weitere Informationen zu den Formatierungsvorgaben können Sie dem Wiki oder direkt dem offiziellen Textile-Handbuch entnehmen.

Sie können auch eine eigene Anweisung verfassen und statt der vorgegebenen in Ihr Modul einbauen. Dazu erstellen Sie ihre Anleitung als HTML-Code, fügen diesen in die Moduleingabe ein und lassen den Funktionsaufruf für die automatisch generierte Hilfe weg.

**Codierung der Modulausgabe**

Hier ein Beispiel, wie der Code für die Modulausgabe aussehen könnte

```
<?php

if(OOAddon::isAvailable('textile'))
{

// Fliesstext 
$text = '';
if(REX_IS_VALUE[1])
{

// Diese 3 Zeilen dürfen keine führenden Leerzeichen besitzen!
$text =<<<EOD
REX_HTML_VALUE[1]
EOD;

$text = rex_a79_textile($text);

} 

$text = str_replace("###","&#x20;",$text);

print '<div class="txt-img">'. $text. '</div>';

}else
{
echo rex_warning('Dieses Modul benötigt das "textile" Addon!');
}

?>
```

Der im Textfeld eingegebene Text wird in der Modulausgabe entsprechend der angegebenen Formatierungen in HTML-Code umgewandelt und angezeigt. Ist das Textile-AddOn nicht installiert, bekommen Sie statt der Eingaben eine Warnmeldung angezeigt ('Dieses Modul benötigt das “textile” Addon!').

``
Die Zeile
$text = str_replace("###","&#x20;",$text);
ermöglicht es, zusätzliche, leere Absätze durch Eingabe von ### einzufügen.

Eingabe:
Das ist ein Absatz

###

Das ist ein zweiter Absatz

Ausgabe:

```
<p>Das ist ein Absatz</p>
<p>&#x20;</p>
<p>Das ist ein zweiter Absatz</p>
```

**Was sieht ein Redakteur?**

Der Redakteur, der einen Text eingeben möchte, ruft das Modul auf, in das das Textile-AddOn eingebunden ist, macht seine Eingaben und verwendet dabei die in der Hilfeliste vorgegebenen Formatierunsangaben, z. B. um Überschriften festzulegen und eine Liste einzugeben.

Hier sei noch erwähnt, dass ein einfacher Zeilenumbruch im Editor auch einen einfachen Umbruch (< br />) in der Ausgabe erzeugt. Bei einem doppelten Umbruch im Editor wird der Text in der Ausgabe als Absatz (< p > Text < / p >)) formatiert. Mehr als zwei Umbrüche werden bei der Ausgabe automatisch auf zwei reduziert. Will er einen größeren Abstand, kann er dies durch Eingabe von “###” erreichen (s. o.).

Hat der Redakteur den Block hinzugefügt, sieht das Ganze im Frontend so aus:

Und hier der dazugehörige Quellcode, schlank, schlicht und sauber

```
<div class="txt-img">	
<h2>Was ist <span class="caps">REDAXO</span></h2>

<p><span class="caps">REDAXO</span> ist ein Content Management System für individuelle, vielfältige und flexible Web-Lösungen.</p>

<h2>Merkmale:</h2>

<ul>
<li>Zentrale Verwaltung mittels einer Client/Serverarchitektur</li>
<li>Trennung von Inhalt und Layout mittels Templates</li>
<li>Die Verwaltung von mehrsprachigen Webseiten ist gegeben</li>
<li>Der Inhalt setzt sich aus verschiedenen Modulen zusammen</li>
<li>Keine Grenzen bei der Erstellung von Modulen</li>
<li>Systemunabhängiges sowie plattformübergreifendes Arbeiten über den Webbrowser</li>
<li>Linkmanagement</li>
<li>Keine Einschränkungen bei der Entwicklung von barrierefreiem Webdesign</li>
</ul>
</div>
```
# Upgrade REDAXO 4.x zu REDAXO 5.x

* [Einleitung](#einleitung)
* [Erste Schritte](#1st)
* [YConverter installieren](#install)
* [Konvertierung der Daten](#convert)
    * [XForm konvertieren](#xform)
* [Übertragung der Datenbank zu REDAXO 5](#transfer)
* [Dateien kopieren](copyfiles)
* [Nachbearbeitung, Fehlerbereinigung](#service)


<a name="einleitung"></a>
## Einleitung

Voraussetzungen:

- Website REDAXO ab 4.6
- Eine frische REDAXO 5.x Installation, ggf. in einem separaten Webspace unter einer Subdomain oder in einer lokal. 
- Installiertes Adminer-AddOn in der REDAXO 5.x Instanz
- Die Templates sollten nicht per require oder include eingebunden sein, sondern direkt eingepflegt sein, andernfalls kann yconverter keine Konvertierung hier durchführen. 

REDAXO 5 ist mit den Vorgängerversionen nicht kompatibel. Die Projekte (z.B. eine Website) müssen zum neuen System migriert werden. Dies erfolgt durch eine Datenbank-Konvertierung, Nachbearbeitung von Modulen und Templates sowie Verschieben von Dateien des files-Ordners. 

>Daten zusätzlich installierter AddOns, außer yform, können nicht konvertiert werden und müssen ggf. separat migriert werden. Es empfiehlt sich vorher zu prüfen welche AddOns in REDAXO 5 fortgeführt werden und ob diese eine Lösung zum Import älterer Versionen anbieten. Alternativ bieten sich ähnliche AddOns an, die die gewünschte Funktionalität wiederherzustellen. 

>Benutzerkonten werden nicht konvertiert und müssen in REDAXO 5 neu angelegt werden.

<a name="1st"></a>
## Erste Schritte

Vor Beginn sollten folgende Schritte durchgeführt werden.

- Deaktivieren der Redakteure um zu vermeiden, dass weitere Inhalte eingepflegt werden. **Benutzer** -> ***Benutzername anklicken*** -> ***Checkbox aktiv deaktivieren*** -> **speichern**
- Backup der Webpräsenz durchführen, z.B. mit dem Backup-AddOn oder mit den vom Hoster bereitgestellten Backuplösungen. 

<a name="install"></a>
## YConverter installieren

YConverter ist nicht im Installer verfügbar und muss in GitHub heruntergeladen werden und dann in die REDAXO 4.x Installation hochgeladen werden. 

- [Zum GitHub-Repo](https://github.com/yakamara/yconverter)
- [Direkter Download](https://github.com/yakamara/yconverter/archive/master.zip)

Man erhält eine Zip-Datei mit der Bezeichnung yconverter-master.zip. Die Datei muss lokal entpackt werden und der Ordner un yconverter umbenannt werden. Anschließend kopiert man den Ordner in den Ordner ***/redaxo/include/addons*** der REDAXO 4.x Installation. Danach lässt es sich in der AddOn-Verwaltung installieren. 

>Einige Hoster bieten Oberflächen (PLESK, CPANEL) an um das Zip direkt auf dem Server hochzuladen und zu entpacken. 

<a name="convert"></a>
## Konvertierung der Daten

Nach erfolgter Installation findet man in der Navigation des REDAXO 4.x Projektes den Navigationspunkt YConverter. 

Die nachfolgenden Tabellen werden in ihrer Struktur und Inhalte in die REDAXO 4 Datenbank dupliziert und für REDAXO 5 modifiziert. Die Tabellenspalten werden angepasst, nicht mehr genutzte Spalten gelöscht, Inhalte teilweise verschoben bzw. konvertiert. 

***Tabellen die konvertiert werden***

* `rex_62_params`
* `rex_62_type`
* `rex_679_type_effects`
* `rex_679_types`
* `rex_action`
* `rex_article`
* `rex_article_slice`
* `rex_clang`
* `rex_file`
* `rex_file_category`
* `rex_module`
* `rex_module_action`
* `rex_template`

>Hinweis: Die Konvertierung hat keinen Einfluss auf die Funktionalität der Webpräsenz. Die REDAXO 4.x-Tabellen bleiben erhalten. Es werden neue Tabellen mit dem Prefix ***yconverter_*** angelegt. 

Nach Bestätigen mit ***Nun auf geht's!*** wird die Konvertierung durchgeführt. 

Findet YConverter Stellen im konvertierten Quellcode, die später nachgearbeitet werden müssen zeigt YConverter diese im Protokoll an. Es empfiehlt sich diese Meldungen zu kopieren und für die spätere Nachbereitung zu sichern. 

![Meldungen bei der Konvertierung](/assets/v5.6.3.yconverter_screen.png)
Meldungen bei der Konvertierung

<a name="xform"></a>
### XForm konvertieren

YConverter bietet auch die Konvertierung von XForm-Tabellen an. Auch hier werden die Tabellen wie oben beschrieben konvertiert und können mittels Formular in die neue Instanz kopiert werden. 

Nach der Übertragung der Daten installiert man in REDAXO 5.x YForm und die Tabellen sollten dann wird wie gewohnt erscheinen. 

<a name="transfer"></a>
## Übertragung der Datenbank zu REDAXO 5

### Variante 1 

Die konvertierten Tabellen können mit dem Formular direkt in die REDAXO 5 Präsenz übertragen werden. 

> Hinweis: Nach der Übertragung wird keine Meldung angezeigt. Es sollte in der REDAXO 5 Präsenz geprüft werden ob die Daten übertragen wurden. 

### Variante 2 

Ist eine direkte Übertragung nicht möglich, da man z.B. keinen Zugriff auf die externe Datenbank von extern hat, ist eine manuelle Übertragung der Daten erforderlich. Hierzu wird in YConverter Adminer mitgeliefert. 

1. Den Adminer im REDAXO 4 in neuem Tab aufrufen.
2. Im Adminer von REDAXO 4 oben links auf Exportieren klicken.
3. Tabellen und Daten alle wegklicken (im Tabellenkopf).
4. Nur die Tabellen und Daten auswählen, bei den die Tabelle mit yconverter_ beginnen.
5. Button Exportieren klicken.
6. Erstellte Daten kopieren.
7. Im Adminer von REDAXO 5 oben links SQL-Kommando klicken und das Kopierte in das Textfeld einfügen.
8. Nach `yconverter_` im Textfeld suchen und löschen.
9. Den Button Ausführen klicken.

> Hinweis: Funktioniert der Import nicht wie gewünscht, sollte man sich den Export als Datei erstellen lassen. Die heruntergeladene Datei kann man dann im Adminer von REDAXO 5 importieren.

<a name="copyfiles"></a>
## Dateien kopieren

Da sich die Dateistruktur in REDAXO 5 geändert hat, müssen die Dateien aus dem `/files`-Ordner in den neuen media-Ordner `/media` in REDAXO 5 kopiert werden. Unterordner, die durch AddOns erstellt wurden, werden nicht benötigt.

Eigene Ordner, die Assets für die Darstellung beinhalten (z.B. für CSS und JS) können ihre ursprüngliche Position kopiert werden.

> Sollten Assets in Unterordnern von /files angelegt sein, z.B. /files/styles/ könnte es zu Problemen bei der Verwendung in Verbindung von Rewrite-AddOns und dem MediaManager kommen. Eine Verschiebung in einen anderen Ordner z.B: /assets/styles/ und Anpassung der Templates und Module sorgt für Abhilfe.  

<a name="service"></a>
## Nachbearbeitung, Fehlerbereinigung

Nach der Übertragung der Daten ist die Präsenz meist noch nicht voll einsatzfähig. 

Sofern es Warnmeldungen bei der Konvertierung gab, sollten diese Stellen als erste abgearbeitet werden. Die entsprechenden Zeilennummern und Codestellen in Modulen und Templates wurden hierfür angegeben. 

REDAXO hilft bei der Suche der Fehler. Die REDAXO-Whoops-Meldung liefert die nötigen Informationen und Codestellen in denen eine Überarbeitung erforderlich ist. Damit dies geschehen kann, muss man im Backend eingeloggt sein. 
Soweit wie möglich einfach die Website und das Backend absurfen und schauen ob ein Fehler erscheint. Des weiteren sollte man regelmäßig das ***Systemlog*** von REDAXO aufsuchen und nach gefundenen Fehlern Ausschau halten.   

Häufig sind die gefundenen Fehler Codefragmente, die bereits in REDAXO 4.x als veraltet angesehen wurden und ausgetauscht werden sollten. Bei der Korrektur des Codes könnten folgende Seiten hilfreich sein:

- [Änderungen REDAXO 4 zu 5](https://redaxo.org/doku/master/aenderungen-v4-v5)
- [Weiterführende Tipps nach Konvertierung von REDAXO 4.x zu 5 in den FOR Tricks](https://friendsofredaxo.github.io/tricks/howto/redaxo_4_5_upgrade)

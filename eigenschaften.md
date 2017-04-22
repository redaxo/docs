# Eigenschaften

Die Methoden der Klasse rex sind global in Templates, Modulen und AddOns verfügbar und ermöglichen Zugriff auf Grundeinstellungen und Zustände des Systems.
Methoden wie `setProperty` und `getProperty` können auch verwendet werden, um systemweit eigene Eigenschaften abzulegen.

## Config-Methoden

Die Werte werden in der Tabelle rex_config gespeichert.

## Property-Methoden

Die Werte werden dynamisch während der Laufzeit verwaltet.

## Beschreibung der Methoden

### getAccesskey

Beispiel: `<button type="submit" <?= rex::getAccesskey("speichern","s") ?>>Speichern</button>`
Schreibt `<button type="submit" accesskey="s" title="speichern[s]">Speichern</button>` in die Ausgabe.

Für den Access Key können auch Werte aus config verwendet werden:
save: s
apply: x
delete: d
add: a

Beispiel: `<button type="submit" <?= rex::getAccesskey("speichern","save") ?>>Speichern</button>`
Schreibt `<button type="submit" accesskey="s" title="speichern[s]">Speichern</button>` in die Ausgabe.

### getConfig

Beispiel: `rex::getConfig('version')` => "5.3"

Siehe auch setConfig

### getDirPerm

Liest die Eigenschaft von `dirperm` aus.

Beispiel: `rex::getDirPerm()` => 755

### getErrorEmail

Gibt die im System eingestellte Error E-Mail Adresse aus.

Beispiel: `rex::getErrorEmail()` => 'info@example.com'

### getFilePerm

Liest die Eigenschaft von `fileperm` aus.

Beispiel: `rex::getFilePerm()` => 664

### getProperty

Liest die Eigenschaft des Wertes, der zuvor über `setProperty` gespeichert wurde.

Beispiel: `rex::getProperty('myvar')` => Inhalt des zuvor über `rex::setProperty('myvar',$var)` gespeicherten Wertes.

Werte können von einem beliebigen Typ sein.

Siehe auch `setProperty`, `hasProperty` und `removeProperty`

### getServer

Liest den Wert aus, der in den Systemeinstellungen im Feld `URL der Website` eingetragen wurde.

Beispiel: `rex::getServer()` => http://example.com/

Die Methode kann verwendet werden, um absolute URLs zu erstellen.

### getServerName

Liest den Wert aus, der in den Systemeinstellungen im Feld `Name der Website` eingetragen wurde.

Beispiel: `rex::getServerName()` => "Meine supertolle Website"

Die Methode kann verwendet werden, um den Title Tag zu füllen.

### getTable

Fügt an einen übergebenen Tabellenname das in der config stehende Prefix für die Datenbanktabellen hinzu. Standard: rex_

Parameter: Tabellenname

Beispiel: `rex::getTable('adressen')` => rex_adressen

Die Funktion ist bevorzugt einzusetzen anstelle von `rex::getTablePrefix.'adressen'`.

### getTablePrefix

Liefert den Wert für den in der config eingestellten Table Prefix für Datenbanktabellen. Standard: rex_

Beispiel: `rex::getTablePrefix()` => rex_

Die Methode `rex::getTable()` ist bevorzugt einzusetzen. 

### getTempPrefix

Liefert den Wert für den in der config eingestellten temp_prefix. Standard: tmp_

Beispiel: `rex::getTempPrefix()` => tmp_

### getUser

Wenn ein Redaxo Benutzer im Backend angemeldet ist, liefert diese Methode den Benutzer als User Objekt.

Beispiel: `rex::getUser()->getName()` => Administrator

### getVersion

Liefert die installierte Version von Redaxo

Beispiel: `rex::getVersion()` => "5.3.0"
`if(rex_string::versionCompare(rex::getVersion(), '5.3.0', '>=')) ...` prüft, ob die Redaxo Version mindestens 5.3.0 ist.

### hasConfig

Prüft, ob ein Config Wert gesetzt ist.

Beispiel: `rex::hasConfig('version')` => true

### hasProperty

Prüft, ob eine Eigenschaft gesetzt ist.

Beispiel: `rex::hasProperty('myvar')` => true

Siehe auch `setProperty`, `getProperty` und `removeProperty`

### isBackend

Prüft, ob gerade das Backend aufgerufen ist. Wird oft in Modulen verwendet, um die Backend Ausgabe anders zu gestalten als die Frontend Ausgabe.

Beispiel: `rex::isBackend()` => true im Backend, false im Frontend

### isDebugMode

Prüft, ob der DebugMode in den Systemeinstellungen aktiviert ist.

Beispiel: `rex::isDebugMode()` => true oder false

### isSafeMode

Prüft, ob der SafeMode des Systems aktiviert ist. Im SafeMode sind AddOns deaktiviert.

Beispiel: `rex::isSafeMode()` => true oder false

### isSetup

Prüft, ob sich das System im Setup Modus befindet. Der Wert kann in den Systemeinstellungen auf true gesetzt werden, was nur sehr sehr ausnahmsweise notwendig sein sollte..

Beispiel: `rex::isSetup()` => normalerweise false

### removeConfig

Eine Config Einstellung löschen.

Beispiel: `rex::removeConfig('ein_konf_wert')`

Siehe auch: `getConfig`, `setConfig` und `hasConfig`

### removeProperty

Eine Eigenschaft löschen.

Beispiel: `rex::removeProperty('myvar')`

Siehe auch `getProperty`, `hasProperty` und `setProperty`

### setConfig

Eine Config Einstellung setzen.

Beispiel: `rex::setConfig('ein_konf_name','der_konf_value')`

Siehe auch: `getConfig`, `removeConfig` und `hasConfig`

### setProperty

Eine Eigenschaft setzen.

Beispiel: `rex::setProperty('myvar','myval')`

Siehe auch `getProperty`, `hasProperty` und `removeProperty`
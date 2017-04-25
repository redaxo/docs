# Eigenschaften
- [rex-Klasse](#rex-klasse)
- [Config-Methoden](#config-methoden)
- [Property-Methoden](#property-methoden)
- [Beschreibung der Methoden](#beschreibung)
    - [getAccesskey](#get-accesskey)
    - [getConfig](#get-config)
    - [getDirPerm](#get-dir-perm)
    - [getErrorEmail](#get-error-email)
    - [getFilePerm](#get-file-perm)
    - [getProperty](#get-property)
    - [getServer](#get-server)
    - [getServerName](#get-server-name)
    - [getTable](#get-table)
    - [getTablePrefix](#get-table-prefix)
    - [getTempPrefix](#get-temp-prefix)
    - [getUser](#get-user)
    - [getVersion](#get-version)
    - [hasConfig](#has-config)
    - [hasProperty](#has-property)
    - [isBackend](#is-backend)
    - [isDebugMode](#is-debug-mode)
    - [isSafeMode](#is-safe-mode)
    - [isSetup](#is-setup)
    - [removeConfig](#remove-config)
    - [removeProperty](#remove-property)
    - [setConfig](#set-config)
    - [setProperty](#set-property)

<a name="rex-klasse"></a>
## "rex"-Klasse
Die Methoden der Klasse `rex` sind global in Templates, Modulen und AddOns verfügbar und ermöglichen Zugriff auf Grundeinstellungen und Zustände des Systems.
Methoden wie `setProperty` und `getProperty` können auch verwendet werden, um systemweit eigene Eigenschaften abzulegen.

<a name="config-methoden"></a>
## Config-Methoden

Die Werte werden in der Tabelle rex_config gespeichert.

**Hinweis:** AddOns können ihre Konfiguration über das Package-Objekt in die Konfiguration schreiben: `rex_addon::get($addon)->setConfig($key, $value);` und lesen `$value = rex_addon::get($addon)->getConfig($key);`.

<a name="property-methoden"></a>
## Property-Methoden

Die Werte werden dynamisch während der Laufzeit verwaltet.

<a name="beschreibung"></a>
## Beschreibung der Methoden

<a name="get-accesskey"></a>
### getAccesskey

Beispiel:

```
<button type="submit" <?= rex::getAccesskey("speichern","s") ?>>Speichern</button>
```
schreibt

```
<button type="submit" accesskey="s" title="speichern[s]">Speichern</button>
```
in die Ausgabe.

Für den Access-Key können auch Werte aus `config` verwendet werden:
save: s
apply: x
delete: d
add: a

Beispiel:

```
<button type="submit" <?= rex::getAccesskey("speichern","save") ?>>Speichern</button>
```
schreibt

```
<button type="submit" accesskey="s" title="speichern[s]">Speichern</button>
```
in die Ausgabe.

<a name="get-config"></a>
### getConfig

Beispiel:

`rex::getConfig('version')` => "5.3"

Siehe auch: [setConfig](#set-config)

<a name="get-dir-perm"></a>
### getDirPerm

Liest die Eigenschaft von `dirperm` aus.

Beispiel:
`rex::getDirPerm()` => 755

<a name="get-error-email"></a>
### getErrorEmail

Gibt die im System eingestellte Error-E-Mail-Adresse aus.

Beispiel:
`rex::getErrorEmail()` => 'info@example.com'

<a name="get-file-perm"></a>
### getFilePerm

Liest die Eigenschaft von `fileperm` aus.

Beispiel:
`rex::getFilePerm()` => 664

<a name="get-property"></a>
### getProperty

Liest die Eigenschaft des Wertes, der zuvor über `setProperty` gespeichert wurde.

Beispiel:
`rex::getProperty('myvar')` => Inhalt des zuvor über `rex::setProperty('myvar',$var)` gespeicherten Wertes.

Die Werte können von einem beliebigen Typ sein.

Siehe auch: [setProperty](#set-property), [hasProperty](#has-property) und [removeProperty](#remove-property)

<a name="get-server"></a>
### getServer

Liest den Wert aus, der in den Systemeinstellungen im Feld `URL der Website` eingetragen wurde.

Beispiel:
`rex::getServer()` => http://example.com/

Die Methode kann verwendet werden, um absolute URLs zu erstellen.

<a name="get-server-name"></a>
### getServerName

Liest den Wert aus, der in den Systemeinstellungen im Feld `Name der Website` eingetragen wurde.

Beispiel:
`rex::getServerName()` => "Meine supertolle Website"

Die Methode kann verwendet werden, um den Title-Tag zu füllen.

<a name="get-table"></a>
### getTable

Fügt an einen übergebenen Tabellennamen das in der `config` stehende Prefix für die Datenbanktabellen hinzu.
Standard: `rex_`

Parameter: Tabellenname

Beispiel:
`rex::getTable('adressen')` => rex_adressen

Die Funktion ist bevorzugt einzusetzen anstelle von `rex::getTablePrefix.'adressen'`

<a name="get-table-prefix"></a>
### getTablePrefix

Liefert den Wert für den in der `config` eingestellten Table Prefix für Datenbanktabellen.
Standard: `rex_`

Beispiel: `rex::getTablePrefix()` => rex_

Die Methode `rex::getTable()` ist bevorzugt einzusetzen. 

<a name="get-temp-prefix"></a>
### getTempPrefix

Liefert den Wert für den in der `config` eingestellten `temp_prefix`.
Standard: `tmp_`

Beispiel:
`rex::getTempPrefix()` => tmp_

<a name="get-user"></a>
### getUser

Wenn ein Redaxo Benutzer im Backend angemeldet ist, liefert diese Methode den Benutzer als User-Objekt.

Beispiel:
`rex::getUser()->getName()` => Administrator

<a name="get-version"></a>
### getVersion

Liefert die installierte Version von REDAXO.

Beispiel:
`rex::getVersion()` => "5.3.0"

`if(rex_string::versionCompare(rex::getVersion(), '5.3.0', '>=')) ...` prüft, ob die REDAXO-Version mindestens 5.3.0 ist.

<a name="has-config"></a>
### hasConfig

Prüft, ob ein Config-Wert gesetzt ist.

Beispiel:
`rex::hasConfig('version')` => true

<a name="has-property"></a>
### hasProperty

Prüft, ob eine Eigenschaft gesetzt ist.

Beispiel:
`rex::hasProperty('myvar')` => true

Siehe auch: [setProperty](#set-property), [getProperty](#get-property) und [removeProperty](#remove-property)

<a name="is-backend"></a>
### isBackend

Prüft, ob gerade das Backend aufgerufen wird. Wird oft in Modulen verwendet, um die Backend-Ausgabe anders zu gestalten als die Frontend-Ausgabe.

Beispiel:
`rex::isBackend()` => true im Backend, false im Frontend

<a name="is-debug-mode"></a>
### isDebugMode

Prüft, ob der DebugMode in den Systemeinstellungen aktiviert ist.

Beispiel:
`rex::isDebugMode()` => true oder false

<a name="is-safe-mode"></a>
### isSafeMode

Prüft, ob der SafeMode des Systems aktiviert ist. Im SafeMode sind AddOns deaktiviert.

Beispiel:
`rex::isSafeMode()` => true oder false

<a name="is-setup"></a>
### isSetup

Prüft, ob sich das System im Setup-Modus befindet. Der Wert kann in den Systemeinstellungen auf `true` gesetzt werden, was nur sehr, sehr ausnahmsweise notwendig sein sollte ...

Beispiel:
`rex::isSetup()` => normalerweise false

<a name="remove-config"></a>
### removeConfig

Eine Config-Einstellung löschen.

Beispiel:
`rex::removeConfig('ein_konf_wert')`

Siehe auch: [getConfig](#get-config), [setConfig](#set-config) und [hasConfig](#has-config)

<a name="remove-property"></a>
### removeProperty

Eine Eigenschaft löschen.

Beispiel:
`rex::removeProperty('myvar')`

Siehe auch: [getProperty](#get-property), [hasProperty](#has-property) und [setProperty](#set-property)

<a name="set-config"></a>
### setConfig

Eine Config-Einstellung setzen.

Beispiel: `rex::setConfig('ein_konf_name','der_konf_value')`

Siehe auch: [getConfig](#get-config), [removeConfig](#remove-config) und [hasConfig](#has-config)

<a name="set-property"></a>
### setProperty

Eine Eigenschaft setzen.

Beispiel:
`rex::setProperty('myvar','myval')`

Siehe auch: [getProperty](#get-property), [hasProperty](#has-property) und [removeProperty](#remove-property)


# Formulare

- [Eingabefelder validieren](#eingabefelder-validieren)

<a name="eingabefelder-validieren"></a>
## Eingabefelder validieren
Die Eingaben von rex_form-Eingabefeldern können vor dem Absenden des Formulars validiert werden. Dazu werden dem validator-Objekt des Eingabefelds ein oder mehrere Validatoren hinzugefügt:

    $field->getValidator()->add( string $type, null|string $message = null, mixed $option = null )
    
$type bezeichnet die Validator-Funktion, $message die auszugebende Fehlermeldung und $option weitere Parameter für die Prüfung

Folgende Validatoren sind verfügbar:

Name | Beschreibung | Parameter
------------- | ------------- | -------------
notEmpty	| prüft, ob ein Eingabefeld leer ist | -
type	| prüft den Wert des Eingabefelds auf einen Variablentyp | Variablentyp: (int/integer, float, real)
minLength | prüft auf eine Mindestlänge des Feldinhalts | Anzahl Zeichen Mindestlänge
maxLength | prüft auf eine Maximallänge des Feldinhalts | Anzahl Zeichen Maximallänge
to be continued | ...

  > **Hinweis:** 
Alle Validator-Typen außer notempty führen die Prüfung erst dann durch, wenn der Feldinhalt nicht leer ist. Soll also z.B. ein Eingabefeld obligatorisch eine deutsche Postleitzahl enthalten, muss zusätzlich zum match auf /^[0-9]{5}$/' auch ein notempty-Validator hinzugefügt werden.

### Beispiele
coming soon...




## Editieren und Anlegen von Datensätzen

Die `rex_form` Klasse ist "Part 2" der Redaxo eigenen Datenbankverwaltung für Addons. Mit Hilfe der `rex_form` klasse ist es möglich Datensätze editeren oder anlegen zu können. Dabei bietet `rex_form` alle nötigen Standard-Formular-Elemente und ermöglicht darüber hinaus den einsatz von Redaxo-Widgets wie Link-, Linklisten oder Media- und Media-Listen-Eingabe-Felder.

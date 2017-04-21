# Aktionen - Moduleingaben überprüfen

## Einleitung / Problemstellung
Falsche Eingabe von Benutzern führen oft zu unerwünschten Ergebnissen, fehlerhaften Darstellungen der Webseite und können ungültiges HTML-Markup zur Folge haben. Daher gehören Validierungen von Eingaben zum guten Ton eines pflichtbewussten Administrators. Dies wird bereits bei einfachen Modulen deutlich, wie beispielsweise einem Überschriftenmodul.

Wir gehen von folgendem Modulcode aus:

**Eingabe:**

```HTML
Überschrift:<br />
<input type="text" size="50" name="VALUE[1]" value="REX_VALUE[1]" />
```

**Ausgabe:**

```PHP
<h1>REX_VALUE[1]</h1>
```

Eine leeren Eingabe ohne Validierung würde folgendes Ergebnis erzeugen:

```PHP 
<h1></h1>
```

Dieses Ergebnis führt bereits zu einem invaliden Markup der Webseite.

## Lösung

Um dieses Problem zu vermeiden, sind Eingaben des Benutzers zu validieren. In REDAXO kann man dies mit Presave-Aktionen bewerkstelligen.

Folgende Presave-Aktion könnte man bei obigen Modul einsetzen:

```PHP
<?php
// Wurde eine Überschrift eingeben?
if(trim($REX_ACTION['VALUE']['1']) == '')
{
// Überschrift ist leer
// -> Speichern des Blockes verhindern
$REX_ACTION['SAVE'] = false;
// Fehlermeldung setzen
$REX_ACTION['MSG'] = 'Bitte geben Sie eine Überschrift ein!';
}
?>
```

Mit diesem Code ist folgende Aktion anzulegen:

-- BILD 1 --

Als sinnvolle Events wären hier “ADD – Beim Hinzufügen des Moduls” und “EDIT – Beim Bearbeiten des Moduls” zu wählen, damit sowohl beim Erstellen als auch beim Ändern von Inhaltsblöcken eine Validierung erfolgt.

Im Anschluss muss man die Aktion noch dem jeweiligen Modul zugeordnen. Dies geschieht durch Auswahl der Aktion innerhalb der Select-Box und Abschicken des Formulars durch den Klick auf “Aktion hinzufügen”:


--BILD 2 ---

Eine Fehleingabe des Benutzers beim Verwalten der Inhalte würde zu folgender Meldung führen:

--BILD 3 ---

Damit ist sichergestellt, dass keine leeren h1-Elemente auf der Webseite erscheinen.

## Ein weiteres Beispiel: Medienvalidierung


```PHP
<?php
// Wurde ein Medium ausgewählt?
if($REX_ACTION['MEDIA']['1'] == '')
{
// kein Medium ausgewählt
// -> Speichern des Blockes verhindern
$REX_ACTION['SAVE'] = false;
// Fehlermeldung setzen
$REX_ACTION['MSG'] = 'Bitte wählen Sie ein PNG-Bild aus!';
}
// Wurde ein PNG Bild gewählt?
else if(strtolower(substr($REX_ACTION['MEDIA']['1'], -3)) != 'png')
{
// Kein PNG ausgewählt
// -> Speichern des Blockes verhindern
$REX_ACTION['SAVE'] = false;
// Fehlermeldung setzen
$REX_ACTION['MSG'] = 'Ungültige Datei gewählt: Bitte wählen Sie ein PNG-Bild aus!';
}
?>
```
Diesen Code muss man ebenfalls als Presave-Aktion mit den Events ADD und EDIT abspeichern. Wenn man die Aktion anschließend noch dem entsprechenden Modul hinzufügt, somit gehören Fehleingaben durch den Benutzer der Vergangenheit an.

Viel Spass beim Validieren…



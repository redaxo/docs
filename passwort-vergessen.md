# Passwort vergessen
Das Passwort einer REDAXO 4 Installation lässt sich über mehrere Wege zurücksetzen.

## Passwort durch Admin ändern lassen
Existiert ein weiterer Benutzer mit admin Rechten, kann dieser im Backend ein neues Passwort für den betroffenen Benutzer hinterlegen.

## Passwort über Datenbank ändern
Hat man Zugriff auf die Datenbank (zum Beispiel über phpMyAdmin oder Adminer) kann man das Passwort dort ersetzen.
Hierzu verbindet man sich mit der Datenbank und wählt die Tabelle rex_user.
In der Zeile des betreffenden Benutzers in der Spalte psw kann man das Passwort anpassen.
Zu beachten ist, dass das Passwort verschlüsselt gespeichert ist und man den Wert durch einen bekannten Schlüssel ersetzen muss. Fügt man die Hash 01b307acba4f54f55aafc33bb06bbbf6ca803e9a ein, lautet das Passwort für den Benutzer anschließend 1234567890

## Setup durchlaufen lassen
Hat man keinen Zugriff auf die Datenbank bleibt der Weg über das Setup.
Auf dem Webserver im Verzeichnis redaxo/include die Datei master.inc.php öffnen und den Wert hinter $REX['SETUP'] auf true setzen.
Wird die Website nun aufgerufen, startet das Setup erneut.
Einfach ohne Änderungen durchklicken bis zu Punkt 3.
Hier wählt man: "Datenbank für Version 4.7 existiert schon [Weiter ohne Datenbankimport]"
Im Schritt 4 kann man nun einen neuen Benutzer anlegen.



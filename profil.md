# Profil

![Profil](/assets/v5.15.0-profil-01-overview.png)

Das Benutzerprofil kann durch Klick auf den Namen neben `Angemeldet als:` aufgerufen werden. Hier können der Name, die Beschreibung, die hinterlegte E-Mail-Adresse und das Passwort geändert werden. Die E-Mail-Adresse ist als interne Kontakt-Information für den Administrator vorgesehen, kann jedoch auch für Benachrichtigungen einiger AddOns wichtig sein. Der Benutzername kann nicht geändert werden.

## Passwort ändern

Zur Änderung des Passwortes gibt man sein altes Passwort ein und schreibt in die anschließenden zwei Felder das neue Passwort. Die Änderung wird mit `Passwort speichern` bestätigt.

Zur eigenen Sicherheit und zum Schutze der Webpräsenz sollte das neue Passwort …
- möglichst aus mehr als 6 Zeichen bestehen
- Ziffern und Buchstaben in Groß- und Kleinschreibung enthalten
- Sonder- oder Satzzeichen enthalten
- keine Begriffe enthalten, die sich in einem Wörterbuch finden lassen
- nicht weiteren Personen zugänglich sein

## Passkey hinzufügen

Seit REDAXO 5.15 kann man anstelle der Benutzername-Passwort-Kombination auch das Login-Verfahren per Passkey nutzen. 
Hierzu muss man einmal das alte Paswort eingeben und dann bestätigen, dass der Passkey angelegt werden soll. 
Ab da an kann man sich ohne Eingabe eines Passwortes in REDAXO einloggen. 

> Die Passkey-Box rechts erscheint nur, wenn der Browser die nötigen Bedingungen erfüllt.

![Profil](/assets/v5.15.0-passkey_bestaetigen.png)
Passkey bestätigen

Wenn man sich mit Passkey eingeloggt hat, kann man im Profil das Passwort optional ganz entfernen.
Bei Passwort-Änderung und Passkey-Hinzufügung muss man immer mit der aktuellen Auth-Methode bestätigen. Also bei Login mit Passkey dann nicht mit dem "Alten Passwort", sondern per Button, der den vorhandenen Passkey prüft.

## Backend-Theme auswählen (light- und dark mode) 

Entsprechend der Systemeinstellung passt sich das REDAXO-Theme  den Vorlieben des Nutzers an. Möchte man ein Theme erzwingen, stehen folgende Optionen zur Vefügung:

- `Hell`  
  Entspricht der bisher bekannten REDAXO-Oberfläche
- `Dunkel`  
  Besonders geeignet für Umgebungen mit wenig Licht (»Dark Mode«).
- `Automatisch`  
  Dies ist die Voreinstellung für alle neuen Nutzer. In diesem Modus entscheidet der Browser anhand der Systemeinstellungen eigenständig, welches Theme verwendet wird. Damit ist beispielsweise auch möglich, dass REDAXO tagsüber hell ausgegeben wird, nach Sonnenuntergang jedoch dunkel.

Die Auswahl des Themes kann von Administratoren deaktiviert werden. Das Auswahlfeld ist dann nicht klickbar, und alle Nutzer erhalten das vorgegebene Theme.

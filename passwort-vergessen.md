# Passwort vergessen

Falls du dein Passwort vergessen hast, musst du dieses in der Datenbank zurücksetzen. Falls du in dieser Richtung zu wenig bzw. keine Erfahrung besitzt, wende dich bitte an deinen Entwickler oder Hoster.

## Änderung des Passworts über phpMyAdmin oder Adminer

Bevor du Änderungen an der Datenbank durchführst, denke daran ein Backup anzulegen.

Suche die Datenbank die du bei der Installation angegeben hast und öffne dort die Tabelle `rex_user`. Dort findest du den Eintrag mit deinem Login.

Ersetze das kryptische Passwort durch folgende Zeile:

```sha
$2y$10$GQripq8LDWMGNsnw5b/u8uFG/fkzC2p2uVlrQFx49F0BzbjATDE1u 
```

Diese Zeile entspricht dem Passwort `redaxo-cms`. Melde dich nun mit deinem Benutzernamen an und ändere *unbedingt* das Passwort in der Benutzerverwaltung.

> Dein Passwort muss unter allen Umständen geändert werden, um Fremdzugriffe zu verhindern! Dieses Passwort wird vermutlich als erstes von Dritten getestet, die sich unerlaubt Zugriff auf das System verschaffen wollen!

## Änderung eines Passworts über die Konsole (ab REDAXO 5.6+)

Ein Passwort kann sehr einfach über die Konsole aktualisiert werden. Hierzu muss man sich im `/redaxo/bin` Ordner der REDAXO-Installation befinden und kann durch Eingabe von `php console user:set-password <user> [<password>]` ein neues Passwort setzen.

Wurde das neue Passwort gespeichert, sollte folgende Meldung erscheinen: `[OK] Saved new password for user XYZ`

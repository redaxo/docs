# Passwort vergessen

Falls du dein Passwort vergessen hast, musst du dieses in der Datenbank zurücksetzen. Falls du in dieser Richtung zu wenig bzw. keine Erfahrung besitzt, wende dich bitte an deinen Entwickler oder Hoster.

## Änderung des Passworts über PhpMyAdmin oder Adminer

Bevor du Änderungen an der Datenbank durchführst, denke daran, ein Backup anzulegen.

Suche die Datenbank, die du bei der Installation angegeben hast und öffne dort die Tabelle `rex_user`. Dort findest du den Eintrag mit deinem Login.

Ersetze das kryptische Passwort durch folgende Zeile:

```sha
$2y$10$tsQCVLC.SnYnEJXwXHLfJ.MNRRG7uGcppoJPvJK6N8BpZ8hKJ3Af2
```

Diese Zeile entspricht dem Passwort `redaxo-cms`. Melde dich nun mit deinem Benutzernamen an und ändere *unbedingt* das Passwort in der Benutzerverwaltung.

> Dein Passwort muss unter allen Umständen geändert werden, um Fremdzugriffe zu verhindern! Dieses Passwort wird vermutlich als erstes von Dritten getestet, die sich unerlaubt Zugriff auf das System verschaffen wollen!

## Neuanlage eines Nutzers über das Setup

Wenn Zugriff auf den Webspace mittels FTP(S) möglich ist, kann auch das Setup verwendet werden, um einen neuen Benutzer mit Administrator-Rechten anzulegen.

> Sofern möglich, ein Backup beim Hoster durchführen.

Folgende Schritte führen zum neuen Login.

1. In der Datei `/redaxo/data/core/config.yml` muss `setup: false` auf `setup: true`gesetzt werden. 
2. Danach die Website unbedingt sofort aufrufen! (Der Setup-Vorgang ist für alle Besucher sichtbar, daher ist Eile geboten!)
3. Durchgehen des Setups, Schritt 4 so belassen wie es ist.
4. In Schritt 5 (Datenbank) `Datenbank existiert schon` auswählen.
5. Im nächsten Schritt einen neuen Nutzer anlegen.
6. Abschließen und dann in REDAXO einloggen. 


## Änderung eines Passworts über die Konsole

Ein Passwort kann sehr einfach über die [Konsole](/{{path}}/{{version}}/console) aktualisiert werden. Hierzu in der Konsole ins Verzeichnis `/redaxo/bin` der REDAXO-Installation wechseln und diesen Befehl eingeben, um das Passwort zurückzusetzen.

```console
php console user:set-password <user> [<password>]
```

Wurde das neue Passwort gespeichert, sollte folgende Meldung erscheinen: `[OK] Saved new password for user XYZ`

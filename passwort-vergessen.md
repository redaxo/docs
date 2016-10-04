# Passwort vergessen

Falls du dein Passwort vergessen hast, musst du dieses in der Datenbank zurücksetzen. Falls Du in dieser Richtung zu wenig bzw. keine Erfahrung besitzt, wende dich bitte an deinen Entwickler oder Hoster.

## Änderung des Passworts mit phpMyAdmin
Bevor du Änderungen an der Datenbank durchführst, denke daran ein Backup anzulegen. 

Suche die Datenbank die du bei der Installation angegeben hast und öffne dort die Tabelle *rex_user*. Dort findest du den Eintrag mit deinem Login. 

Ersetze das kryptische Passwort durch folgende Zeile:

          $2y$10$j3WXi9dV9ft0osXCj/QfS.XGXYEnCxFEHx8LJ/PbrvjOjbKObrCV2
          
Diese Zeile entspricht dem Passwort 123456789. Melde dich nun mit deinem Benutzernamen an und ändere *unbedingt* das Passwort in der Benutzerverwaltung.

> Dein Passwort muss unter allen Umständen geeändert werden, um Fremdzugriffe zu verhindern! Dieses Passwort wird vermutlich als erstes von Dritten getestet, die sich unerlaubt Zugriff auf das System verschaffen wollen!

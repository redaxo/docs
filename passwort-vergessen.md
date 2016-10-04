# Passwort vergessen

Falls Du dein Passwort vergessen hast, musst du dieses in der Datenbank zurücksetzen. Falls Du in dieser Richtung zu wenig bzw. keine Erfahrung besitzt, wende dich bitte an deinen Entwickler oder Hoster.

Suche die Datenbank die Du bei der Installation angegeben hast und öffnen die Tabelle rex_user. Suche den Eintrag mit deinem Login und bearbeite diesen. Der Editiervorgang ist von einer phpMyAdmin-Version zur nächsten unterschiedlich möglich.

Ersetze das kryptische Passwort durch folgende Zeile:

          $2y$10$j3WXi9dV9ft0osXCj/QfS.XGXYEnCxFEHx8LJ/PbrvjOjbKObrCV2
          
Diese Zeile entspricht dem Passwort 123456789. Melde dich nun mit deinem Benutzernamen an und ändere das Passwort in der Benutzerverwaltung.

> Dein Passwort muss unter allen Umständen geeändert werden, um Fremdzugriffe zu verhindern! Dieses Passwort wird vermutlich als ersten von Dritten getestet, die sich unerlaubt zugriff verschaffen wollen!

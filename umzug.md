# Umzug einer REDAXO Website
- [Allgemeines](#allg)
- [Umzug per Backup-Addon](#ba)
- [Umzug mit manuellem Datenbank-Backup](#db)

<a name="allg"></a>
## Allgemeines

Um eine Redaxo-Installation von einem Server auf einen anderen Server zu übertragen, gibt es verschiedene Lösungswege. Im Regelfall müssen dazu das Dateisystem (Redaxo, einschließlich Addons und Konfigurationsdateien) und die Datenbank umgezogen werden. 

Falls sich dabei auch die verwendete (Sub-)Domain ändert, sollte nach dem Umzug im Bereich `System` die Domain angepasst werden. Wenn ein Rewrite-Addon zum Einsatz kommt, müssen dort die Einstellungen ggf. vorab angepasst werden. Hierzu die Dokumentation des verwendeten Addons unbedingt beachten. 

Die nachfolgenden Lösungen zeigen den klassischen Weg mittels via "FTP,SFTP, WebDAV"-Datensicherung. 

> Tipps: Einige Hoster bieten zur Verwaltung des Webspaces auch Oberflächen wie PLESK oder CPANEL an. Hier enthalten ist auch ein Dateimanager, mit dem man die komplette Dateistruktur einer Webpräsenz zippen und entpacken kann. Websitebetreiber mit einem Shell-Zugriff können häufig auch einen direkten "Server zu Server"-Filefransfer z.B. per SCP durchführen. 

<a name="ba"></a>
## Umzug per Backup-Addon

- Die Datenbank der Quell-Präsenz wird mit Hilfe des [Backup](/{{path}}/{{version}}/backup)-AddOns ***auf dem Server*** gesichert. 
- Download aller Ordner und Dateien der REDAXO-Installation, z.B. per SFTP
- Im Download unter `/redaxo/data/core/config.yml` die Zeile `setup` von `false` auf `true` stellen
- Die Dateien auf den Ziel-Server übertragen
- Website auf dem Zielserver aufrufen, das Setup wird aufgerufen
- Bei Schritt 4 die Zugangsdaten der neuen Datenbank angeben oder ggf. eine Datenbank anlegen
- Bei Schritt 5 unter ***Vorhandenen Export einspielen:*** die Datensicherung auswählen
- Setup bis zum Ende durchführen - **fertig*** (ggf. anschließend im Bereich `System` den Cache löschen)

<a name="db"></a>
## Umzug mit manuellem Datenbank-Backup 

- Sicherung der kompletten Datenbank über das `Backup`-Addon in Redaxo. 
- Download aller Ordner und Dateien der REDAXO-Installation, z.B. per SFTP
- Upload der in Schritt 2 heruntergeladenen Dateien auf den Ziel-Server
- Import der Datenbank-Sicherung in der neuen Datenbank, z.B. mit PHPMyAdmin oder Adminer
- Unter `/redaxo/data/core/config.yml` die Zeile `setup` von `false` auf `true` stellen
- Ebenfalls unter `/redaxo/data/core/config.yml` unterhalb der Zeile `db` die neuen Datenbank-Zugangsdaten einstellen.
- Das Setup durchlaufen und in Schritt 4 des Setups ***Datenbank existiert schon*** auswählen. Die Anlage eines  Administratorzugangs ist nicht erforderlich
- Anschließend einloggen und ggf. im Bereich `System` den Cache löschen




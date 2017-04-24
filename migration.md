# Migration

## Grundlegendes

Um eine Redaxo-Installation von einem Server auf einen anderen Server zu übertragen, gibt es verschiedene Lösungswege. Im Regelfall müssen dazu das Dateisystem (Redaxo, einschließlich Addons und Konfigurationsdateien) und die Datenbank umgezogen werden. Falls sich dabei auch die verwendete (Sub-)Domain ändert, sollte nach dem Umzug im Bereich `System` die Domain angepasst werden. Wenn ein Rewrite-Addon zum Einsatz kommt, müssen dort die Domain-Einstellungen ggf. angepasst werden. Hierzu die Dokumentation der verwendeten Addons unbedingt beachten. 

> Tipp: Einige Hoster bieten zur Verwaltung des Webspaces auch Oberflächen wie PLESK oder CPANEL an. Hier enthalten ist auch ein Dateimanager, mit dem man die komplette Dateistruktur einer Webpräsenz zippen und entpacken kann.



## Via FTP (Möglichkeit 1)
1. Sicherung der kompletten Datenbank über das `Backup`-Addon in Redaxo. 
Tipp: Zusätzlich die Tabelle `rex_user` mit auswählen, um die Redaxo-Benutzer mit zu kopieren.
2. Download der kompletten Redaxo-Installation über einen (S)FTP-Client
3. Upload der in Schritt 2 heruntergeladenen Dateien auf den Ziel-Server
4. Import der Datenbank-Sicherung in der neuen Datenbank, z.B. mit PHPMyAdmin oder Adminer.
5. Unter `/redaxo/data/core/config.yml` die Zeile `setup` von `false` auf `true` stellen.
6. Ebenfalls unter `/redaxo/data/core/config.yml` unterhalb der Zeile `db` die neuen Datenbank-Zugangsdaten einstellen.
7. Das Setup durchlaufen und in Schritt 4 des Setups keine Änderungen an der Datenbank vornehmen sowie keinen weiteren Administrator-Benutzer erstellen.
8. Anschließend einloggen und ggf. im Bereich `System` den Cache löschen.

## Via FTP (Möglichkeit 2)
1. Sicherung der kompletten Datenbank über das `Backup`-Addon in Redaxo. 
> Tipp: Zusätzlich die Tabelle `rex_user` mit auswählen, um die Redaxo-Benutzer mit zu kopieren.
2. Download der kompletten Redaxo-Installation über einen (S)FTP-Client
3. Upload der in Schritt 2 heruntergeladenen Dateien auf den Ziel-Server
4. Unter `/redaxo/data/core/config.yml` die Zeile `setup` von `false` auf `true` stellen.
5. Das Setup durchlaufen und in Schritt 4 des Setups die neuen Datenbank-Zugangsdaten angeben. Außerdem einen Test-Admin anlegen.
6. Mit dem Test-Admin einloggen und über das `Backup-Addon` die Datenbank-Sicherung einspielen. Achtung: Hierbei wird der gerade angelegte Test-Admin mit der `id=1` überschrieben.
7. Anschließend ggf. im Bereich `System` den Cache löschen.


# Umzug einer REDAXO Website

* [Allgemeines](#allg)
* [Umzug per Backup-AddOn](#ba)
* [Umzug mit manuellem Datenbank-Backup](#db)

<a name="allg"></a>

## Allgemeines

Um eine REDAXO-Installation von einem Server auf einen anderen Server zu übertragen, gibt es verschiedene Lösungswege. Im Regelfall müssen dazu das Dateisystem (REDAXO, einschließlich AddOns und Konfigurationsdateien) und die Datenbank umgezogen werden.

Falls sich dabei auch die verwendete (Sub-)Domain ändert, sollte nach dem Umzug im Bereich `System` die Domain angepasst werden. Wenn ein Rewrite-AddOn zum Einsatz kommt, müssen dort die Einstellungen ggf. vorab angepasst werden. Hierzu die Dokumentation des verwendeten AddOns unbedingt beachten.

Die nachfolgenden Lösungen zeigen den klassischen Weg via "FTP, SFTP, WebDAV"-Datensicherung.

> Tipps: Einige Hoster bieten zur Verwaltung des Webspaces auch Oberflächen wie PLESK oder CPANEL an. Hier enthalten ist auch ein Dateimanager, mit dem man die komplette Dateistruktur einer Webpräsenz zippen und entpacken kann. Websitebetreiber mit einem Shell-Zugriff können häufig auch einen direkten "Server zu Server"-Filefransfer z. B. per SCP durchführen.

<a name="ba"></a>

## Umzug per Backup-AddOn

* Die Datenbank der Quell-Präsenz wird mithilfe des [Backup](/{{path}}/{{version}}/backup)-AddOns ***auf dem Server*** gesichert.
* Download aller Ordner und Dateien der REDAXO-Installation, z. B. per SFTP (Transfer-Einstellungen des FTP-Programms auf `binary/binär` einstellen)
* Im Download unter `/redaxo/data/core/config.yml` die Zeile `setup` von `false` auf `true` stellen
* Die Dateien auf den Ziel-Server übertragen
* Website auf dem Ziel-Server aufrufen, das Setup wird aufgerufen
* Bei Schritt 4 die Zugangsdaten der neuen Datenbank angeben oder ggf. eine Datenbank anlegen
* Bei Schritt 5 unter ***vorhandenen Export einspielen:*** die Datensicherung auswählen
* Setup bis zum Ende durchführen - ***fertig*** (ggf. anschließend im Bereich `System` den Cache löschen)

<a name="db"></a>

## Umzug mit manuellem Datenbank-Backup

* Sicherung der kompletten Datenbank über das `Backup` -AddOn in REDAXO.
* Download aller Ordner und Dateien der REDAXO-Installation, z. B. per SFTP (Transfer-Einstellungen des FTP-Programms auf `binary/binär` einstellen)
* Upload der in Schritt 2 heruntergeladenen Dateien auf den Ziel-Server
* Import der Datenbank-Sicherung in der neuen Datenbank, z. B. mit PHPMyAdmin oder Adminer
* Unter `/redaxo/data/core/config.yml` die Zeile `setup` von `false` auf `true` stellen
* Ebenfalls unter `/redaxo/data/core/config.yml` unterhalb der Zeile `db` die neuen Datenbank-Zugangsdaten einstellen.
* Das Setup durchlaufen und in Schritt 4 des Setups ***Datenbank existiert schon*** auswählen. Die Anlage eines Administratorzugangs ist nicht erforderlich.
* Anschließend einloggen und ggf. im Bereich `System` den Cache löschen.

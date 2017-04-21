# Installation
Um mit REDAXO 4.x arbeiten zu können, muss das CMS auf einem Webserver installiert werden. REDAXO stellt sehr geringe Hardware-Anforderungen: PHP ab Version 4 und MySQL ab Version 4 sind ausreichend. Je nachdem, welche Features man nutzen möchte, sind zusätzliche Leistungsmerkmale des Servers Voraussetzung. Um URLs suchmaschinenfreundlich umzuwnandeln, benötigt muss der Server mod_rewrite unterstützen, und zum automatischen Verkleinern von Bildern muss der Server GDLib enthalten.

## Download und Upload

![Start der Installation](/assets/4-x-tutorial-installation-01.jpg)

Für jede Sprache stehen jeweils eine ISO- und UTF-8-Variante zur Wahl. Achtung: Je nach Zeichensatz des Frontends sollte auch im Backend der entsprechende Zeichensatz gewählt werden, damit die Daten korrekt in der Datenbank landen. Sprich: Wenn man eine Website in UTF-8 aufbauen will – was vor allem bei mehrsprachigen Websites mit fremden Zeichensätzen fast unabdingbar ist –, muss auch fü das Backend UTF-8 wählen.

Die hier gewählte Einstellung können jedoch noch nach der Installation geändert werden.

![Start der Installation](/assets/4-x-tutorial-installation-02.jpg)

## 1. Schritt

Im ersten Schritt werden die Ordner- und Dateirechte überprüft. Je nach Hoster kann es sein, dass man die Rechte der Konfigurationsdateien und des Cache-Ordners generated manuell anpassen muss.

![1.Schritt](/assets/4-x-tutorial-installation-03.jpg)

## 2. Schritt

Der zweite Schritt 2 fragt nach der Datenbankverbindung; diese erhält man vom Hoster.
Die optionalen Angaben (Serverdomain, Serverbezeichnung, Email-Adresse) sind nicht von Belang, aber man kann auf diese Systemvariablen in der Ausgabe oder in eigenen Programmierungen zugreifen und daurch diese Information zentral verwalten.

![2. Schritt](/assets/4-x-tutorial-installation-04.jpg)

## 3. Schritt

Unter den Optionen im dritten Schritt wählt man üblicherweise **Datenbank einrichten**. Falls man jedoch die Demo studieren will – und das ist zum Kennlernen von REDAXO durchaus sinnvoll –, wählt man **Vorhandenen Export einspielen [Demo einspielen]**.

Ein neues Projekt wird man zwar üblicherweise mit einer leeren Datenbank beginnen. Doch Profis benutzen auch gern einen selbst zusammen gestellten Export, der bereits alle benötigten Module enthält. Wenn man diesen Export in das Verzeichnis redaxo/include/addons/import_export/backup legt, steht der Export bei der Installation ebenfalls zur Auswahl.

![3. Schritt](/assets/4-x-tutorial-installation-05.jpg)

## 4. Schritt

Der vierte Schritt dient lediglich zum Anlegen des Administrator-Accounts.

![4. Schritt](/assets/4-x-tutorial-installation-06.jpg)

## 5. Schritt

Wenn man den fünften Schritt sieht, ist bereits alles geschafft: Ein Link führt zum Login, der üblicherweise unter der Adresse domain.de/redaxo/ zu finden ist.

![5. Schritt](/assets/4-x-tutorial-installation-07.jpg)


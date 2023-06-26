# Aktualisierung

* [Hinweise / bitte beachten](#hinweise)
* [Aktualisierung durchführen](#aktualisierung)
* [REDAXO auf utf8mb4 umstellen](#utf8mb4)

<a name="hinweise"></a>

## REDAXO up to date

Um den Betrieb in aktuellen Serverumgebungen und eine möglichst sichere Ausführung zu gewährleisten, wird REDAXO ständig weiterentwickelt. Je nach Version werden neue Funktionen, Fehlerkorrekturen oder Sicherheitsupdates bereitgestellt. Im Falle von Sicherheitsupdates sollten diese auf jeden Fall durchgeführt werden.

Mit dem [Installer-AddOn](/{{path}}/{{version}}/installer) bietet REDAXO hierfür eine komfortable Lösung.

## Hinweise

### Core-Upades

Allgemein ist es nicht erforderlich, die Core-Updates schrittweise durchzuführen. 

**Ausnahme:** 
Bei Versionen unter 5.6.5 sollte zunächst ein Update auf diese Version durchgeführt werden. 

Möchte man das System dennoch schrittweise aktualisieren, sollte das aktuelle Bugfix-Release des Feature-Release für die Update-Schritte genutzt werden. 
Beispiel: `5.11.2 -> 5.12.1 -> 5.13.3 -> 5.14.1 -> 5.15.1` 


### Datensicherung

Wenn Aktualisierungen am System oder an AddOns vorgenommen werden, sollte in jedem Fall vorher eine vollständige Sicherung des Systems durchgeführt werden. Dazu muss die Datenbank gesichert werden. Dies kann entweder über das Backup-AddOn oder über eigene Datenbanktools (z.B. PhpMyAdmin oder adminer) erfolgen. Bei einigen AddOns kann es auch sinnvoll sein, die Daten des AddOns selbst zu sichern, hierzu bitte die Dokumentation des AddOns beachten.

>Vor Aktualisierungen des Systems und AddOns sollten unbedingt die Versionshinweise beachtet werden. Möglicherweise werden bei einem Update Anpassungen am Code von Modulen, Templates oder anderen AddOns notwendig.



<a name="aktualisierung"></a>

## Aktualisierung durchführen

Um die Aktualisierungen über den Installer durchführen zu können, ist die Anmeldung im System als Benutzer mit dem Recht `Admin` notwendig. Der Installer ist dann über den Menüpunkt [Installer](/{{path}}/{{version}}/installer) erreichbar. Dort werden Updates aller Core-Versionen und AddOns aufgelistet, die über den Installer verfügbar sind.

![Aktualisierung](/assets/v.5.13.0-aktualisierung.png)

Falls ein Update für den REDAXO-Core (Kernsystem) verfügbar ist, wird dies am Anfang der Liste angezeigt. Wird ein Eintrag angeklickt, werden zunächst die Versionshinweise angezeigt. Ein Klick auf "Aktualisieren" aktualisiert das AddOn, bzw. das Core-System, und der Eintrag verschwindet aus der Liste.

Sofern die Liste leer ist, ist das System auf dem aktuellen Stand.

Es gibt Fälle, bei denen ein Update per Konsole notwendig ist, wenn z. B. Timeouts auftreten sollten. Hierzu eine aktuelle Version von REDAXO herunterladen und so vorgehen:

* `/redaxo/src/core` und `/redaxo/src/addons` mit denen aus der ZIP austauschen (eigene Addons sichern und zurückkopieren)
* in `/data/core/config.yml` "setup: true" setzen
* Setup durchlaufen lassen und dort "Update der Datenbank" auswählen; hier kann alternativ auch per CLI "Update database" ausgeführt werden:
`php redaxo/bin/console setup:run`

<a name="utf8mb4"></a>

## REDAXO auf utf8mb4 umstellen

> Es sollte vorher ein Backup der Datenbank durchgeführt werden.

REDAXO unterstützt seit Version 5.9 vollständig utf8mb4, dies ermöglicht die vollständige Darstellung des UTF-8 Zeichensatzes inkl. Emojis.

Nach einem Update im Installer ist noch eine Konvertierung der Datenbank erforderlich.

* Hierzu im System das Setup starten und dieses ohne Änderungen bis zum Schritt **5 Datenbank** durchlaufen.
* Das Setup prüft, ob utf8mb4 vom Server unterstützt wird. Anschließend `Aktualisierung der Datenbank` und `utf8mb4 [emphohlen]` auswählen.
* Durch Bestätigung zum nächsten Schritt wird die Datenbank konvertiert.

Die Einrichtung eines Benutzers ist nicht erforderlich und kann übersprungen werden.

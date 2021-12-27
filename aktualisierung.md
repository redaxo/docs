# Aktualisierung

* [Hinweise](#hinweise)
* [Aktualisierung durchführen](#aktualisierung)
* [REDAXO auf utf8mb4 umstellen](#utf8mb4)

<a name="hinweise"></a>

## REDAXO up to date

REDAXO wird ständig weiterentwickelt um den Betrieb unter aktuellen Serverumgebungen zu gewährleisten. Je nach Version erhält man neue Funktionen, Fehlerkorrekturen oder Sicherheitsaktualisierungen. Bei Sicherheitsaktualisierungen sollte dies unbedingt durchgeführt werden.   

Hierzu bietet REDAXO eine komfortable Lösung mit dem Installer-AddOn an. 


## Hinweise

**Wichtiger Hinweis:** Wenn Aktualisierungen am System oder an AddOns vorgenommen werden, sollte in jedem Fall vorher eine komplette Sicherung des Systems gemacht werden. Hierzu muss die Datenbank gesichert werden. Dies kann entweder über das Backup-AddOn oder über eigene Datenbanktools (z. B. phpmyAdmin oder adminer) erledigt werden. Bei AddOns kann es auch sinnvoll sein, die Dateien des AddOns selbst zu sichern.

>Vor Aktualisierungen des Systems und AddOns sollten unbedingt die Versionshinweise beachtet werden. Möglicherweise werden bei einem Update Anpassungen am Code von Modulen, Templates oder anderen AddOns notwendig.

<a name="aktualisierung"></a>

## Aktualisierung durchführen

Um die Aktualisierungen über den Installer durchführen zu können, muss man im System als Person mit dem Recht `Admin` eingeloggt sein. Zum Installer gelangt man dann über den Menüpunkt [Installer](/{{path}}/{{version}}/installer). Dort werden alle Core-Versionen und AddOns aufgelistet, die über den Installer aktualisiert werden können.

![Aktualisierung](/assets/v.5.13.0-aktualisierung)

Falls ein Update für den REDAXO-Core (Kernsystem) verfügbar ist, wird dies am Anfang der Liste angezeigt. Klickt man dort auf einen Eintrag, werden zunächst die Versionshinweise angezeigt. Ein Klick auf "Aktualisieren" aktualisiert das AddOn, bzw. das Core-System, und der Eintrag verschwindet aus der Liste.

Sofern die Liste leer ist, ist das System auf dem aktuellen Stand.

Es gibt Fälle, wo ein Update per Konsole notwendig ist, wenn z. B. Timeouts auftreten sollten. Hierzu kann man das aktuelle Redaxo-ZIP herunter laden und so vorgehen:

* /redaxo/src/core und /redaxo/src/addons mit denen aus der ZIP austauschen (eigene Addons sichern und zurück kopieren)
* in /data/core/config.yml "setup: true" setzen
* Setup durchlaufen lassen und dort "Update der Datenbank" auswählen; hier kann alternativ auch per CLI "Update database" ausgeführt werden:
php redaxo/bin/console setup:run

<a name="utf8mb4"></a>

## REDAXO auf utf8mb4 umstellen

> Es sollte vorher ein Backup der Datenbank durchgeführt werden.

REDAXO unterstützt seit Version 5.9 vollständig utf8mb4, dies ermöglicht die vollständige Darstellung des UTF-8 Zeichensazes inkl. Emojis.

Nach einem Update im Installer ist noch eine Konnvertierung der Datenbank erforderlich.

* Hierzu startet man im System das Setup und geht dieses durch ohne Änderungen bis zum Schritt **5 Datenbank**.
* Das Setup prüft ob utf8mb4 vom Server unterstützt wird. Anschließend wählt man `Aktualisierung der Datenbank` und `ùtf8mb4 [emphohlen]` aus.
* Durch Bestätigung zum nächsten Schritt wird die Datenbank konvertiert.

Die Einrichtung eines Benutzers ist nicht erforderlich und kann übersprungen werden.

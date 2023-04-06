# Installer

Für die Aktualisierung von REDAXO, den Download und die Installation neuer AddOns ist der Installer die zentrale Anlaufstelle. Updates des Systems und der AddOns werden im Bereich `Vorhandene aktualisieren` angezeigt. Unter dem Reiter `Neues herunterladen` befindet sich eine Übersicht der verfügbaren AddOns. Dort werden die AddOns beschrieben und stehen zum Download zur Verfügung. 

Die Installation eines neu heruntergeladenen AddOns ist direkt nach dem Download möglich.  
Unter Einstellungen kann festgelegt werden, dass Backups erstellt werden. Bei einer Aktualisierung werden Backups der alten AddOn-Verzeichnisse bzw. bei einem Core-Update der entsprechenden Core-Verzeichnisse erstellt. Diese werden unter `redaxo/data/addons/install/` abgelegt. Eine Sicherung der Datenbank wird aber **nicht** durchgeführt! Dies kann z.B. über das [Backup-AddOn](/{{path}}/{{version}}/backup) erfolgen.

* [Vorhandene Aktualisieren](#aktualisieren)
* [Neue AddOns herunterladen](#herunterladen)
* [AddOn installieren ](#installieren)
* [Eigende AddOns hochladen](#hochladen)


<a name="aktualisieren"></a>

## Vorhandene Aktualisieren

![Aktualisieren](/assets/v5.15.0-installer-00-aktualisieren.png)

Im Bereich "Vorhandene Aktualisieren" sieht man, welche AddOns und Bestandteile des Kernsystems (Core) aktualisiert werden können. Bevor ein Update durchgeführt wird, wird dringend empfohlen, die Release Notes (Versionshinweise) zu lesen.

Durch Anklicken des Namens (key) erhält man Informationen über die neuen Versionen.

![Versionen](/assets/v5.2.0-installer-03-versionen.png)

> Manchmal ist es erforderlich, Anpassungen nach einem Update durchzuführen. Ist man sich hierbei nicht sicher, was zu tun ist, sollte man besser alles vorerst belassen wie es ist und das jeweilige Update besser nicht ausführen. Kontaktiere gegebenenfalls die Community, die Agentur oder den Entwickler die für Dich die Website erstellt haben.

<a name="herunterladen"></a>

## Neue AddOns herunterladen

![Download](/assets/v5.2.0-installer-02-neue.png)

Neue AddoOns lädt man über den Reiter `Neue Herunterladen`. Hier findet man eine Liste der AddOns und ein paar Informationen wie Autor, Kurzbeschreibung. Weiterführende Informationen zum AddOn und zu den Versionen, erhält man nach Klick auf `Ansehen` oder dem AddOn-Namen. Um das AddOn herunterzuladen, klickt man bei der gewünschten Version auf `herunterladen`. 


Anschließend kann man das AddOn unter "AddOns" installieren.

<a name="installieren"></a>
## AddOn installieren 

Bis Version 5.15 konnte man ein AddOn nur in der AddOnverwaltung installieren. Seit 5.15 ist es möglich die Installation direkt nach dem Herunterladen zu installieren und zu aktivieren. 

![Installation](/assets/v5.15.0-installer-01-installieren.png)

<a name="hochladen"></a>

## Eigene AddOns hochladen

Entwickler können eigene AddOns direkt aus der REDAXO-Installation heraus in den Downloadbereich von redaxo.org hochladen und zum Download bereitstellen. Die AddOns stehen danach im Installer und auf der Website redaxo.org zum Download bereit. Hierzu benötigt man einen API-Key, den man im eigenen myREDAXO-Account einsehen kann.

Weitere Informationen zur Erstellung und Bereitstellung eigener AddOns im Kapitel [Veröffentlichung](/{{path}}/{{version}}/addon-veroeffentlichung).

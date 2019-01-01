# Installer

Der Installer ist die zentrale Anlaufstelle, um REDAXO zu aktualisieren und neue AddOns herunterzuladen. Updates des Systems und des AddOns werden im Abschnitt `Vorhandene aktualisieren` angezeigt. Neue AddOns (Erweiterungen des Systems) kann man im Abschnitt `Neue herunterladen` anzeigen und in das System laden.

Neu heruntergeladene AddOns werden nicht automatisch installiert. Die abschließende Installation und Aktivierung erfolgt beim Menüpunkt "AddOns".
Aktualisierungen finden dagegen automatisch statt.
Im Addon unter Einstellungen kann festgelegt werden, dass Backups erstellt werden sollen. Bei Aktuallisierungen werden Backups der alten AddOn-Ordner bzw. bei einem Core-Update der entsprechenden Core-Verzeichnisse erstellt und unter `redaxo/data/addons/install/` abgelegt. Ein Datenbankbackup wird jedoch **nicht** ausgeführt! Dieses kann z.B. über das [Backup-AddOn](/{{path}}/{{version}}/backup) erfolgen.

- [Vorhandene Aktualisieren](#aktualisieren)
- [Neue Addons herunterladen](#herunterladen)
- [Eigende Addons hochladen](#hochladen)

<a name="aktualisieren"></a>

## Vorhandene Aktualisieren

![Systemcheck](/assets/v5.2.0-installer-01-aktualisieren.png)

Im Bereich "Vorhandene Aktualisieren" sieht man, welche AddOns und Bestandteile des Kernsystems (Core) aktualisiert werden können. Vor der Durchführung einer Aktualisierung sollten unbedingt die Versionshinweise beachtet werden. **Vor Aktualierungen von Addons und Core sollte ein Backup durchgeführt werden.**

Die Informationen zur neuen Version erhält man, wenn man den Namen (key) anklickt. Dort werden auch ggf.  weitere zur Verfügung stehende Versionen angezeigt.

![Systemcheck](/assets/v5.2.0-installer-03-versionen.png)

> Manchmal ist es erforderlich, Anpassungen nach einem Update durchzuführen. Ist man sich hierbei nicht sicher sein, was zu tun ist, sollte man besser alles vorerst belassen wie es ist und das jeweilige Update besser nicht ausführen. Kontaktiere gegebenenfalls die Agentur oder den Entwickler, der für Dich die Website erstellt hat. 

<a name="herunterladen"></a>
## Neue Addons herunterladen

![Systemcheck](/assets/v5.2.0-installer-02-neue.png)


Neue AddoOns lädt man über den Reiter `Neue Herunterladen`. Hier findet man eine Liste der AddOns und ein paar Informationen wie Autor, Kurzbeschreibung. Um mehr über das AddOn zu erfahren, kann man den Addon-Namen anklicken oder Ansehen anklicken. Um das Addon herunterzuladen, klickt man bei der gewünschten Version auf `herunterladen`. 

Anschließend kann man das Addon unter "Addons" installieren. 

<a name="hochladen"></a>
## Eigene Addons hochladen
Entwickler können eigene Addons direkt aus der REDAXO-Installation heraus in den Downloadbereich von redaxo.org hochladen und zum Download bereitstellen. Die Addons stehen danach im Installer und auf der Website redaxo.org zum Download bereit. Hierzu benötigt man einen API-Key, den man im eigenen myRedaxo-Account einsehen kann. 

Weitere Informationen zur Erstellung und Bereitstellung eigener Addons im Kapitel [Veröffentlichung](/{{path}}/{{version}}/addon-veroeffentlichung).



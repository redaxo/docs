# Troubleshooting CSRF-Token

## Hintergrund

CSRF steht für Cross-Site Request Forgery. Es handelt sich dabei um eine Art von Angriff, bei dem ein Angreifer eine Anfrage an eine Website sendet, die der Benutzer bereits authentifiziert hat. Dadurch kann der Angreifer Aktionen im Namen des Benutzers ausführen, ohne dass dieser davon Kenntnis hat. 

Um sich vor CSRF-Angriffen zu schützen, verwenden viele Websites Anti-CSRF-Token, die in Formularen eingebettet sind und bei jeder Anfrage überprüft werden.

**Grundsätzlich ist das Deaktivieren des CSRF-Schutzes nicht empfehlenswert, da es die Sicherheit des Systems gefährdet.**

## Ursachen für CSRF-Fehler in REDAXO (Allgemein)

### Ursache 1: Quota überschritten

Einzelne Webhosting-Anbeiter haben auch heute noch Quotas für die **Anzahl der Dateien** und den **Gesamtspeicherplatz**, die ein Benutzer in seinem Webspace speichern darf. Wenn diese Quota überschritten wird, kann es zu Problemen kommen, da auch das Schreiben temporärer Dateien (z.B. für die Session und damit das CSRF-Token) nicht mehr möglich ist.

#### Lösung für überschrittene Quotas

- Prüfe, ob Quotas existieren und weshalb diese überschritten wurden.
- Lösche ggf. nicht mehr benötigte Dateien.

### Ursache 2: Fehlende Schreibrechte

Wenn REDAXO nicht die nötigen Schreibrechte hat, um temporäre Dateien zu erstellen, kann es zu Problemen kommen, da auch das Schreiben temporärer Dateien (z.B. für die Session und damit das CSRF-Token) nicht mehr möglich ist.

### Ursache 3: Session Autostart

Ist in den PHP-Einstellungen "session.auto_start" aktiviert, wird empfohlen, dies zu deaktivieren, um Probleme zu vermeiden. <https://github.com/redaxo/redaxo/issues/5733>

#### Lösung für Session Autostart

- Prüfe, ob "session.auto_start" aktiviert ist.
- Deaktiviere ggf. "session.auto_start"

#### Lösung für fehlende Schreibrechte

- Prüfe, ob die Schreibrechte für REDAXO korrekt gesetzt sind.

## Ursachen speziell innerhalb von YForm

### Ursache 1-3: Siehe REDAXO Allgemein

Die Ursachen 1-3 können auch innerhalb von YForm auftreten. Siehe dazu die Lösungen unter "REDAXO Allgemein".

### Ursache 4: Veraltete YTemplates

Werden ältere YTemplates geladen, die noch nicht kompatibel mit einer aktuellen YFORM-Version sind, kann dies sich in einem CSRF-Token-Fehler äußern. Mögliche Speicherorte: Theme-Addon, Project-Addon, eigene-Addons.

#### Lösung für veraltete YTemplates

- Prüfe, ob die YTemplates kompatibel mit der verwendeten YFORM-Version sind.
- Lösche ggf. nicht mehr benötigte YTemplates.
- Aktualisiere ggf. die YTemplates.

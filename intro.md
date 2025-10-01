# Dokumentation REDAXO 5.16 – 5.20.x

Die REDAXO-Dokumentation ist der Startpunkt für die Installation und Redaktion einer REDAXO-Webpräsenz. Zudem finden Developer hier auch die erforderlichen Informationen zur Entwicklung eigener Lösungen.

> Wir freuen uns sehr über Mitarbeit bei der REDAXO-Dokumentation. Derzeit arbeiten Peter Bickel, Thomas Skerbis, Wolfgang Bund und Alexander Walther an der Dokumentation.

>Unterstützung wird immer benötigt; die Dokumentation wird in [GitHub gepflegt und erweitert](https://github.com/redaxo/docs), sodass sich alle beteiligen können. Neue Artikel oder Verbesserungen können gerne per Pull-Request oder Issues eingereicht werden.
[Zur Dokumentation auf GitHub](https://github.com/redaxo/docs).



## Neues in dieser Doku

**Sicherheit und Konfiguration**
- [REDAXO absichern](/{{path}}/{{version}}/absichern): Umfassendes Kapitel zur Absicherung des Backends mit Live-Mode und Security AddOn
- [Live-Mode](/{{path}}/{{version}}/absichern#livemode): Sicherheitsmodus für Live-Systeme zur Einschränkung von PHP-Code-Ausführung
- [Security AddOn](/{{path}}/{{version}}/absichern#securityaddon): AddOn für erweiterte Backend-Sicherheit mit IP-Kontrolle und Benutzerprotokoll
- [MediaPool-Sicherheit](/{{path}}/{{version}}/medienpool#mime-typen-sicherheit): MIME-Type-Prüfung und SVG-Bereinigung für sicheren Datei-Upload
- [Safe Mode Enhancement](/{{path}}/{{version}}/configyml#safe-mode): Erweiterte Admin-Beschränkungen und globale Konfiguration
- [Datenbank-SSL](/{{path}}/{{version}}/configyml#datenbank-ssl): Sichere Datenbankverbindungen mit Zertifikatsprüfung
- [Backend Login Policies](/{{path}}/{{version}}/configyml#login-policies): Brute-Force-Schutz mit konfigurierbaren Limits und Verzögerungen

**Entwicklung und APIs**
- [`rex_file::append`](/{{path}}/{{version}}/file#rexfile_append): Erweiterte Dokumentation der append-Methode zum Anhängen von Content an Dateien
- [Namespace-Unterstützung](/{{path}}/{{version}}/api#namespace-registrierung): Explizite Registrierung für API-Funktionen und REX_VAR-Klassen
- [Request-Validierung](/{{path}}/{{version}}/requests#explizite-werte): Validierung mit expliziten Werte-Arrays für rex_get() und rex_post()
- [Extension Points](/{{path}}/{{version}}/extension-points#page-structure-orderby): Neuer Extension Point für benutzerdefinierte Struktursortierung
- [Template-Übersetzungen](/{{path}}/{{version}}/templates#template-namen-uebersetzen): Automatische Übersetzung von Template-Namen mit translate:template_name Format

**Medien und Tools**
- [Video-Vorschau](/{{path}}/{{version}}/media-manager#video-vorschau): Media Manager Integration mit ffmpeg für automatische Video-Thumbnails
- [Console Autocompletion](/{{path}}/{{version}}/console#autocompletion): Integrierte Autovervollständigung für Package-, User- und Datenbank-Befehle
- [Formular-Validierung](/{{path}}/{{version}}/formulare#erweiterte-validierung): Verbesserte Unique-Constraint-Validierung mit benutzerdefinierten Fehlermeldungen

## Übersicht der Kategorien

**Einleitung**

Grundlegende Informationen zur aktuellen Version, Aktualisierung, API

**Setup und Administration**

Installationsanleitung, erster Login, Passwort-Wiederherstellung

**Anwender**

Der Bereich für Anwender ist primär an Redakteurinnen und Redakteure gerichtet. Hier wird die Bedienung des Systems erläutert.

**Basis**

Grundlegende technische Informationen zum Aufbau einer REDAXO-Webpräsenz

**Service**

Informationen für Developer

**Weitere System AddOns / PlugIns**

Informationen zu System Addons

**AddOn-Entwicklung**

Entwicklung und Bereitstellung eigener AddOns

**Datenbank**

Datenbankabfragen, Tabellen ändern und Prioritäten

# config.yml

* [Einleitung](#plugin)
* [Speicherort](#speicherort)
* [Aufbau](#aufbau)
* [Auslesen der Einstellungen](#config)
* Beispiele
  * [Passwort-Policies anpassen](#policies)

<a name="einleitung"></a>

## Einleitung

In der config.yml werden die für den Betrieb des Projektes erforderlichen Einstellungen hinterlegt. Hierzu gehören die bei der Installation gemachten Angaben und weitere allgemeine Einstellungen, die individuell angepasst werden können. Nicht alle Einstellungen sind über das Backend von REDAXO erreichbar. Diese müssen bei Bedarf direkt in der Datei gepflegt werden. 

<a name="speicherort"></a>

## Speicherort

Der Speicherort ist `redaxo/data/core/config.yml`

> Die config.yml wird bei einem Update nicht überschrieben und ist daher updatesicher.

<a name="aufbau"></a>

##  Aufbau

```yml
setup: false
debug:
    enabled: false
    throw_always_exception: false
instname: rex20201222171044
server: 'https://domain.tld/'
servername: 'REDAXO Website'
error_email: user@domain.tld
fileperm: '0664'
dirperm: '0775'
session_duration: 7200
session_keep_alive: 21600
session:
    backend:
        cookie: { lifetime: null, path: null, domain: null, secure: null, httponly: true, samesite: Lax }
    frontend:
        cookie: { lifetime: null, path: null, domain: null, secure: null, httponly: true, samesite: Lax }
password_policy:
    length:
        min: 8
        max: 4096
    lowercase:
        min: 0
    uppercase:
        min: 0
    digit:
        min: 0
    reuse_previous:
        not_last: 6
        not_months: 12
    validity:
        renew_months: 12
        block_months: 24
lang: de_de
lang_fallback:
    - en_gb
    - de_de
use_https: false
use_hsts: false
hsts_max_age: 31536000
use_gzip: true
use_etag: true
use_last_modified: false
start_page: structure
timezone: Europe/Berlin
socket_proxy: null
setup_addons:
    - backup
    - be_style
system_addons:
    - backup
    - mediapool
    - structure
    - metainfo
    - be_style
    - media_manager
    - users
    - install
    - project
table_prefix: rex_
temp_prefix: tmp_
db:
    1:
        host: localhost
        login: dbuser
        password: XXXXXXXXX
        name: dbname
        persistent: false
        ssl_key: null
        ssl_cert: null
        ssl_ca: null
    2:
        host: ''
        login: ''
        password: ''
        name: ''
        persistent: false
        ssl_key: null
        ssl_cert: null
        ssl_ca: null
use_accesskeys: true
accesskeys:
    save: s
    apply: x
    delete: d
    add: a
    add_2: 'y'
editor: null
editor_basepath: null
theme: null

```
| Knoten | Subknoten |  | Werte | Beschreibung |
| ------ | --------- | --- | ----- | ------------ |
| setup |  |  | true/ false/ hash+DayTime | Legt fest, ob das Setup ausgeführt werden soll. Bei true wird das Setup ausgeführt. Wird das Setup über das Backend gestartet findet sich hier ein Hash und eine DateTime-Angabe die festlegt bis wann der Setupaufruf gültig ist. |
| debug | enabled |  | true/false | Startetet oder beenden den Debug-Modus |
|  | throw\_always\_exception |  | true/false | Legt fest ob Exceptions immer ausgegeben werden sollen |
| instname |  |  | rex… | Eindeutiger Installationsname, Beispiel: rex20201222171044 |
| server |  |  | url | Url zum Frontend der Website |
| servername |  |  | string | Name der Website (wird meist im Titel ausgegeben) |
| error\_email |  |  | E-Mail-Adresse | E-Mail-Adresse an die Fehlerberichte geschickt werden sollen. |
| fileperm |  |  | digit | Legt die allgemeinen Rechte für Dateien fest, z.B.: 0664 |
| dirperm |  |  | digit | Legt die allgemeinen Rechte für Ordner fest, z.B.: 0775 |
| session\_duration |  |  | Sekunden | Legt die Session-Dauer fest |
| session\_keep\_alive |  |  | Sekunden | Legt den Keep live-Zeitraum für die Session fest |
| session | backend | cookie |  | Hier werden Einstellungen für das Cookie-Handling im Backend festgelegt.<br>Dazu gehören u.a Pfadangabe zur Cookie-Speicherung, Domain und Laufzeit |
|  | frontend<br>  | cookie |  | Hier werden Einstellungen für das Cookie-Handling im Frontend festgelegt. |
| <span class="colour" style="color:var(--color-prettylights-syntax-entity-tag)">password\_policy</span> | length |  | digit | Hier können Angaben zur minimalen und maximalen Zeichenlänge für Passwörter festgelegt werden |
|  | lowercase |  | digit | Angabe wieviele Kleinbuchstaben das Passwort enthalten muss |
|  | uppercase |  | digit | Angabe wieviele Großbuchstaben das Passwort enthalten muss |
|  | <span class="colour" style="color:var(--color-prettylights-syntax-entity-tag)">digit</span> |  | digit | Wieviele Zahlen soll das Passwort enthalten |
|  | reuse\_previous | not\_last |  | Wie viele der zuletzt benutzten Passwörter dürfen nicht erneut verwendet werden. Im Beispiel dürfen also die letzten 6 Passwörter nicht erneut verwendet werden |
|  |  | not\_last |  | Nach wie viel Monaten darf ein Passwort erneut verwendet werden |
|  | validity | renew\_months |  | Nach wie viel Monaten wird eine Passwortänderung nach dem Login erzwungen. |
|  |  | block\_months |  | <span class="highlight" style="background-color:rgb(255, 255, 255)"><span class="colour" style="color:rgb(36, 41, 46)"><span class="font" style="font-family:-apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;"><span class="size" style="font-size:14px">Nach wie viel Monaten ohne Passwortänderung wird der Account gesperrt</span></span></span></span> |
| lang |  |  | Sprachcode | Hier wird die default-Sprache festgelegt (Konfigurierbar im System) |
| <span class="colour" style="color:var(--color-prettylights-syntax-entity-tag)">lang\_fallback</span> |  |  | Sparchcodes | Legt das Verhalten fest auf welche Sprachen REDAXO zurückspringen soll, wenn eine Übersetzung nicht gefunden wird. |
| use\_https |  |  | true, false, frontend, backend | Legt fest ob https für Frontend und / oder Backend genutzt werden soll. |
| use\_hsts |  |  | true / false | Aktiviert HSTS (HTTP Strict Transport Security) |
| hsts\_max\_age |  |  | Sekunden | Legt die Laufzeit der HSTS-Einstellung fest |
| <span class="colour" style="color:var(--color-prettylights-syntax-entity-tag)">use\_gzip</span> |  |  | true / false | Aktiviert oder deaktiviert die GZIP-Kompression |
| use\_etag |  |  | true / false | Legt fest ob etag-Header ausgeliefert werden sollen |
| use\_last\_modified |  |  | true / false | Legt fest ob ein last modified header ausgeliefert werden soll |
| start\_page |  |  | addonkey | Legt die Standard-Startseite im Backend fest. ( Kann je Nutzer im Backend überschrieben werden) |
| timezone |  |  | Zeitzone | Beispiel: <span class="colour" style="color:var(--color-prettylights-syntax-string)">Europe/Berlin</span> |
| socket\_proxy |  |  | IP:Port | Legt die Einstellungen  für einen Socket proxy fest |
| setup\_addons |  |  | AddOn-Keys | Legt die AddOns fest, die während der Installation aktiv sein sollen |
| system\_addons |  |  | AddOn-Keys | Legt die System-Addons fest. Sie werden automatisch installiert und sind auch im Debug-Modus verfügbar. |
| table\_prefix |  |  | string | Legt das Prefix für die Tabellen fest, default rex\_ |
| temp\_prefix |  |  | string | Legt das Prefix für temporäre Tabellen fast, default temp\_. Diese Tabellen werden bei einem Backup nicht beachtet. |
| db | 1 |  |  | Legt die Verbindungseinstellungen für die Hauptdatenbank(1) und Pfade für eine TLS-Verbindung fest. |
|  | 2 |  |  | Legt die Verbindungseinstellungen für die optionale 2. Datenbank und Pfade für eine TLS-Verbindung fest. |
| use\_accesskeys |  |  | true / false | Sollen Accesskeys zur vereinfachten Bedienung im Backend angeboten werden? |
| accesskeys | save |  | char | Accesskey Speichern |
|  | apply |  | char | Accesskey Übernehmen |
|  | delete |  | char | Accesskey Löschen |
|  | add |  | char | Accesskey Hinzufügen |
|  | add\_2 |  | char | Accesskey Hinzufügen, alternativ |
| editor |  |  | Config-Wert | Legt den externen Code-Editor fest |
| editor\_basepath |  |  | Pfad | Ersetzt den tatsächlichen Basis-Pfad der Installation mit dem hier angegebenen lokalen Pfad (nützlich für Produktivumgebungen, Docker etc.). |
| theme |  |  | null / light / dark | Legt das Backend-Theme fest und deaktiviert damit die Theme-Auswahl für Nutzer |

<a name="config"></a>

## Auslesen der Einstellungen

Das Auslesen der Einstellungen wird im Kapitel zur [Konfiguration (rex_config)](/{{path}}/{{version}}/konfiguration) erklärt. 

## Beispiele

<a name="policies"></a>

### Passwort-Policies anpassen 

Festlegen der Passwortregeln zur Verpflichtung der Redakteure neue Passwörter nach einem bestimmten Zeitraum festzulegen

```yaml
password_policy:
    length:
        min: 8
        max: 4096
    lowercase:
        min: 1
    uppercase:
        min: 1
    reuse_previous:
        not_last: 6
        not_months: 12
    validity:
        renew_months: 12
        block_months: 24
```

Über die Keys `reuse_previous` und `validity` lassen sich folgende Einstellungen steuern:
* `reuse_previous`:
    - `not_last`: Wie viele der zuletzt benutzten Passwörter dürfen nicht erneut verwendet werden. Im Beispiel dürfen also die letzten 6 Passwörter nicht erneut verwendet werden
    - `not_months`: Nach wie viel Monaten darf ein Passwort erneut verwendet werden
    
Wird beides gesetzt, gilt auch beides. Im Beispiel dürfen also sowohl die letzten 6 Passwörter, als auch alle Passwörter aus den letzten 12 Monaten nicht verwendet werden
* `validity`:
    - `renew_months`: Nach wie viel Monaten wird eine Passwortänderung nach dem Login erzwungen.
    - `block_months`: Nach wie viel Monaten ohne Passwortänderung wird der Account gesperrt

Im Beispiel muss man also nach 12 Monaten das Passwort ändern. Dazu wird man nach dem LogIn zwangsweise auf das Profil geleitet, mit der Warnung, dass man das Passwort ändern muss. Versucht man aber erst nach 24 Monaten sich wieder einzuloggen, ist man gesperrt, man gelangt also auch nicht mehr zum Profil, um das Passwort zu ändern. Diese Aufgabe muss dann ein Admin erledigen.


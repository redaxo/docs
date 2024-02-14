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
setup: true
live_mode: false
safe_mode: false
debug:
    enabled: false
    throw_always_exception: false # `true` for all error levels, `[E_WARNING, E_NOTICE]` for subset
instname: null
server: https://www.redaxo.org/
servername: REDAXO
error_email: null
fileperm: '0664'
dirperm: '0775'
session_duration: 7200
session_keep_alive: 21600
session_max_overall_duration: 2419200 # 4 weeks
backend_login_policy:
    login_tries_until_blocked: 50
    login_tries_until_delay: 3
    relogin_delay: 5
    enable_stay_logged_in: true
# using separate cookie domains for frontend and backend is more secure,
# but be warned that some features like detecting a backend user in the frontend
# will no longer work.
session:
    backend:
        # save_path:
        # sid_length:
        # sid_bits_per_character:
        cookie:
            lifetime: null
            path: null
            domain: null
            secure: null
            httponly: true
            samesite: 'Lax'
    frontend:
        # save_path:
        # sid_length:
        # sid_bits_per_character:
        cookie:
            lifetime: null
            path: null
            domain: null
            secure: null
            httponly: true
            samesite: 'Lax'
password_policy:
    length: {min: 8, max: 4096}
    lowercase: {min: 0}
    uppercase: {min: 0}
    digit: {min: 0}
    # no_reuse_of_last: 6
    # format analog https://www.php.net/manual/de/dateinterval.construct.php
    # no_reuse_within: P6W
    # force_renew_after: P6W
    # block_account_after: P3M
lang: en_gb
lang_fallback: [en_gb, de_de]
use_https: false
use_hsts: false
hsts_max_age: 31536000 # 1 year
use_gzip: false
use_etag: true
use_last_modified: false
start_page: structure
timezone: Europe/Berlin
socket_proxy: null
setup_addons:
    - backup
    - be_style
    - install
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
        login: root
        password: ''
        name: redaxo5
        persistent: false
        ssl_key: null
        ssl_cert: null
        ssl_ca: null
        ssl_verify_server_cert: true
    2:
        host: ''
        login: ''
        password: ''
        name: ''
        persistent: false
        ssl_key: null
        ssl_cert: null
        ssl_ca: null
        ssl_verify_server_cert: true
use_accesskeys: true
accesskeys:
    save: s
    apply: x
    delete: d
    add: a
    add_2: y
editor: null
editor_basepath: null
theme: null
```

| Knoten | Subknoten |  | Werte | Beschreibung |
| ------ | --------- | --- | ----- | ------------ |
| setup |  |  | true/ false/ hash+DayTime | Legt fest, ob das Setup ausgeführt werden soll. Bei true wird das Setup ausgeführt. Wird das Setup über das Backend gestartet findet sich hier ein Hash und eine DateTime-Angabe die festlegt bis wann der Setupaufruf gültig ist. |
| live |  |  | true/false | Im Live-Mode wird das System gehärtet, sodass ein gekaperter Backend-Admin-Account weniger Schaden anrichten kann. |
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
|  | frontend | cookie |  | Hier werden Einstellungen für das Cookie-Handling im Frontend festgelegt. |
| length |  | digit | Hier können Angaben zur minimalen und maximalen Zeichenlänge für Passwörter festgelegt werden |
|  | lowercase |  | digit | Angabe wieviele Kleinbuchstaben das Passwort enthalten muss |
|  | uppercase |  | digit | Angabe wieviele Großbuchstaben das Passwort enthalten muss |
|  |  | digit | Wieviele Zahlen soll das Passwort enthalten |
|  | reuse\_previous | not\_last |  | Wie viele der zuletzt benutzten Passwörter dürfen nicht erneut verwendet werden. Im Beispiel dürfen also die letzten 6 Passwörter nicht erneut verwendet werden |
|  |  | not\_last |  | Nach wie viel Monaten darf ein Passwort erneut verwendet werden |
|  | validity | renew\_months |  | Nach wie viel Monaten wird eine Passwortänderung nach dem Login erzwungen. |
|  |  | block\_months |  |
| lang |  |  | Sprachcode | Hier wird die default-Sprache festgelegt (Konfigurierbar im System) |
|  |  | Sparchcodes | Legt das Verhalten fest auf welche Sprachen REDAXO zurückspringen soll, wenn eine Übersetzung nicht gefunden wird. |
| use\_https |  |  | true, false, frontend, backend | Legt fest ob https für Frontend und / oder Backend genutzt werden soll. |
| use\_hsts |  |  | true / false | Aktiviert HSTS (HTTP Strict Transport Security) |
| hsts\_max\_age |  |  | Sekunden | Legt die Laufzeit der HSTS-Einstellung fest |
|  |  | true / false | Aktiviert oder deaktiviert die GZIP-Kompression |
| use\_etag |  |  | true / false | Legt fest ob etag-Header ausgeliefert werden sollen |
| use\_last\_modified |  |  | true / false | Legt fest ob ein last modified header ausgeliefert werden soll |
| start\_page |  |  | addonkey | Legt die Standard-Startseite im Backend fest. ( Kann je Nutzer im Backend überschrieben werden) |


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


# config.yml

* [Einleitung](#plugin)
* [Speicherort](#speicherort)
* [Aufbau](#aufbau)
* [Auslesen der Einstellungen](#config)
* Beispiele
  * [Passwort-Policies anpassen](#policies)
* [Hinweise: https/hsts-config](#https-config)

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
| debug | enabled |  | true/false | Startetet oder beenden den Debug-Modus |
| live_mode |  |  | true/false | Aktiviert oder deaktiviert den Live-Modus. Mehr dazu unter [REDAXO absichern](/{{path}}/{{version}}/absichern) |
| safe_mode |  |  | true/false | Aktiviert oder deaktiviert den Safe-Modus global. Siehe [Safe Mode konfigurieren](#safe-mode) |
|  | throw\_always\_exception |  | true/false | Legt fest ob Exceptions immer ausgegeben werden sollen |
| instname |  |  | rex… | Eindeutiger Installationsname, Beispiel: rex20201222171044 |
| server |  |  | url | Url zum Frontend der Website |
| servername |  |  | string | Name der Website (wird meist im Titel ausgegeben) |
| error\_email |  |  | E-Mail-Adresse | E-Mail-Adresse an die Fehlerberichte geschickt werden sollen. |
| fileperm |  |  | digit | Legt die allgemeinen Rechte für Dateien fest, z.B.: 0664 |
| dirperm |  |  | digit | Legt die allgemeinen Rechte für Ordner fest, z.B.: 0775 |
| session\_duration |  |  | Sekunden | Legt die Session-Dauer fest |
| session\_keep\_alive |  |  | Sekunden | Legt den Keep live-Zeitraum für die Session fest |
| session | backend | cookie |  | Hier werden Einstellungen für das Cookie-Handling im Backend festgelegt.<br>Dazu gehören u.a Pfadangabe zur Cookie-Speicherung, Domain und Laufzeit |
|  | frontend<br>  | cookie |  | Hier werden Einstellungen für das Cookie-Handling im Frontend festgelegt. |
| backend\_login\_policy | login\_tries\_until\_blocked |  | digit | Anzahl der Login-Versuche bis ein Account gesperrt wird (Standard: 50) |
|  | login\_tries\_until\_delay |  | digit | Anzahl der Login-Versuche ohne Verzögerung (Standard: 3) |
|  | relogin\_delay |  | digit | Verzögerung in Sekunden nach erreichen von login\_tries\_until\_delay (Standard: 5) |
|  | enable\_stay\_logged\_in |  | true/false | Aktiviert/deaktiviert die "Angemeldet bleiben" Option (Standard: true) |
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
| use\_hsts |  |  | true / false | Aktiviert HSTS (HTTP Strict Transport Security)  [⚠️ Hinweise: https/hsts-config](#https-config)|
| hsts\_max\_age |  |  | Sekunden | Legt die Laufzeit der HSTS-Einstellung fest |
| <span class="colour" style="color:var(--color-prettylights-syntax-entity-tag)">use\_gzip</span> |  |  | true / false | Aktiviert oder deaktiviert die GZIP-Kompression |
| use\_etag |  |  | true / false | Legt fest ob etag-Header ausgeliefert werden sollen |
| use\_last\_modified |  |  | true / false | Legt fest ob ein last modified header ausgeliefert werden soll |
| start\_page |  |  | addonkey | Legt die Standard-Startseite im Backend fest. ( Kann je Nutzer im Backend überschrieben werden) |
| timezone |  |  | Zeitzone | Beispiel: <span class="colour" style="color:var(--color-prettylights-syntax-string)">Europe/Berlin</span> |
| socket\_proxy |  |  | IP:Port | Legt die Einstellungen  für einen Socket proxy fest |
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

### Safe Mode konfigurieren

Der Safe Mode deaktiviert alle AddOns und ermöglicht den Zugriff auf das Backend, auch wenn AddOns Probleme verursachen. Seit REDAXO 5.16 kann der Safe Mode aus Sicherheitsgründen nur noch von Administratoren aktiviert werden.

**Aktivierung durch Administratoren:**

Eingeloggte Administratoren können den Safe Mode über die System-Seite oder per URL-Parameter aktivieren:

```
/redaxo/index.php?safemode=1
```

Bei dieser Variante ist der Safe Mode nur für die jeweilige Admin-Session aktiv.

**Globale Aktivierung über config.yml:**

Für Notfälle kann der Safe Mode auch global über die config.yml aktiviert werden:

```yaml
safe_mode: true
```

Bei dieser Konfiguration ist der Safe Mode für alle Backend-Nutzer aktiviert, unabhängig von der Session. Diese Option sollte nur in Notfällen verwendet werden, wenn sich Administratoren nicht mehr normal einloggen können.

**Verwendungszwecke:**
- Fehlerhaft Addons deaktivieren
- Backend-Zugriff bei AdDon-Problemen ermöglichen 
- Fehlerdiagnose ohne AddOn-Interferenzen
- Notfall-Zugriff für Administratoren

> **Sicherheitshinweis:** Der Safe Mode deaktiviert auch sicherheitsrelevante AddOns. Die globale Aktivierung über config.yml sollte nur temporär erfolgen.

### Datenbank SSL-Konfiguration

REDAXO unterstützt SSL/TLS-verschlüsselte Datenbankverbindungen. Die Konfiguration erfolgt in der config.yml unter dem `db`-Knoten:

```yaml
db:
    1:
        host: localhost
        login: root
        password: 'mypassword'
        name: redaxo5
        persistent: false
        ssl_key: /path/to/client-key.pem      # Optionaler Client-Private-Key
        ssl_cert: /path/to/client-cert.pem    # Optionales Client-Zertifikat
        ssl_ca: /path/to/ca-cert.pem          # CA-Zertifikat für Verifikation
        ssl_verify_server_cert: true          # Server-Zertifikat verifizieren
```

**SSL-Parameter:**

- `ssl_key`: Pfad zum Client-Private-Key (optional)
- `ssl_cert`: Pfad zum Client-Zertifikat (optional)  
- `ssl_ca`: Pfad zum CA-Zertifikat für die Verifikation
- `ssl_verify_server_cert`: Aktiviert/deaktiviert die Server-Zertifikat-Verifikation

**Konfigurationsbeispiele:**

```yaml
# Einfache SSL-Verbindung ohne Client-Zertifikat
db:
    1:
        host: mysql.example.com
        ssl_verify_server_cert: true

# SSL mit Client-Zertifikat-Authentifizierung
db:
    1:
        host: secure-mysql.example.com
        ssl_key: /var/ssl/client-key.pem
        ssl_cert: /var/ssl/client-cert.pem
        ssl_ca: /var/ssl/ca-cert.pem
        ssl_verify_server_cert: true

# SSL ohne Server-Verifikation (nicht empfohlen für Produktion)
db:
    1:
        host: mysql.internal.network
        ssl_verify_server_cert: false
```

> **Sicherheitshinweis:** In Produktionsumgebungen sollte `ssl_verify_server_cert` immer auf `true` gesetzt sein, um Man-in-the-Middle-Angriffe zu verhindern.

### Backend Login-Richtlinien

Das Backend Login-System bietet verschiedene Sicherheitseinstellungen zum Schutz vor Brute-Force-Angriffen. Die Konfiguration erfolgt über `backend_login_policy` in der config.yml:

```yaml
backend_login_policy:
    login_tries_until_blocked: 50    # Anzahl Versuche bis zur Sperrung
    login_tries_until_delay: 3       # Anzahl Versuche ohne Verzögerung  
    relogin_delay: 5                 # Verzögerung in Sekunden
    enable_stay_logged_in: true      # "Angemeldet bleiben" Option
```

**Funktionsweise:**

1. **Erste Versuche ohne Verzögerung**: Bis zu `login_tries_until_delay` Versuche können ohne Verzögerung durchgeführt werden (Standard: 3)

2. **Verzögerte Versuche**: Nach `login_tries_until_delay` Versuchen wird bei jedem weiteren Versuch eine Verzögerung von `relogin_delay` Sekunden eingeführt

3. **Account-Sperrung**: Nach `login_tries_until_blocked` Versuchen wird der Account komplett gesperrt und kann nur von einem Administrator entsperrt werden

**Beispiel-Szenario:**
```yaml
login_tries_until_delay: 3
relogin_delay: 5  
login_tries_until_blocked: 10
```

- Versuche 1-3: Sofortige Login-Versuche möglich
- Versuche 4-10: 5 Sekunden Wartezeit zwischen den Versuchen
- Ab Versuch 11: Account gesperrt

**Konfigurationsoptionen:**

```yaml
# Strenge Sicherheit (für kritische Systeme)
backend_login_policy:
    login_tries_until_blocked: 5
    login_tries_until_delay: 2
    relogin_delay: 30
    enable_stay_logged_in: false

# Moderate Sicherheit (Standard-Empfehlung)
backend_login_policy:
    login_tries_until_blocked: 20
    login_tries_until_delay: 3
    relogin_delay: 5
    enable_stay_logged_in: true

# Entwicklungsumgebung (weniger restriktiv)
backend_login_policy:
    login_tries_until_blocked: 100
    login_tries_until_delay: 10
    relogin_delay: 1
    enable_stay_logged_in: true
```

> **Sicherheitshinweis:** In Produktionsumgebungen sollten restriktive Werte gewählt werden. Die "Angemeldet bleiben" Funktion sollte bei höchsten Sicherheitsanforderungen deaktiviert werden.

<a name="https-config"></a>

### HTTPS und HSTS-Konfiguration

```yaml
use_https: true
use_hsts: true
hsts_max_age: 31536000    # 1 Jahr
```

⚠️ HSTS-Warnhinweise:
- Aktivierung NUR mit validem SSL-Zertifikat
- HSTS-Einstellungen werden vom Browser gecached
- Stufenweiser Rollout empfohlen:
  1. HTTPS testen
  2. HSTS mit kurzem max_age testen
  3. max_age schrittweise erhöhen

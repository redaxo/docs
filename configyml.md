# config.yml

* [Einleitung](#plugin)
* [Speicherort](#speicherort)

<a name="einleitung"></a>

## Einleitung

In der config.yml werden die für den Betrieb des Projektes erforderlichen Einstellungen hinterlegt. Hierzu gehören die bei der Installation gemachten Angaben und weitere allgemeine Einstellungen, die individuell angepasst werden können. Nicht alle Einstellungen sind über das Backend von REDAXO erreichbar. Diese müssen bei Bedarf direkt in der Datei gepflegt werden. 

<a name="speicherort"></a>

## Speicherort

Der Speicherort ist `redaxo/data/core/config.yml`

> Die config.yml wird bei einem Update nicht überschrieben und ist daher updatesicher.


##  Beispiel config.yml

```yml
setup: false
debug:
    enabled: false
    throw_always_exception: false
instname: rex20201222171044
server: 'https://domain.tld/'
servername: 'REDAXO Website'
error_email: skerbis@klxm.de
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

```

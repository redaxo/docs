# System

- [Einstellungen (und Features)](#settings)
- [Sprachen](#lang)
- [Logdateien](#log)
- [Systembericht](#bericht)
- [Customizer](#custom)
- [Historie](#historie)

<a name="settings"></a>
## Einstellungen

Im Tab Einstellungen werden die grundlegenden Daten zur Konfiguration des Systems und für die Website erfasst. 

- Url der Website
- Name der Website 
- Backendsprache
- E-Mail-Adresse bei Fehlern
- E-Mail-Benachrichtigung bei Fehlern (wenn PHPMailer Addon aktiviert) 
- Startartikel
- Fehlerartikel
- Standardtemplate
- Editor-Integration

Die Einstellungen werden ggf. von installierten AddOns erweitetert und bieten dann weitere Optionen. 

Im Panel **Features** stehen folgende Funktionen zur Verfügung:

### Cache Löschen

Templates und Sprachdateien werden erstellt, Artikelcache wird gelöscht. Sobald ein Artikel im Frontend aufgerufen wird, wird der Cache des/der entsprechenden Artikels/Kategorie wieder erstellt. *Sollte nur gestartet werden, wenn ein Problem vorliegt*

### Debug-Modus aktivieren

Mit dem Debug-Modus werden bei PHP-Skriptfehlern im Frontend und Backend zusätzliche Angaben zum Fehler ausgegeben. Ausserdem werden keine immutable cache-http-header verwendet. Der Debug-Modus sollte im Live-Betrieb nicht aktiviert werden, da die Fehlermeldungen auch sensible Daten beinhalten können, darüber hinaus wird die Webpräsenz auf noindex gesetzt.  

### Safe mode aktivieren

Im Safe mode werden vorübergehend alle AddOns deaktiviert. Falls bspw. ein AddOn nach der Installation Probleme macht, kann dieses über den Safe mode deaktiviert oder deinstalliert werden.

### Setup

Hier kann das Setup erneut gestartet werden. Es kann dafür verwendet werden eine defekte Installation im **Notfall** zu reparieren, das Passwort des Admins zurückzusetzen oder nötige Konvertierungsaufgaben nach einem größeren Update durchzuführen (z.B. [Aktualisierung der Datenbank auf utf8mb4](/{{path}}/{{version}}/aktualisierung#utf8mb4))  

<a name="lang"></a>
## Sprachen

REDAXO unterstützt mehrere Sprachen. Im Reiter Sprachen können diese angelegt und verwaltet werden. Weitere Informationen zum Thema im Kapitel: [Mehrsprachigkeit](/{{path}}/{{version}}/mehrsprachigkeit). 

<a name="log"></a>
## Logdateien

Hier werden zentral die Log-Dateien des Systems und einiger AddOns zur Protokollierung und Fehleranalyse abgelegt. 


<a name="bericht"></a>
## Systembericht

Der Systembericht informiert über die aktuelle Serverumgebung und installierte AddOns mit Angabe der Versionsnummer. Er kann als Markdown-Code heruntergeladen werden und so für den Support in GitHub und Slack anderen Nutzern bereitgestellt werden. Die Daten selbst sind soweit bereinigt, dass sie keine Informationen über die Server IP und Datenbanknamen verraten. 


<a name="custom"></a>
## Customizer (sofern installiert) 

Der Customizer stellt Optionen zur Individualisierung des Backends zur Verfügung. Darüber hinaus stellt er für Entwickler CodeMirror zur konfortablesn Darstellung von Code zur Verfügung. 

<a name="historie"></a>
## Historie (sofern installiert)

Ist das History-Plugin der Struktur installier, kann die Historie hier gelöscht werden. 




<details>
<summary>System report (REDAXO 5.9.0, PHP 7.3.14)</summary>

| REDAXO        |            |
| ------------: | :--------- |
|       Version | 5.9.0      |


| PHP           |            |
| ------------: | :--------- |
|       Version | 7.3.14     |
|       OPcache | yes        |
|        Xdebug | no         |


| Database      |                 |
| ------------: | :-------------- |
|       Version | MariaDB 10.1.44 |
| Character set | utf8            |


| Server        |            |
| ------------: | :--------- |
|            OS | Linux      |
|          SAPI | fpm-fcgi   |
|     Webserver | Apache     |


| Request       |               |
| ------------: | :------------ |
|       Browser | Safari/13.0.5 |
|      Protocol | HTTP/1.0      |
|         HTTPS | yes           |


| Packages                   |             |
| -------------------------: | :---------- |
|                    adminer | 1.8.1       |
|                     backup | 2.5.1       |
|                be_password | 1.1.0       |
|                   be_style | 2.9.0       |
|        be_style/customizer | 2.9.0       |
|            be_style/redaxo | 2.9.0       |
|                   be_tools | 1.5         |
|                    bloecks | 2.1.1       |
|           bloecks/cutncopy | 2.1.1       |
|          bloecks/dragndrop | 2.1.1       |
|             bloecks/status | 2.1.1       |
|                 cheatsheet | 0.0.1       |
|                       cke5 | 3.7.1       |
|                    cronjob | 2.6.0       |
|    cronjob/optimize_tables | 2.6.0       |
|                    cropper | 1.1.0       |
|                 focuspoint | 2.2.0       |
|            global_settings | 2.4.1       |
|                   icecoder | 2.0.1       |
|                 iconpicker | 1.1.0       |
|                    install | 2.6.0       |
|                       iwcc | 1.0.8       |
|                  klxm_info | 0.0.1       |
|                   markitup | 3.3.4       |
|                     matomo | 1.2.1       |
|                     mblock | 3.1.0       |
|              media_manager | 2.8.0       |
|         media_manager_plus | 2.0.0       |
|                  mediapool | 2.7.0       |
|                   metainfo | 2.6.0       |
|                      mform | 5.3.1       |
|                 mform/docs | 1.0         |
|                    minibar | 2.0.1       |
|                     minify | 2.1.0       |
|              modulsammlung | 4.13.4      |
|           navigation_array | 1.0.2       |
|                 pdf_viewer | 2.0.0       |
|                     pdfout | 1.6.0       |
|                  phpmailer | 2.7.0       |
|                       plyr | 3.1.2       |
|                    project | dev         |
|           quick_navigation | 3.7.1       |
|                  search_it | 6.6.6       |
|     search_it/autocomplete | 6.6.6       |
|    search_it/documentation | 6.6.6       |
|            search_it/stats | 6.6.6       |
|                 seocheckup | 1.3.4       |
|                simplestats | 1.0.0       |
|                       sked | 1.10.0      |
|                  structure | 2.9.0       |
|          structure/content | 2.9.0       |
|          structure/history | 2.9.0       |
|           structure_tweaks | 1.1.1       |
|                   ui_tools | 1.0.0       |
| ui_tools/jquery-minicolors | 2.2.7       |
|           uikit_collection | 2.0.0       |
|                   uploader | 2.0.5       |
|                        url | 1.0.1       |
|                usage_check | 2.2.1       |
|                      users | 2.6.0       |
|                      video | 2.0.0-beta4 |
|                     watson | 2.1.0       |
|                       ycom | 3.0-beta4   |
|                  ycom/auth | 3.0-beta4   |
|                  ycom/docs | 3.0-beta4   |
|                 ycom/group | 3.0-beta4   |
|                      yform | 3.3.1       |
|                 yform/docs | 3.3.1       |
|                yform/email | 3.3.1       |
|              yform/manager | 3.3.1       |
|                yform/tools | 3.3.1       |
|              yform_geo_osm | 1.1.2       |
|            yform_usability | 1.4         |
|                   yrewrite | 2.6         |
|                zip_install | 1.1         |

</details>

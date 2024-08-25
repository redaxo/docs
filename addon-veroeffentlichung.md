# AddOn Veröffentlichung

* [Erstellung des AddOn-Keys](#anker-addon-key)
* [Mein API-Key](#anker-api-key)
* [Das Installer-AddOn](#anker-installer)
* [Veröffentlichen einer Version](#anker-addon-version)
  + [Settings](#anker-addon-version-settings)
  + [Meine Packages](#anker-addon-version-meinepackages)
  + [Eigenes AddOn](#anker-addon-version-eigenesaddon)
  + [AddOn-Version aktualisieren / löschen](#anker-addon-version-aktualisieren)
  + [AddOn-Version erstellen](#anker-addon-version-erstellen)
  + [Ausschließen von Development-Dateien im Package](#exclude)
  + [AddOn direkt aus GitHub heraus veröffentlichen](#installeraction)
* [Updates](#updates)
  + [Updates testen, geheime AddOns](#testing)
* [Meldungen nach erfolgreicher Installation ausgeben](#statusmsg)
* [Meldung bei fehlerhafter Installation ausgeben](#error_install)

Um eigene AddOns zu veröffentlichen, sollten man folgenden Weg nehmen.

<a name="anker-addon-key"></a>

## Erstellung des AddOn-Keys

Jedes AddOn hat eine eindeutige Kennung. Diese Kennung nennen wir Key und ist gleichzeitig auch der Ordnername. Um einen passenden Key zu registrieren und auch die Bezeichnung und Beschreibung des AddOns festzulegen, muss man sich zunächst in MyREDAXO [registrieren](/registrierung/) und dann [einloggen](/myredaxo/login/). Unter *Meine AddOns* kann dann die AddOn-Definition mit dem passenden Key angelegt werden.

<a name="anker-api-key"></a>

## Mein API-Key

Um verschiedene weitere Aktionen durchführen zu können, die man nun auf der eigenen REDAXO-Installation machen muss, braucht man einen API-Key. Diesen kann man sich in MyREDAXO erstellen. Dieser besteht aus einer Zeichenkette und sollte nicht weitergegeben werden, da man mit dem Key und dem eigenen Login Versionen veröffentlichen, löschen oder ändern kann.

<a name="anker-installer"></a>

## Das Installer-AddOn

Jede aktuelle REDAXO-Version hat einen Installer. Darüber werden AddOns installiert und aktualisiert, aber auch eigene AddOns  erstellt, bearbeitet und veröffentlicht.

<a name="anker-addon-version"></a>

## Veröffentlichen einer Version

<a name="anker-addon-version-settings"></a>

### Settings

Einzelne Versionen müssen entwickelt und geprüft werden. Das macht man meistens lokal auf dem eigenen Rechner. Hier muss das AddOn, welches man veröffentlichen will, existieren. Zunächst muss aber der API-Key in den Installer Einstellungen eingetragen werden. Nur dadurch kann erkannt werden, zu welchen AddOns man Zugriff hat.

![Settings](/assets/v5.3.0-installer-settings.png)

Einstellungsdialog

<a name="anker-addon-version-meinepackages"></a>

### Meine Packages

Jetzt kann man über **Core & Packages/Eigene hochladen** einsehen, welche AddOns bereits registriert sind und auch in der lokalen Installation vorhanden sind.
Das heißt, wenn man Änderungen durchführen und eine neue Version eines AddOns veröffentlichen möchte, muss genau dieses AddOn in der lokalen Installation zur Verfügung stehen.

![Meine Packages](/assets/v5.3.0-installer-meinepackages.png)

Eigene hochladen - Meine Packages

<a name="anker-addon-version-eigenesaddon"></a>

### Eigenes AddOn

Um ein AddOn zu veröffentlichen oder eine neue Version aufzuspielen, wählt man das gewünschte AddOn in der Liste aus.
In dieser Liste können einzelne Versionen mit "Datei aktualisieren" aktualisiert werden oder über das "+" eine neue Version erstellt werden.

![Eigenes AddOn](/assets/v5.3.0-installer-eigenesaddon.png)

Eigenes AddOn

<a name="anker-addon-version-aktualisieren"></a>

### AddOn-Version aktualisieren / löschen

Eine Aktualisierung wird mit den vorhandenen Versionsinformationen abgeglichen. D.h. wenn lokal eine spezielle Version läuft, dann kann man in den anderen Versionen nur die Beschreibung und den Status ändern. Sofern die ausgewählte Version mit der lokalen übereinstimmt oder man auf "ZIP-Datei erstellen und hochladen" klickt, kann man die eigene lokale Version komplett hochladen und ersetzen.

Eine einzelne Version kann man über den Löschen-Button aus dem Online-Archiv entfernen.

![AddOn aktualisieren](/assets/v5.3.0-installer-addon-aktualisieren.png)

AddOn aktualisieren

<a name="anker-addon-version-erstellen"></a>

### AddOn-Version erstellen

Versionen werden direkt aus dem lokalen AddOn selbst herangezogen (package.yml). Diese Version ist entsprechend voreingestellt und die Beschreibung und der Status können gesetzt werden. Sofern diese Version online gestellt wird, ist sie sofort für andere REDAXO-User verfügbar. Mit "Assets aus dem Root-Assets-Ordner nehmen" können Assets aus dem REDAXO-Assets-Ordner übernommen werden.

![AddOn erstellen](/assets/v5.3.0-installer-addon-version-erstellen.png)

AddOn erstellen


<a name="exclude"></a>

## Ausschließen von Development-Dateien im Package

Während der Entwicklung werden häufig Dateien benötigt, die im eigentlchen AddOn nicht erforderlich sind. Diese Dateien und Ordner kann man in der `package.yml` auf ignorieren setzen. Sie werden somit bei der AddOn-Veröffentlichung nicht mehr beachtet.   

```php 
installer_ignore:
    - node_modules
    - .env
    - src
```
  
<a name="installeraction"></a>

## AddOn direkt aus GitHub heraus veröffentlichen

Mit der [FriendsOfREDAXO/installer-action](https://github.com/FriendsOfREDAXO/installer-action) können AddOns direkt aus GitHub heraus releast werden. 
Nach Einrichtung der `installer-action` werden GitHub-Releases automatisch in den Installer übertragen. 
  
**Voraussetzung:** Das AddOn muss vorab in MyREDAXO angelegt und beschrieben sein. 

[Informationen zur Einrichtung auf GitHub](https://github.com/FriendsOfREDAXO/installer-action). 
   
  
<a name="updates"></a>

## Updates
Sind Aktualisierungen an Datenbanken und Konfigurationen erforderlich sollte dem AddOn eine `update.php` beigelegt sein. Diese wird automatisch beim Update eines AddOns ausgeführt. 

Häufig reicht es, hier die `install.php`einzubinden, da dort bereits die allgemeinen Config-Properties und die Konfiguration der Datenbank mittels `rex_sql_table` sichergestellt werden.

Weitergehende Anpassungen führt man dann nach dem include der install.php aus. 

***Beispiel***

```php 
$addon = rex_addon::get('mein_addon');
$addon->includeFile(__DIR__ . '/install.php');
```


<a name="testing"></a>

### Updates testen, geheime AddOns

Mit hinterlegtem API-Key kann man über den Installer eigene, offline gestellte, AddOns/Versionen laden. Diese AddOn-Versionen sind nicht öffentlich. Auf diese Weise können Updates in Ruhe über den Installer getestet werden oder der Installer ggf. für private AddOn-Installationen genutzt werden.

> Zu bedenken dabei ist, dass der API-Key auch Schreibrechte hat. Also **alle Administratoren** der REDAXO-Installation hätten damit Zugriff auf die eigenen AddOns. Sie könnten diese verändern, **zerstören** und auch **löschen**. Daher sollte der Key unbedingt wieder entfernt werden.
> 

<a name="statusmsg"></a>

## Meldung nach erfolgreicher Installation ausgeben

Es ist möglich, im Installer eine Information direkt nach erfolgter Installation auszugeben, um z.B. auf die nächsten Schritte hinzuweisen. 

```php
$addon = rex_addon::get('mein_addon');
$addon->setProperty('successmsg', rex_i18n::msg('mein_addon_install_msg');
```

<a name="error_install"></a>

## Meldung bei fehlerhafter Installation ausgeben

Sollte was während der Installation schieflaufen, kann man die Installation als nicht erfolgreich markieren und eine Fehlermeldung ausgeben. 

```php 
if ($something_bad_happened) {
    $addon->setProperty('installmsg', 'Installation fehlgeschlagen');
    $addon->setProperty('install', false);
}
```

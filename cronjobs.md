# Cronjobs

- [Zweck des Cronjob-AddOns](#zweck)
- [Einstellungen eines Cronjobs](#einstellungen)
  - [Name](#name)
  - [Beschreibung](#beschreibung)
  - [Umgebung](#umgebung)
  - [Ausführung](#ausfuehrung)
  - [Status](#status)
  - [Typ](#typ)
  - [Intervall](#intervall)
- [Neue Typen durch AddOns definieren](#neue-typen)
- [Klassen-Referenz](#klassen-referenz)

<a name="zweck"></a>

## Zweck des Cronjob-AddOns

Cronjobs dienen der regelmäßigen automatisierten Ausführung von Programmcode. Das Cronjobs-AddOn ist Bestandteil der REDAXO-Basisinstallation, muss jedoch bei Bedarf separat installiert werden.

Beispiele für die Verwendung:

* Regelmäßige Datenbank-Tabellenoptimierung
* Zeitgesteuertes Veröffentlichen von Artikeln
* routinemäßige Aufgaben wie Datenbank-Backups

Im Add-on lassen sich dann beliebig viele Einträge erstellen, die gemäß den Einstellungen jedes Eintrages abgearbeitet werden.

<a name="einstellungen"></a>

## Einstellungen eines Cronjobs

<a name="name"></a>

### Name

Zunächst gibt man den Namen eines Eintrags ein. Dies kann beispielsweise `RSS Feed lesen` oder `Monatliches Backup` sein.

<a name="beschreibung"></a>

### Beschreibung

Eine aussagekräftige Beschreibung vervollständigt den informativen Teil des Eintrages.

<a name="umgebung"></a>

### Umgebung

Im Feld `Umgebung` kann man ein oder mehrere Ereignisse wählen, bei denen der Cronjob ausgeführt wird.

- Frontend
- Backend
- Skript (empfohlen, benöitgt Server-Cron)

Sobald ein eingestelltes Intervall erreicht ist, wartet das AddOn auf das eingestellte Ereignis: einen Seitenaufruf im Frontend, auf eine Aktion durch einen Nutzer im Backend oder den Aufruf der Skriptumgebung. Tritt das eingestellte Ereignis ein, wird der Cronjob ausgeführt.

Obwohl alle drei Einträge gleichzeitig aktiviert werden können, sollte man die Umgebung `Skript` nicht gleichzeitig mit `Frontend` oder `Backend` auswählen - von Testzwecken einmal abgesehen.

Somit können Cronjobs ausgelöst werden durch:

- Einen Seitenaufruf im Frontend
- Einen Seitenaufruf im Backend
- Einen direkten Aufruf der Cronjob-Skriptumgebung durch den Server

Bei der Ausführung in der Umgebung `Frontend` und `Backend` läuft der Cronjob in der Session des jeweiligen Users, sodass dort auch ein Zugriff auf die Session möglich ist. Nur die Umgebung `Skript` erlaubt die Ausführung des Cronjobs unabhängig von einem Aufruf von REDAXO im Frontend oder im Backend. Der Aufruf des Skripts erfolgt durch `.../redaxo/bin/console cronjob:run`, also z.B. `/home/users/12345/www/redaxo/bin/console cronjob:run`

Nur in der Umgebung `Backend` ist es möglich, den Cronjob manuell in den Einstellungen des AddOns zu starten.

#### Empfehlungen 

Die empfohlene Umgebung ist `Skript`, hierbei wird der Cronjob über einen serverseitigen Cronjob aufgerufen. 

Sollte die Ausführung als Cronjob nicht möglich sein (z.B.: aufgrund mangelnder Rechte auf dem Server), stehen die alternativen Umgebungen `Frontend` und `Backend` zur Verfügung. 

Bei `Skript` findet die Ausführung über den Cronjob des Betriebssystems statt (z.B. `crontab -e`) und ist unabhängig von den Seitenaufrufen in REDAXO. Zum Aufruf muss `redaxo/bin/console cronjob:run` aufgerufen werden. Das Intervall zwischen den Server-Cronjobs muss kleiner oder gleich sein, als das kleinste Intervall im REDAXO-Cronjob.

**Wir empfehlen, den Aufruf serverseitig in möglichst kurzem Intervallen durchzuführen, das Cronjob-Addon regelt dann die tatsächliche Ausführung.**

`Frontend` und `Backend` werden ausgeführt, wenn im Frontend und / oder Backend Seitenaufrufe erfolgen. Dies hat u.U. zur Folge, dass die Cronjobs ggf. später ausgeführt werden, als erwünscht. (z.B. bei regelmäßigen Backups, E-Mail-Benachrichtigungen)  


<a name="ausfuehrung"></a>

### Ausführung

Wenn eines der Ereignisse `Frontend` oder `Backend` eintritt, so kann der Cronjob seinen Dienst zu Beginn des Aufrufs erledigen oder am Ende. Nur in Ausnahmefällen sollte die Einstellung `Beginn` gewählt werden, da sie den jeweiligen Aufruf verzögert. Das fällt natürlich weniger ins Gewicht, wenn die Ausführung am Ende geschieht.

<a name="status"></a>

### Status

Im Feld `Status` kann ein Cronjob deaktiviert werden. Standard ist `aktiviert`.

<a name="typ"></a>

### Typ

Im Feld `Typ` bestehen die Auswahlmöglichkeiten:

- PHP-Code
- PHP-Callback
- URL-Aufruf

AddOns können dort weitere Einträge hinzufügen.

Beispielsweise:

- Datenbankexport (durch das AddOn `Backup`)
- Search it: Reindexieren (durch das AddOn `Search it`)

Je nach Einstellung im Feld `Typ` stehen unterschiedliche Eingabemöglichkeiten im Bereich `Typspezifische Parameter` zur Verfügung.
So kann bei der Einstellung `PHP-Code` kompletter PHP-Code eingegeben werden, bei der Einstellung `PHP-Callback` lediglich ein Aufruf.

AddOns können eigene, typspezifische Parameter zur Verfügung stellen.

<a name="intervall"></a>

### Intervall

Die Standardeinstellung für den Bereich `Intervall` ist die tägliche Ausführung, jeweils beim nächsten Aufruf der Umgebung nach 0:00 Uhr.

<a name="neue-typen"></a>

## Neue Typen durch AddOns definieren

AddOns können eigene Ausführungstypen definieren. Dies wird beispielsweise im System AddOn `Backup` verwendet, um automatisierte Backups auszuführen.

### Grundlagen

Um einen eigenen Cronjob-Typ zu erstellen, muss eine PHP-Klasse erstellt werden, die von der abstrakten Basisklasse `rex_cronjob` erbt. Diese Klasse definiert die Funktionalität des Cronjobs und stellt die Konfigurationsfelder für das Backend zur Verfügung.

### Schritt-für-Schritt-Anleitung

#### 1. Cronjob-Klasse erstellen

Erstelle eine neue PHP-Datei in deinem AddOn unter `/lib/` oder `/lib/cronjob/`. Die Klasse muss von `rex_cronjob` erben:

```php
<?php

class rex_cronjob_mein_typ extends rex_cronjob
{
    public function execute()
    {
        // Hier wird die Hauptfunktionalität implementiert
        // Rückgabe: true bei Erfolg, false bei Fehler
        
        try {
            // Deine Cronjob-Logik hier
            $this->setMessage('Cronjob erfolgreich ausgeführt');
            return true;
        } catch (Exception $e) {
            $this->setMessage('Fehler: ' . $e->getMessage());
            return false;
        }
    }

    public function getTypeName()
    {
        // Name des Cronjob-Typs im Backend
        return 'Mein Cronjob-Typ';
    }

    public function getParamFields()
    {
        // Konfigurationsfelder für das Backend
        return [
            [
                'label' => 'Beispiel-Parameter',
                'name' => 'beispiel_param',
                'type' => 'text',
                'notice' => 'Hier eine Beschreibung des Parameters eingeben'
            ]
        ];
    }
}
```

#### 2. Cronjob-Typ registrieren

Die Registrierung erfolgt über die `boot.php` deines AddOns:

```php
<?php
// boot.php des AddOns

rex_cronjob_manager::registerType('rex_cronjob_mein_typ');
```

#### 3. Praktisches Beispiel: Abonnenten-Benachrichtigung

Hier ist ein vollständiges Beispiel für einen Cronjob, der über neue Abonnenten in einer Tabelle informiert:

```php
<?php

class rex_cronjob_subscriber_notification extends rex_cronjob
{
    public function execute()
    {
        $success = true;
        $messages = [];
        
        // Parameter abrufen
        $email = $this->getParam('notification_email');
        $table = $this->getParam('subscriber_table', 'rex_newsletter_user');
        $last_check = $this->getParam('last_check_timestamp', 0);
        
        if (empty($email)) {
            $this->setMessage('Keine E-Mail-Adresse für Benachrichtigung konfiguriert');
            return false;
        }
        
        try {
            // Neue Abonnenten seit letzter Prüfung finden
            $current_time = time();
            $sql = rex_sql::factory();
            
            $query = "
                SELECT id, email, createdate, firstname, lastname 
                FROM {$table} 
                WHERE createdate > :last_check 
                AND status = 1 
                ORDER BY createdate DESC
            ";
            
            $sql->setQuery($query, ['last_check' => date('Y-m-d H:i:s', $last_check)]);
            $new_subscribers = $sql->getArray();
            
            if (count($new_subscribers) > 0) {
                // E-Mail-Benachrichtigung vorbereiten
                $subject = 'Neue Newsletter-Abonnenten: ' . count($new_subscribers);
                $message_body = "Es wurden " . count($new_subscribers) . " neue Abonnenten gefunden:\n\n";
                
                foreach ($new_subscribers as $subscriber) {
                    $name = trim(($subscriber['firstname'] ?? '') . ' ' . ($subscriber['lastname'] ?? ''));
                    $message_body .= "- " . $subscriber['email'];
                    if ($name) {
                        $message_body .= " (" . $name . ")";
                    }
                    $message_body .= " - " . rex_formatter::date($subscriber['createdate'], 'datetime') . "\n";
                }
                
                // E-Mail versenden (PHPMailer-AddOn verwenden)
                if (rex_addon::get('phpmailer')->isAvailable()) {
                    $mail = new rex_mailer();
                    $mail->addAddress($email);
                    $mail->Subject = $subject;
                    $mail->Body = $message_body;
                    
                    if ($mail->send()) {
                        $messages[] = "Benachrichtigung an {$email} gesendet: " . count($new_subscribers) . " neue Abonnenten";
                    } else {
                        $success = false;
                        $messages[] = "Fehler beim E-Mail-Versand: " . $mail->ErrorInfo;
                    }
                } else {
                    $success = false;
                    $messages[] = "PHPMailer-AddOn ist nicht verfügbar";
                }
            } else {
                $messages[] = "Keine neuen Abonnenten gefunden";
            }
            
            // Zeitstempel für nächste Prüfung aktualisieren
            $this->setParam('last_check_timestamp', $current_time);
            
            // Status-Nachricht setzen
            $this->setMessage(implode("\n", $messages));
            
        } catch (Exception $e) {
            $this->setMessage('Fehler bei der Abonnenten-Prüfung: ' . $e->getMessage());
            return false;
        }
        
        return $success;
    }
    
    public function getTypeName()
    {
        return rex_i18n::msg('cronjob_subscriber_notification');
    }
    
    public function getParamFields()
    {
        return [
            [
                'label' => rex_i18n::msg('cronjob_subscriber_notification_email'),
                'name' => 'notification_email',
                'type' => 'text',
                'notice' => rex_i18n::msg('cronjob_subscriber_notification_email_notice'),
                'attributes' => ['type' => 'email']
            ],
            [
                'label' => rex_i18n::msg('cronjob_subscriber_table'),
                'name' => 'subscriber_table',
                'type' => 'text',
                'default' => 'rex_newsletter_user',
                'notice' => rex_i18n::msg('cronjob_subscriber_table_notice')
            ],
            [
                'label' => rex_i18n::msg('cronjob_subscriber_last_check'),
                'name' => 'last_check_timestamp',
                'type' => 'hidden',
                'default' => 0
            ]
        ];
    }
    
    public function getEnvironments()
    {
        // Nur in Skript-Umgebung ausführen für beste Performance
        return ['script'];
    }
}
```

#### 4. Sprachdateien ergänzen

Für mehrsprachige Unterstützung sollten entsprechende Sprachdateien erstellt werden (`lang/de_de.lang`):

```
cronjob_subscriber_notification = Abonnenten-Benachrichtigung
cronjob_subscriber_notification_email = E-Mail-Adresse für Benachrichtigungen
cronjob_subscriber_notification_email_notice = E-Mail-Adresse, an die Benachrichtigungen über neue Abonnenten gesendet werden
cronjob_subscriber_table = Abonnenten-Tabelle
cronjob_subscriber_table_notice = Name der Datenbanktabelle mit den Abonnenten (Standard: rex_newsletter_user)
cronjob_subscriber_last_check = Letzter Prüfzeitpunkt
```

### Verfügbare Parameterfeld-Typen

Die `getParamFields()` Methode kann verschiedene Eingabefeld-Typen zurückgeben:

#### Text-Eingabefeld
```php
[
    'label' => 'Textfeld',
    'name' => 'text_param',
    'type' => 'text',
    'notice' => 'Hilfstext für das Feld',
    'default' => 'Standardwert',
    'attributes' => ['placeholder' => 'Platzhalter-Text']
]
```

#### Textarea
```php
[
    'label' => 'Mehrzeiliger Text',
    'name' => 'textarea_param',
    'type' => 'textarea',
    'attributes' => ['rows' => 5, 'cols' => 50]
]
```

#### Auswahlfeld (Select)
```php
[
    'label' => 'Auswahl',
    'name' => 'select_param',
    'type' => 'select',
    'options' => [
        'option1' => 'Erste Option',
        'option2' => 'Zweite Option',
        'option3' => 'Dritte Option'
    ],
    'default' => 'option1'
]
```

#### Checkbox
```php
[
    'label' => 'Aktiviert',
    'name' => 'checkbox_param',
    'type' => 'select',
    'options' => ['0' => 'Nein', '1' => 'Ja'],
    'default' => '1'
]
```

#### Verstecktes Feld
```php
[
    'name' => 'hidden_param',
    'type' => 'hidden',
    'default' => 'wert'
]
```

### Registrierung in project-addOn

Für projektspezifische Cronjobs kann die Registrierung auch im `project`-AddOn erfolgen:

1. Datei anlegen: `/redaxo/src/addons/project/lib/cronjob_mein_typ.php`
2. In `/redaxo/src/addons/project/boot.php` registrieren:

```php
<?php
if (rex_addon::get('cronjob')->isAvailable()) {
    rex_cronjob_manager::registerType('rex_cronjob_mein_typ');
}
```

### Erweiterte Funktionen

#### Umgebungen einschränken
```php
public function getEnvironments()
{
    // Nur in bestimmten Umgebungen verfügbar
    return ['script']; // oder ['frontend', 'backend']
}
```

#### Parameter zur Laufzeit aktualisieren
```php
public function execute()
{
    // Parameter können während der Ausführung geändert werden
    $counter = (int) $this->getParam('execution_counter', 0);
    $this->setParam('execution_counter', $counter + 1);
    
    return true;
}
```

### Debugging und Logging

Für die Entwicklung und Fehlersuche können Nachrichten gesetzt werden:

```php
public function execute()
{
    $debug_info = [];
    
    try {
        // Arbeit durchführen
        $debug_info[] = 'Schritt 1 abgeschlossen';
        
        // Bei Erfolg
        $this->setMessage('Cronjob erfolgreich: ' . implode(', ', $debug_info));
        return true;
        
    } catch (Exception $e) {
        $this->setMessage('Fehler in Schritt ' . count($debug_info) . ': ' . $e->getMessage());
        return false;
    }
}
```

<a name="klassen-referenz"></a>

## Klassen-Referenz

### rex_cronjob (Basisklasse)

Die abstrakte Basisklasse `rex_cronjob` stellt die Grundfunktionalität für alle Cronjob-Typen bereit.

#### Erforderliche Methoden

##### execute()
```php
abstract public function execute(): bool
```
**Beschreibung:** Führt die Hauptfunktionalität des Cronjobs aus.
**Rückgabe:** `true` bei erfolgreicher Ausführung, `false` bei Fehlern.
**Beispiel:**
```php
public function execute()
{
    try {
        // Cronjob-Logik hier
        $this->setMessage('Erfolgreich ausgeführt');
        return true;
    } catch (Exception $e) {
        $this->setMessage('Fehler: ' . $e->getMessage());
        return false;
    }
}
```

#### Optionale Methoden

##### getTypeName()
```php
public function getTypeName(): string
```
**Beschreibung:** Liefert den angezeigten Namen des Cronjob-Typs im Backend.
**Standard:** Gibt den Klassennamen zurück.
**Beispiel:**
```php
public function getTypeName()
{
    return rex_i18n::msg('mein_cronjob_typ_name');
}
```

##### getParamFields()
```php
public function getParamFields(): array
```
**Beschreibung:** Definiert die Konfigurationsfelder für das Backend.
**Rückgabe:** Array mit Feld-Definitionen.
**Beispiel:**
```php
public function getParamFields()
{
    return [
        [
            'label' => 'E-Mail-Adresse',
            'name' => 'email',
            'type' => 'text',
            'attributes' => ['type' => 'email'],
            'notice' => 'Ziel-E-Mail-Adresse'
        ]
    ];
}
```

##### getEnvironments()
```php
public function getEnvironments(): array
```
**Beschreibung:** Definiert die Umgebungen, in denen der Cronjob verfügbar ist.
**Standard:** `['frontend', 'backend', 'script']`
**Beispiel:**
```php
public function getEnvironments()
{
    return ['script']; // Nur in Skript-Umgebung
}
```

#### Parameter-Verwaltung

##### setParam()
```php
public function setParam(string $key, mixed $value): void
```
**Beschreibung:** Setzt einen Parameter-Wert.

##### getParam()
```php
public function getParam(string $key, mixed $default = null): mixed
```
**Beschreibung:** Ruft einen Parameter-Wert ab.

##### setParams()
```php
public function setParams(array $params): void
```
**Beschreibung:** Setzt alle Parameter auf einmal.

##### getParams()
```php
public function getParams(): array
```
**Beschreibung:** Ruft alle Parameter ab.

#### Nachrichten-Verwaltung

##### setMessage()
```php
public function setMessage(string $message): void
```
**Beschreibung:** Setzt eine Status-Nachricht für die Anzeige im Backend.

##### getMessage()
```php
public function getMessage(): string
```
**Beschreibung:** Ruft die aktuelle Status-Nachricht ab.

##### hasMessage()
```php
public function hasMessage(): bool
```
**Beschreibung:** Prüft, ob eine Status-Nachricht gesetzt ist.

### rex_cronjob_manager

Verwaltet die verfügbaren Cronjob-Typen und deren Ausführung.

#### Statische Methoden

##### registerType()
```php
static public function registerType(string $class): void
```
**Beschreibung:** Registriert einen neuen Cronjob-Typ.
**Beispiel:**
```php
rex_cronjob_manager::registerType('rex_cronjob_mein_typ');
```

##### getTypes()
```php
static public function getTypes(): array
```
**Beschreibung:** Liefert alle registrierten Cronjob-Typen.

##### factory()
```php
static public function factory(string $class): rex_cronjob
```
**Beschreibung:** Erstellt eine Instanz eines Cronjob-Typs.

### Parameterfeld-Definitionen

Parameterfelder werden als assoziative Arrays definiert:

#### Grundstruktur
```php
[
    'label' => 'Feldbezeichnung',        // Angezeigter Name
    'name' => 'parameter_name',          // Interner Parameter-Name
    'type' => 'text',                    // Feldtyp
    'default' => 'Standardwert',         // Optional: Standardwert
    'notice' => 'Hilfstext',             // Optional: Erläuterung
    'attributes' => []                   // Optional: HTML-Attribute
]
```

#### Verfügbare Feldtypen

##### text
Einzeiliges Texteingabefeld
```php
[
    'type' => 'text',
    'attributes' => ['placeholder' => 'Beispieltext']
]
```

##### textarea
Mehrzeiliges Texteingabefeld
```php
[
    'type' => 'textarea',
    'attributes' => ['rows' => 10, 'cols' => 50]
]
```

##### select
Auswahlfeld (Dropdown)
```php
[
    'type' => 'select',
    'options' => [
        'wert1' => 'Anzeige 1',
        'wert2' => 'Anzeige 2'
    ]
]
```

##### hidden
Verstecktes Feld (für interne Werte)
```php
[
    'type' => 'hidden',
    'default' => 'interner_wert'
]
```

#### HTML-Attribute

Über das `attributes` Array können beliebige HTML-Attribute gesetzt werden:

```php
[
    'type' => 'text',
    'attributes' => [
        'type' => 'email',              // HTML5-Eingabetyp
        'required' => 'required',       // Pflichtfeld
        'pattern' => '[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,}$',
        'title' => 'Gültige E-Mail-Adresse eingeben',
        'maxlength' => 255,
        'class' => 'form-control my-class',
        'data-toggle' => 'tooltip'
    ]
]
```

### Internationalisierung

Für mehrsprachige Anwendungen sollten alle sichtbaren Texte über das i18n-System verwaltet werden:

#### Sprachdatei (lang/de_de.lang)
```
mein_cronjob_typ = Mein Cronjob-Typ
mein_cronjob_param_email = E-Mail-Adresse
mein_cronjob_param_email_notice = Ziel-E-Mail für Benachrichtigungen
```

#### Verwendung im Code
```php
public function getTypeName()
{
    return rex_i18n::msg('mein_cronjob_typ');
}

public function getParamFields()
{
    return [
        [
            'label' => rex_i18n::msg('mein_cronjob_param_email'),
            'name' => 'email',
            'notice' => rex_i18n::msg('mein_cronjob_param_email_notice')
        ]
    ];
}
```

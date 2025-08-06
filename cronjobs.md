# Cronjobs

- [Einführung](#einfuehrung)
  - [Zweck des Cronjob-AddOns](#zweck)
  - [Anwendungsfälle](#anwendungsfaelle)
- [Installation und Konfiguration](#installation)
- [Cronjob erstellen](#cronjob-erstellen)
  - [Grundeinstellungen](#grundeinstellungen)
    - [Name](#name)
    - [Beschreibung](#beschreibung)
    - [Status](#status)
  - [Ausführungseinstellungen](#ausfuehrungseinstellungen)
    - [Umgebung](#umgebung)
    - [Ausführungszeitpunkt](#ausfuehrungszeitpunkt)
    - [Intervall](#intervall)
  - [Funktionalität](#funktionalitaet)
    - [Typ](#typ)
    - [Typspezifische Parameter](#typspezifische-parameter)
- [Ausführungsumgebungen im Detail](#umgebungen-detail)
  - [Skript-Umgebung (empfohlen)](#skript-umgebung)
  - [Frontend-Umgebung](#frontend-umgebung)
  - [Backend-Umgebung](#backend-umgebung)
  - [Server-Cronjob einrichten](#server-cronjob)
- [Eigene Cronjob-Typen entwickeln](#eigene-typen)
  - [Grundlagen](#grundlagen-entwicklung)
  - [Schritt-für-Schritt-Anleitung](#anleitung)
  - [Praktisches Beispiel](#praktisches-beispiel)
  - [Parameterfeld-Typen](#parameterfeld-typen)
  - [Erweiterte Funktionen](#erweiterte-funktionen)
  - [Debugging und Logging](#debugging)
- [API-Referenz](#api-referenz)
  - [rex_cronjob Klasse](#rex-cronjob-klasse)
  - [rex_cronjob_manager Klasse](#rex-cronjob-manager-klasse)
  - [Parameterfeld-Definitionen](#parameterfeld-definitionen)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)

<a name="einfuehrung"></a>
## Einführung

<a name="zweck"></a>
### Zweck des Cronjob-AddOns

Das Cronjob-AddOn ermöglicht die automatisierte, zeitgesteuerte Ausführung von Aufgaben in REDAXO. Es ist Teil der REDAXO-Basisinstallation, muss jedoch bei Bedarf separat installiert werden. Mit diesem AddOn können beliebig viele Cronjobs definiert werden, die gemäß individuellen Zeitplänen ausgeführt werden.

<a name="anwendungsfaelle"></a>
### Anwendungsfälle

Typische Einsatzgebiete für Cronjobs:

* **Wartungsaufgaben**: Regelmäßige Datenbank-Optimierung und Bereinigung
* **Content-Management**: Zeitgesteuertes Veröffentlichen oder Archivieren von Artikeln
* **Backup-Routinen**: Automatische Datenbank- und Datei-Backups
* **Synchronisation**: Abgleich mit externen Systemen (RSS-Feeds, APIs)
* **Benachrichtigungen**: Versand von E-Mail-Reports oder Newsletter
* **Datenverarbeitung**: Import/Export von Daten, Bildoptimierung
* **Monitoring**: Überwachung von System-Metriken und Alarmierung

<a name="installation"></a>
## Installation und Konfiguration

1. **Installation**: Das Cronjob-AddOn über den Installer aktivieren
2. **Konfiguration**: Unter `AddOns > Cronjob` die Verwaltungsoberfläche aufrufen
3. **Server-Cronjob**: Für optimale Performance einen Server-Cronjob einrichten (siehe [Server-Cronjob einrichten](#server-cronjob))

<a name="cronjob-erstellen"></a>
## Cronjob erstellen

<a name="grundeinstellungen"></a>
### Grundeinstellungen

<a name="name"></a>
#### Name
Ein aussagekräftiger Name für den Cronjob, z.B. `Tägliches Backup`, `RSS-Feed Import` oder `Cache-Bereinigung`.

<a name="beschreibung"></a>
#### Beschreibung
Eine detaillierte Beschreibung der Aufgabe. Diese hilft bei der späteren Wartung und Dokumentation.

<a name="status"></a>
#### Status
- **Aktiviert**: Cronjob wird gemäß Zeitplan ausgeführt
- **Deaktiviert**: Cronjob wird pausiert (Standard: aktiviert)

<a name="ausfuehrungseinstellungen"></a>
### Ausführungseinstellungen

<a name="umgebung"></a>
#### Umgebung

Die Umgebung bestimmt, wodurch der Cronjob ausgelöst wird:

| Umgebung | Auslöser | Empfohlen für |
|----------|----------|---------------|
| **Skript** | Server-Cronjob | Zeitkritische und regelmäßige Aufgaben |
| **Frontend** | Seitenaufruf im Frontend | Unkritische, seltene Aufgaben |
| **Backend** | Aktivität im Backend | Administrative Aufgaben |

**Wichtig**: Die Umgebung `Skript` sollte nicht gleichzeitig mit `Frontend` oder `Backend` aktiviert werden (außer zu Testzwecken).

<a name="ausfuehrungszeitpunkt"></a>
#### Ausführungszeitpunkt

Nur für Frontend/Backend-Umgebung relevant:
- **Beginn**: Vor dem Seitenaufbau (kann zu Verzögerungen führen)
- **Ende**: Nach dem Seitenaufbau (empfohlen)

<a name="intervall"></a>
#### Intervall

Definiert die Häufigkeit der Ausführung:
- Minütlich, stündlich, täglich, wöchentlich, monatlich
- Benutzerdefinierte Intervalle möglich
- Standard: Täglich nach 0:00 Uhr

<a name="funktionalitaet"></a>
### Funktionalität

<a name="typ"></a>
#### Typ

Verfügbare Standard-Typen:
- **PHP-Code**: Direkter PHP-Code
- **PHP-Callback**: Funktions- oder Methodenaufruf
- **URL-Aufruf**: HTTP-Request an eine URL

AddOns können weitere Typen bereitstellen:
- **Datenbankexport** (Backup-AddOn)
- **Search it: Reindexieren** (Search it-AddOn)
- Weitere projektspezifische Typen

<a name="typspezifische-parameter"></a>
#### Typspezifische Parameter

Je nach gewähltem Typ stehen unterschiedliche Eingabemöglichkeiten zur Verfügung:

**PHP-Code**:
```php
// Beispiel: Cache leeren
rex_delete_cache();
echo "Cache wurde geleert";
```

**PHP-Callback**:
```php
// Beispiel: Statische Methode
MyClass::myMethod
```

**URL-Aufruf**:
```
https://example.com/webhook
```

<a name="umgebungen-detail"></a>
## Ausführungsumgebungen im Detail

<a name="skript-umgebung"></a>
### Skript-Umgebung (empfohlen)

**Vorteile:**
- Unabhängig von Seitenaufrufen
- Zuverlässige, zeitgenaue Ausführung
- Keine Performance-Beeinträchtigung für Besucher
- Ideal für ressourcenintensive Aufgaben

**Nachteile:**
- Erfordert Zugriff auf Server-Cronjobs
- Keine Session-Informationen verfügbar

<a name="frontend-umgebung"></a>
### Frontend-Umgebung

**Vorteile:**
- Kein Server-Zugriff erforderlich
- Zugriff auf Frontend-Session

**Nachteile:**
- Abhängig von Besucheraufkommen
- Kann Ladezeiten beeinflussen
- Unregelmäßige Ausführung möglich

<a name="backend-umgebung"></a>
### Backend-Umgebung

**Vorteile:**
- Manuelle Ausführung möglich
- Zugriff auf Backend-Session
- Gut für administrative Aufgaben

**Nachteile:**
- Nur bei Backend-Aktivität
- Nicht für zeitkritische Aufgaben geeignet

<a name="server-cronjob"></a>
### Server-Cronjob einrichten

Für die Skript-Umgebung muss ein Server-Cronjob konfiguriert werden:

**1. Crontab öffnen:**
```bash
crontab -e
```

**2. Cronjob hinzufügen:**
```bash
# Jede Minute ausführen (empfohlen)
* * * * * /usr/bin/php /pfad/zu/redaxo/bin/console cronjob:run

# Alle 5 Minuten ausführen
*/5 * * * * /usr/bin/php /pfad/zu/redaxo/bin/console cronjob:run

# Stündlich ausführen
0 * * * * /usr/bin/php /pfad/zu/redaxo/bin/console cronjob:run
```

**Wichtig**: Das Server-Intervall sollte kleiner oder gleich dem kleinsten REDAXO-Cronjob-Intervall sein.

<a name="eigene-typen"></a>
## Eigene Cronjob-Typen entwickeln

<a name="grundlagen-entwicklung"></a>
### Grundlagen

Um einen eigenen Cronjob-Typ zu erstellen, muss eine PHP-Klasse von `rex_cronjob` abgeleitet werden. Diese definiert die Funktionalität und stellt Konfigurationsfelder bereit.

<a name="anleitung"></a>
### Schritt-für-Schritt-Anleitung

#### 1. Cronjob-Klasse erstellen

Erstelle eine PHP-Datei in `/redaxo/src/addons/mein_addon/lib/cronjob/`:

```php
<?php

class rex_cronjob_mein_typ extends rex_cronjob
{
    public function execute()
    {
        try {
            // Hauptfunktionalität implementieren
            $this->setMessage('Erfolgreich ausgeführt');
            return true;
        } catch (Exception $e) {
            $this->setMessage('Fehler: ' . $e->getMessage());
            return false;
        }
    }

    public function getTypeName()
    {
        return 'Mein Cronjob-Typ';
    }

    public function getParamFields()
    {
        return [
            [
                'label' => 'Parameter',
                'name' => 'mein_parameter',
                'type' => 'text',
                'notice' => 'Beschreibung des Parameters'
            ]
        ];
    }
}
```

#### 2. Typ registrieren

In der `boot.php` des AddOns:

```php
<?php
if (rex_addon::get('cronjob')->isAvailable()) {
    rex_cronjob_manager::registerType('rex_cronjob_mein_typ');
}
```

<a name="praktisches-beispiel"></a>
### Praktisches Beispiel

**Newsletter-Abonnenten-Benachrichtigung:**

```php
<?php

class rex_cronjob_subscriber_notification extends rex_cronjob
{
    public function execute()
    {
        $email = $this->getParam('notification_email');
        $table = $this->getParam('subscriber_table', 'rex_newsletter_user');
        $last_check = $this->getParam('last_check_timestamp', 0);
        
        if (empty($email)) {
            $this->setMessage('Keine E-Mail-Adresse konfiguriert');
            return false;
        }
        
        try {
            // Neue Abonnenten finden
            $sql = rex_sql::factory();
            $sql->setQuery(
                "SELECT * FROM {$table} 
                 WHERE createdate > :last_check 
                 AND status = 1",
                ['last_check' => date('Y-m-d H:i:s', $last_check)]
            );
            
            $new_subscribers = $sql->getArray();
            
            if (count($new_subscribers) > 0) {
                // E-Mail senden
                $this->sendNotification($email, $new_subscribers);
                $this->setMessage(count($new_subscribers) . ' neue Abonnenten gefunden');
            } else {
                $this->setMessage('Keine neuen Abonnenten');
            }
            
            // Zeitstempel aktualisieren
            $this->setParam('last_check_timestamp', time());
            
            return true;
            
        } catch (Exception $e) {
            $this->setMessage('Fehler: ' . $e->getMessage());
            return false;
        }
    }
    
    private function sendNotification($email, $subscribers)
    {
        if (!rex_addon::get('phpmailer')->isAvailable()) {
            throw new Exception('PHPMailer nicht verfügbar');
        }
        
        $mail = new rex_mailer();
        $mail->addAddress($email);
        $mail->Subject = 'Neue Newsletter-Abonnenten: ' . count($subscribers);
        
        $body = "Neue Abonnenten:\n\n";
        foreach ($subscribers as $subscriber) {
            $body .= "- {$subscriber['email']} ({$subscriber['createdate']})\n";
        }
        
        $mail->Body = $body;
        
        if (!$mail->send()) {
            throw new Exception('E-Mail-Versand fehlgeschlagen');
        }
    }
    
    public function getTypeName()
    {
        return 'Newsletter-Abonnenten-Benachrichtigung';
    }
    
    public function getParamFields()
    {
        return [
            [
                'label' => 'Benachrichtigungs-E-Mail',
                'name' => 'notification_email',
                'type' => 'text',
                'attributes' => ['type' => 'email'],
                'notice' => 'E-Mail für Benachrichtigungen'
            ],
            [
                'label' => 'Tabelle',
                'name' => 'subscriber_table',
                'type' => 'text',
                'default' => 'rex_newsletter_user'
            ],
            [
                'name' => 'last_check_timestamp',
                'type' => 'hidden',
                'default' => 0
            ]
        ];
    }
}
```

<a name="parameterfeld-typen"></a>
### Parameterfeld-Typen

#### Text-Eingabefeld
```php
[
    'label' => 'Textfeld',
    'name' => 'text_param',
    'type' => 'text',
    'default' => 'Standardwert',
    'notice' => 'Hilfetext',
    'attributes' => [
        'placeholder' => 'Platzhalter',
        'maxlength' => 255,
        'required' => 'required'
    ]
]
```

#### Textarea
```php
[
    'label' => 'Mehrzeiliger Text',
    'name' => 'textarea_param',
    'type' => 'textarea',
    'attributes' => ['rows' => 10, 'cols' => 50]
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
        'option2' => 'Zweite Option'
    ],
    'default' => 'option1'
]
```

#### Checkbox (als Select)
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
    'default' => 'interner_wert'
]
```

<a name="erweiterte-funktionen"></a>
### Erweiterte Funktionen

#### Umgebungen einschränken
```php
public function getEnvironments()
{
    // Nur in Skript-Umgebung verfügbar
    return ['script'];
}
```

#### Parameter zur Laufzeit ändern
```php
public function execute()
{
    $counter = (int) $this->getParam('counter', 0);
    $counter++;
    
    // Arbeit durchführen...
    
    // Counter für nächste Ausführung speichern
    $this->setParam('counter', $counter);
    
    $this->setMessage("Ausführung #{$counter} erfolgreich");
    return true;
}
```

<a name="debugging"></a>
### Debugging und Logging

```php
public function execute()
{
    $debug = [];
    
    try {
        // Schritt 1
        $debug[] = 'Daten geladen';
        
        // Schritt 2
        $debug[] = 'Verarbeitung abgeschlossen';
        
        // Bei Erfolg
        $this->setMessage('Erfolgreich: ' . implode(' > ', $debug));
        return true;
        
    } catch (Exception $e) {
        // Bei Fehler
        $this->setMessage(
            'Fehler nach: ' . implode(' > ', $debug) . 
            ' - ' . $e->getMessage()
        );
        return false;
    }
}
```

<a name="api-referenz"></a>
## API-Referenz

<a name="rex-cronjob-klasse"></a>
### rex_cronjob Klasse

#### Abstrakte Methoden (müssen implementiert werden)

| Methode | Rückgabe | Beschreibung |
|---------|----------|--------------|
| `execute()` | `bool` | Hauptfunktionalität des Cronjobs |

#### Optionale Methoden

| Methode | Rückgabe | Beschreibung |
|---------|----------|--------------|
| `getTypeName()` | `string` | Anzeigename im Backend |
| `getParamFields()` | `array` | Konfigurationsfelder |
| `getEnvironments()` | `array` | Verfügbare Umgebungen |

#### Parameter-Methoden

| Methode | Parameter | Beschreibung |
|---------|-----------|--------------|
| `setParam($key, $value)` | string, mixed | Einzelnen Parameter setzen |
| `getParam($key, $default)` | string, mixed | Parameter abrufen |
| `setParams($params)` | array | Alle Parameter setzen |
| `getParams()` | - | Alle Parameter abrufen |

#### Nachrichten-Methoden

| Methode | Parameter | Beschreibung |
|---------|-----------|--------------|
| `setMessage($message)` | string | Status-Nachricht setzen |
| `getMessage()` | - | Nachricht abrufen |
| `hasMessage()` | - | Prüft ob Nachricht vorhanden |

<a name="rex-cronjob-manager-klasse"></a>
### rex_cronjob_manager Klasse

| Methode | Parameter | Beschreibung |
|---------|-----------|--------------|
| `registerType($class)` | string | Neuen Typ registrieren |
| `getTypes()` | - | Alle Typen abrufen |
| `factory($class)` | string | Instanz erstellen |

<a name="parameterfeld-definitionen"></a>
### Parameterfeld-Definitionen

#### Grundstruktur
```php
[
    'label' => 'Bezeichnung',      // Pflicht: Anzeigename
    'name' => 'parameter_name',    // Pflicht: Interner Name
    'type' => 'text',              // Pflicht: Feldtyp
    'default' => '',               // Optional: Standardwert
    'notice' => '',                // Optional: Hilfetext
    'attributes' => [],            // Optional: HTML-Attribute
    'options' => []                // Nur für type='select'
]
```

#### HTML5-Eingabetypen

Über das `attributes` Array können HTML5-Typen gesetzt werden:

```php
// E-Mail
['attributes' => ['type' => 'email']]

// Nummer
['attributes' => ['type' => 'number', 'min' => 0, 'max' => 100]]

// Datum
['attributes' => ['type' => 'date']]

// URL
['attributes' => ['type' => 'url']]
```

<a name="best-practices"></a>
## Best Practices

### Performance

1. **Skript-Umgebung verwenden** für zeitkritische Aufgaben
2. **Ressourcenintensive Aufgaben** in kleinere Teile aufteilen
3. **Timeouts beachten** und ggf. erhöhen
4. **Datenbankabfragen optimieren** (Indizes nutzen)

### Fehlerbehandlung

1. **Try-Catch-Blöcke** verwenden
2. **Aussagekräftige Fehlermeldungen** zurückgeben
3. **Logging** für kritische Operationen implementieren
4. **Transaktionen** bei Datenbankoperationen nutzen

### Sicherheit

1. **Eingaben validieren** bei Parametern
2. **Berechtigungen prüfen** bei sensiblen Operationen
3. **Prepared Statements** für Datenbankabfragen
4. **Externe APIs** mit Timeouts absichern

### Wartbarkeit

1. **Sprechende Namen** für Cronjobs und Parameter
2. **Dokumentation** in Beschreibungsfeldern
3. **Versionierung** bei eigenen Typen
4. **Internationalisierung** über Sprachdateien

<a name="troubleshooting"></a>
## Troubleshooting

### Cronjob wird nicht ausgeführt

**Mögliche Ursachen:**
- Cronjob ist deaktiviert
- Server-Cronjob nicht eingerichtet
- Falsches Intervall konfiguriert
- PHP-Fehler im Code

**Lösungsansätze:**
1. Status prüfen (aktiviert?)
2. Server-Cronjob testen: `/pfad/zu/redaxo/bin/console cronjob:run`
3. Error-Log prüfen
4. Manuell im Backend ausführen (Test)

### Performance-Probleme

**Optimierungen:**
- Große Datenmengen in Batches verarbeiten
- Datenbankabfragen mit LIMIT versehen
- Caching implementieren
- Auf Skript-Umgebung umstellen

### E-Mail-Versand funktioniert nicht

**Prüfpunkte:**
- PHPMailer-AddOn installiert und konfiguriert?
- SMTP-Einstellungen korrekt?
- Spam-Filter prüfen
- Test-Mail über PHPMailer-AddOn senden

### Debugging aktivieren

```php
public function execute()
{
    // Debug-Modus
    if ($this->getParam('debug_mode')) {
        rex_logger::factory()->log('info', 'Cronjob Start', [
            'params' => $this->getParams(),
            'time' => date('Y-m-d H:i:s')
        ]);
    }
    
    // Cronjob-Logik...
    
    return true;
}
```

# Benutzerrechte

In REDAXO werden die Nutzerrechte über Rollen definiert. Rollen sammeln die Berechtigungen, die den Benutzern zugeteilt werden können.  Die zuständige Klasse für einfache Berechtigungen ist [rex_perm](https://friendsofredaxo.github.io/phpdoc/classes/rex-perm.html), die für erweiterte Berechtigungen (als `multiselect`-Feld) ist [rex_complex_perm](https://friendsofredaxo.github.io/phpdoc/classes/rex-complex-perm.html)

## Definieren

Berechtigungen können in der Datei `package.yml` definiert werden, oder später im PHP-Code des AddOns.

### Package.yml

```yml
page:
 title: translate:title
 perm: addonname[]
 subpages:
  foo: {perm: addonname[foo], title: translate:foo}
  bar: {perm: addonname[bar], title: translate:bar}
```

### PHP

Zur Laufzeit können die Berechtigungen in Gruppen eingeteilt werden und weitere registriert werden. 

```php
<?php

if(rex::isBackend() && is_object(rex::getUser())) {
  rex_perm::register('addonname[]', null);
  rex_perm::register('addonname[]', "foo");
  rex_perm::register('addonname[]', "translate:bar");
}
```

Der 2. Parameter gibt eine zusätzliche Beschriftung aus. 

Ohne den dritten Parameter werden alle Berechtigungen in die Gruppe `rex_perm::GENERAL` gespeichert. Diese Berechtigungen erscheinen in den Rollen unter `Allgemein`. 

Dazu gibt es noch `rex_perm::OPTIONS` und `rex_perm::EXTRAS`. Diese Zusatzgruppen eigenen sich gut um die einzelnen Features eines AddOns freizugeben, wogegen GENERAL eher genutzt wird, um den Zugriff auf das AddOn/Plugin generell zu erlauben für diese Rolle.

```php
<?php

if(rex::isBackend() && is_object(rex::getUser())) {
  rex_perm::register('addonname[]', "Mein Addon");
  rex_perm::register('addonname[foo]', "translate:addon_foo", rex_perm::OPTIONS);
  rex_perm::register('addonname[bar]', "translate:addon_bar", rex_perm::GENERAL);
}
```

## Komplexe Berechtigungen

Komplexe Berechtigungen werden mit der Klasse `rex_complex_perm` realisiert. Hier am Beispiel des YForm 4 Table-Managers:

### boot.php

```php
rex_complex_perm::register('yform_manager_table_view', 'rex_yform_manager_table_perm_edit');
```

### Eigene Klasse
```php
class rex_yform_manager_table_perm_edit extends rex_complex_perm
{
    public function hasPerm($table_name)
    {
        return $this->hasAll() || in_array($table_name, $this->perms);
    }

    public static function getFieldParams()
    {
        $arrayOptions = [];
        foreach (rex_yform_manager_table::getAll() as $table) {
            $arrayOptions[$table->getTableName()] = rex_i18n::translate($table->getName()).' ['.$table->getTableName().']';
        }

        return [
            'label' => rex_i18n::msg('yform_manager_table'),
            'all_label' => rex_i18n::msg('yform_manager_tables_edit'),
            'options' => $arrayOptions,
        ];
    }
}
```

## Berechtigungen prüfen

Es empfiehlt sich, zu prüfen, ob der Benutzer eingeloggt ist.

### Ist Admin

Prüfen, ob der User ein Admin ist `rex::getUser()->isAdmin()`.

### Einzelne Rechte prüfen

Prüfen, ob der User die nötigen Rechte aktiviert hat:

```php
if( rex::getUser()->hasPerm('addonname[]') && rex::getUser()->hasPerm('addonname[foo]') ) {
 // code goes here
}
```

### Zugriff auf Module

Weitere Berechtigungen wie Module können wie folgt abgefragt werden:

```php
if( rex::getUser()->getComplexPerm('modules')->hasPerm($ModuleID) ) {
 // code goes here
}
```

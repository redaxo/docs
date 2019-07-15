
# Konfigurations-Formulare für AddOns

Möchte man individuelle Einstellungen durch den Nutzer festlegen lassen, benötigt man Formulare zur Pflege der AddOn-Konfiguration. 
Hierzu mussten bis REDAXO 5.4.0 die Formulare manuell erstellt werden und die Config selbst gespeichert werden. Mit `rex_config_form` hat sich das grundlegend geeändert.
`rex_config_form` erlaubt es Konfigurationen mittels `rex_form` zu erstellen. 

Zuständig ist dafür ist die auf der `rex_form_base` aufsetzende Class `rex_config_form`.


Instanzieren der `rex_config_form`

```php
$form = rex_config_form::factory("addonxyz");
```

`addonxyz` ist der Namespace in der Tabelle `rex_config`


```php
$field = $form->addTextField('field_key');
```

`field_key` ist der Schlüssel in der Tabelle `rex_config`

Der Absende-Button und die Routinen zum Speichern der Daten werden automatisch hinzugefügt. 

Damit das Formular im REDAXO-Stil ausgegeben werden kann, wird es an das section-Fragment übergeben. 

```php
$fragment = new rex_fragment();
$fragment->setVar('class', 'edit', false);
$fragment->setVar('title', $this->i18n('example_title'), false);
$fragment->setVar('body', $form->get(), false);
echo $fragment->parse('core/page/section.php');
```


Mit `rex_config_form` kann ein Konfigurationsformular also wie folgt erstellt werden: 


```php
$addon = rex_addon::get('beispiel_addon');
$form = rex_config_form::factory($addon->name);

$field = $form->addInputField('vorname');
$field->setLabel("Vorname");

$field = $form->addInputField('nachname');
$field->setLabel("Nachname");

$fragment = new rex_fragment();
$fragment->setVar('class', 'edit', false);
$fragment->setVar('title', "Beispiel-Einstellungen", false);
$fragment->setVar('body', $form->get(), false);
echo $fragment->parse('core/page/section.php');

```


Zum Vergleich: Beispiel des gleichen Konfigurationsformulars vor REDAXO Version 5.4.0 (manuell gebaute Formular) 

```php
$addon = rex_addon::get('beispiel_addon');

$content = '';

if (rex_post('config-submit', 'boolean')) {
    $addon->setConfig(rex_post('config', [
        ['vorname', 'string'],
        ['nachname', 'string'],
    ]));

    $content .= rex_view::info('Änderung gespeichert');
}

$content .=  '
<div class="rex-form">
    <form action="' . rex_url::currentBackendPage() . '" method="post">
        <fieldset>';

$formElements = [];

$n = [];
$n['label'] = '<label for="rex-out5-border-text">Vorname</label>';
$n['field'] = '<input class="form-control"  type="text" id="rex-out5-border-text" name="config[nachname]" value="' . $addon->getConfig('vorname') . '"/>';
$formElements[] = $n;

$n['label'] = '<label for="rex-out5-border-farbe">Nachname</label>';
$n['field'] = '<input class="form-control" type="text" id="rex-out5-border-farbe" name="config[nachname]" value="' . $addon->getConfig('nachname'). '"/>';
$formElements[] = $n;

$fragment = new rex_fragment();
$fragment->setVar('elements', $formElements, false);
$content .= $fragment->parse('core/form/form.php');
$content .= '
        </fieldset>
        <fieldset class="rex-form-action">';
$formElements = [];
$n = [];
$n['field'] = '<div class="btn-toolbar"><button id="rex-out5-border-save" type="submit" name="config-submit" class="btn btn-save rex-form-aligned" value="1">Einstellungen speichern</button></div>';
$formElements[] = $n;
$fragment = new rex_fragment();
$fragment->setVar('elements', $formElements, false);
$content .= $fragment->parse('core/form/submit.php');
$content .= '
        </fieldset>
    </form>
</div>';
$fragment = new rex_fragment();
$fragment->setVar('class', 'edit');
$fragment->setVar('title', 'Beispiel-Einstellungen');
$fragment->setVar('body', $content, false);
echo $fragment->parse('core/page/section.php');
```










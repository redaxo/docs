# Datenbankzugriff - rex_sql Klasse

Neben den Möglichkeiten des OOP Frameworks, bietet REDAXO mit der rex_sql Klasse Zugriff
auf die REDAXO-Tabellen oder andere Addon Tabellen.

## READ: Einträge aus rex_file lesen

```PHP
<?php
$db_table = "rex_file";

$sql = rex_sql::factory();
// $sql->debugsql = 1; //Ausgabe Query
$sql->setQuery("SELECT * FROM $db_table WHERE category_id=1");

$ausgabe = '<ul>';
for($i=0; $i<$sql->getRows(); $i++)
{
$filename = $sql->getValue('filename'); 
$ausgabe .= '<li>' . $filename . '</li>'; 

$sql->next();
}	
$ausgabe .= '</ul>';

print $ausgabe;

?>
```

## WRITE: Einträge schreiben


```PHP
<?php

$db_table = "rex_addon_mytabelle";

$db = rex_sql::factory();
$db->debugsql = 0;
$db->setTable($db_table);	

$db->setValue("name", rex_post('name', 'string'));
$db->insert();

?>
```


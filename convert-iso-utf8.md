# # Inhalte von Iso auf Utf-8 konvertieren

Sagen wir mal wir haben REDAXO mit dem Zeichensatz iso-8859-1 erstellt (Standardeinstellung) und stellen fest das nun neue sprachen hinzukommen sollen und wir alles auf utf-8 konvertieren müssen.

Da REDAXO nur einen allgemeinen Zeichensatz akzeptiert müssen wir die vorhandenen Inhalte konvertieren. Mit diesem Skript kann man dies tun. Dabei werden alle Tabellen ausgelesen und anhand des primary keys geupdated. Bitte darauf achten, dass alle Tabellen aus der vorhandenen Datenbank ausgelesen und aktualisiert werden. Außerdem bitte DATENBANKNAME einsetzen. nur einmal ausführen und am besten eine Sicherung machen. Viel erfolg..

## Vorgehensweise:

* Folgenden Code in ein neues aktives Template einfügen
* Artikel anlegen und das neue Template dem Artikel zuweisen
* Artikel via Frontend aufrufen
* fertig

```PHP

<?php

$gt = new sql();
$gt->setQuery("show tables");

for ($t=0;$t<$gt->getRows();$t++)
{

	$table = $gt->getValue("Tables_in_DATENBANKNAME");

	$gc = new sql();
	$gc->setQuery("show columns from $table");

	unset($columns);
	$columns = Array();
	$pri = "";
	for ($c=0;$c<$gc->getRows();$c++)
	{
		$columns[] = $gc->getValue("Field");
		if ($pri == "" && $gc->getValue("Key") == "PRI") $pri = $gc->getValue("Field");
		$gc->next();
	}

	if ($pri != "")
	{

		$gr = new sql();
		$gr->setQuery("select * from $table");

		echo "<br /><br /><b>$table | $pri</b>:";
		for($r=0;$r<$gr->getRows();$r++)
		{
			reset($columns);

			$privalue = $gr->getValue($pri);

			$uv = new sql();
			$uv->setTable($table);
			$uv->where($pri.'="'.$privalue.'"');
			echo "<br /> -- <b>$privalue</b> :"; 
			foreach($columns as $key => $column)
			{
				if ($pri!=$column)
				{
					$value = $gr->getValue($column);
					$newvalue = utf8_encode($value);
					$uv->setValue($column,addslashes($newvalue));
					echo " | ".substr($value,0,20)."... => ".substr($newvalue,0,20)."...";
				}
			}
			$uv->update();
			// echo $uv->printError();
			$gr->next();	
		}

	}

	$gt->next();
}



?>

```

## Von ISO-1 auf UTF-8 nur auf spezielle Tabellen und Queries.


```PHP
<?php

$quers[0]["rex_article_slice"] = "select * from rex_article_slice where clang=5";

foreach($quers as $quer)
{ 

	$table = key($quer);
	$query = current($quer);

	$gc = new sql();
	$gc->setQuery("show columns from $table");
	unset($columns);
	$columns = Array();
	$pri = "";


	echo "<p>Table:$table <br />Query:$query Spalten: ";
	for ($c=0;$c<$gc->getRows();$c++)
	{
		$columns[] = $gc->getValue("Field");
		if ($pri == "" && $gc->getValue("Key") == "PRI") $pri = $gc->getValue("Field");
		echo $gc->getValue("Field")." ";
		$gc->next();
	}
	echo "<br />PRIMARY KEY: $pri</p>";

	if ($pri != "")
	{
		$gr = new sql();
		$gr->setQuery($query);

		echo "<p><b>$table | $pri | $query</b>:</p>";
		for($r=0;$r<$gr->getRows();$r++)
		{
			reset($columns);
			$privalue = $gr->getValue($pri);
			$uv = new sql();
			$uv->setTable($table);
			$debug = $table;
			$uv->where($pri.'="'.$privalue.'"');
			$update = FALSE;
			$out = "<br />-- <b>$privalue</b>:<br />";
			foreach($columns as $key => $column)
			{
				if ($pri!=$column) {
					$value = $gr->getValue($column);
					$newvalue = utf8_encode($value);
					if ($value != $newvalue)
					{
						$uv->setValue($column,addslashes($newvalue));
						$out .= 
							"<pre>".
							htmlspecialchars(str_replace("\n\r","",substr($value,0,1000)))."
=>
".
							'<span style="color:green;">'.
							htmlspecialchars(str_replace("\n\r","",substr($newvalue,0,1000))).
							'</span>'.
							"</pre>";
						$update = TRUE;
					}
				}
			}
			if ($update)
			{
				// $uv->update(); 
				//echo $uv->printError(); 
				echo $out."</p>";
			}else
			{
				// echo "<br />NO UPDATE - Nothing has been changed";
			}
			$gr->next();
		}
	}
}

?>
```


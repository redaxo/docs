# URLs

- [Standard-URL-Schema](#standard-url-schema)
- [URL-Rewrite-AddOns](#standard-url-schema)
- [URLs formatieren mit rex_getUrl()](#standard-url-schema)
    - [Artikel-ID](#standard-url-schema)
    - [Sprach-ID](#standard-url-schema)
    - [Parameter](#standard-url-schema)
    - [Trennzeichen](#standard-url-schema)

<a name="standard-url-schema"></a>
## Standard-URL-Schema

Das standardmäßige URL-Schema des REDAXO-Frontends arbeitet mit der Artikel-ID, bzw. zusätzlich mit der Sprach-ID, sofern mehrere Sprachen im CMS angelegt wurden:
```
// Dieser Link führt zum Artikel mit der ID 3
./index.php?article_id=3
```

Sofern mehr als eine Sprache in REDAXO existiert, also eine oder mehrere Sprachen angelegt wurden, taucht zusätzlich die Sprach-ID mit in der URL auf:
```
// Dieser Link führt zum Artikel mit der ID 3 in der SPrache mit der ID 2
./index.php?article_id=3&clang=2
```

> Hinweis: Auch Links zu Artikeln der aktuellen Sprache enthalten diesen Sprachparameter, obwohl er nicht nötig wäre.

<a name="url-rewrite-addons"></a>
## URL-Rewrite-AddOns

Beim Einsatz von URL-Rewrite-AddOns wie beispielsweise yRewrite werden "schönere" URLs generiert, die für den Besucher angenehmer zu erfassen und auch für Suchmaschinen leichter auszuwerten sind. Diese URLs orientieren sich am klassischen Ordner--Schema von statischen Websites aund lauten z.B. so:
```
/ueber-uns/kontakt/
```

<a name="rex-get-url"></a>
## URLs formulieren mit rex_getUrl

Wenn man Frontend-URLs zu internen REDAXO-Artikeln setzt, möchte man dies natürlich in einer Weise tun, die unabhängig von jeglichen Rewrite-Mechanismen immer funktioniert. Hierbei hilft die Funktion `rex_getUrl`.

Parameter | Erklärung
------------- | ------------- 
`$id` | Die ID des gewünschten Artikels
`$clang` | Die ID der gewünschten Sprache
`$params` | Array von Parametern
`$separator` | Das Trennzeichen zwischen den Parametern (Default: '&amp;')

<a name="artikel-id"></a>
### Artikel-ID

Beim Aufruf übergibt man rex_getUrl im Normlfall eine gültige Artikel-ID. Die Artikel-ID kann als feste Zahl oder auch dynamisch mittels einer Variable übergeben werden:
```
// Die URL des aktuellen Artikels wird ausgegeben
$aktuelle_id = $this->getValue('article_id');
<?php echo rex_getUrl($aktuelle_id); ?>
```

<a name="sprach-id"></a>
### Sprach-ID

Beim mehrsprachigen Websites wird als zweiter Parameter die Sprach-ID übergeben. Dieser Aufruf wechselt zum aktuellen Artikel in der Sprache mit der ID 2:
```
// Die URL des aktuellen Artikels in der Sprache mit der ID 2 ausgegeben
$aktuelle_id = $this->getValue('article_id');
<?php echo rex_getUrl($aktuelle_id, 2); ?>
```

Mehr Information über Links in mehrsprachigen Websites findet sich im Kapitel [Mehrsprachigkeit](/{{path}}/{{version}}/mehrsprachigkeit)

<a name="parameter"></a>
### Parameter

```
// Die URL des aktuellen Artikels in der Sprache mit der ID 2 ausgegeben
$aktuelle_id = $this->getValue('article_id');
<?php echo rex_getUrl($aktuelle_id, rex_clang::getCurrentId(), array ('chapters' => 2, 'page' => 3) ); ?>
```


<a name="trennzeichen"></a>
### Trennzeichen



/**
58  * Leitet auf einen anderen Artikel weiter.
59  *
60  * @param null|int|string $article_id
61  * @param null|int|string $clang      SprachId des Artikels
62  *
63  * @throws InvalidArgumentException
64  *
65  * @package redaxo\structure
66  */
67 function rex_redirect($article_id, $clang = null, array $params = [])
68 {
69     if (null !== $article_id && '' !== $article_id && !is_int($article_id) && $article_id !== (string) (int) $article_id) {
70         throw new InvalidArgumentException(sprintf('"%s" is not a valid article_id!', $article_id));
71     }
72 
73     rex_response::sendRedirect(rex_getUrl($article_id, $clang, $params, '&'));
74 }


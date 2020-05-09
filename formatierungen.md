# Formatierungen

* [Formatierungen rex_formatter](#rex-formatter)
  + [Aufruf von rex_formatter](#aufruf-von-rex-formatter)
  + [Ein einfaches Beispiel](#einfaches-beispiel)
  + [Formattypen](#formattypen)
    - [date](#date)
    - [strftime](#strftime)
    - [number](#number)
    - [bytes](#bytes)
    - [sprintf](#sprintf)
    - [nl2br](#nl2br)
    - [truncate](#truncate)
    - [widont](#widont)
    - [version](#version)
    - [url](#url)
    - [email](#email)
    - [custom](#custom)

<a name="rex-formatter"></a>

## Formatierungen rex_formatter

Der `rex_formatter` formatiert Strings zu einem bestimmten Formattyp. Eine komplette Liste findet sich in der <https://redaxo.org/api/master/source-class-rex_formatter.html>

<a name="aufruf-von-rex-formatter"></a>

## Aufruf von rex_formatter

Folgendermaßen lässt sich der `rex_formatter` generell aufrufen:

``` php
$formattedString = rex_formatter::( string $value, string 'formatType', string 'format');
```

| Parameter    | Erklärung                                              |
|--------------|--------------------------------------------------------|
| `$value` | Die Variable, die formatiert werden soll               |
| `formatType` | Die Formatierung, die angewandt werden soll            |
| `format` | Das Format, in der die Variable ausgegeben werden soll |

<a name="einfaches-beispiel"></a>

## Ein einfaches Beispiel

``` php
$date = 'March 9. 2018 10:31 PM';
echo rex_formatter::format($date,'date','Y.m.d H:i');
// gibt aus: 2018.03.09 22:31
```

<a name="formattypen"></a>

## Formattypen

Folgende Formattypen stehen zur Verfügung:

* [date](#date)
* [strftime](#strftime)
* [number](#number)
* [bytes](#bytes)
* [sprintf](#sprintf)
* [nl2br](#nl2br)
* [truncate](#truncate)
* [widont](#widont)
* [version](#version)
* [url](#url)
* [email](#email)
* [custom](#custom)

<a name="date"></a>

### date

Formatiert den übergebenen String in ein Datum mit dem gewählten Format.
Die zu verwendenden Format-Zeichen finden sich im [date-Manual](http://php.net/manual/de/function.date.php) von PHP.

``` php
$value = 'March 9. 2018 10:31 PM';
echo rex_formatter::format($value,'date','Y.m.d H:i');
// gibt aus: 2018.03.09 22:31
```

<a name="strftime"></a>

### strftime

Formatiert den übergebenen String in das gewählte Format. Dabei ist es möglich, einen Timestamp oder einen Datetime-String zu übergeben.
Die zu verwendenden Format-Zeichen finden sich im [strftime-Manual](http://php.net/manual/de/function.strftime.php) von PHP.

``` php
$datetime = 'March 9. 2018 10:31 PM';
echo rex_formatter::format($datetime,'strftime','%a KW %V');
// gibt aus: Fri KW 10

$timestamp = '1520631060';
$formattedString = rex_formatter::format($timestamp,'strftime','%a KW %V');
// gibt aus: Fri KW 10
```

<a name="number"></a>

### number

Formatiert das übergebene Value in eine Nummer mit dem gewählten Format. Das übergebene Format muss als Array angelegt sein, wie im [number_format-Manual](http://www.php.net/manual/en/function.number-format.php) von PHP angegeben. Der voreingestellte Standard, wenn kein `$number_format` übergeben wird, ist `array(2, ',', ' ')` .

``` php
$number = '12345.6789';
$numberFormat = [2,",","."];
echo rex_formatter::format($number,'number',$numberFormat);
// gibt aus: 12.345,68

$formattedString = rex_formatter::number($number,$numberFormat);
// gibt aus: 12.345,68
```

``` php
$number_format = [decimal_numbers 2, decimals_point ',', thousands_seperator ' ']
```

#### Number-Format-Parameter

| Parameter              | Erklärung                                                            |
|------------------------|----------------------------------------------------------------------|
| `decimal_numbers` | Die Anzahl an Stellen, die hinter dem Komma ausgegeben werden sollen |
| `decimals_point` | Das Trennzeichen für Komma-Zahlen                                    |
| `thousands_sepearator` | Das Trennzeichen für Tausender-Trennung                              |

<a name="bytes"></a>

### bytes

Formatiert das übergebene Value zu einem String, bei dem die Größe angehängt wird. Das Format definiert, wie die Nummer angezeigt werden soll (s. [number](#number)).
Je nach Größe des übergebenen Values werden automatisch folgende Byte-Größen angehängt:
`'B', 'KiB', 'MiB', 'GiB', 'TiB', 'PiB', 'EiB', 'ZiB', 'YiB'` 

``` php
$bytes = '1234567890';
$numberFormat = [2,",","."];
echo rex_formatter::format($bytes,'bytes',$numberFormat);
// gibt aus: 1,15 GiB

echo rex_formatter::bytes($bytes,$numberFormat);
// gibt aus: 1,15 GiB
```

<a name="sprintf"></a>

### sprintf

Formatiert / ersetzt das übergebene Value in das gewählte Format. Fallback ist `%s` , wenn kein Format angegeben wurde. Beim `rex_formatter` kann immer nur ein Value formatiert werden. Will man verschiedene Values in einem String ersetzen / formatieren, lohnt es sich eher, die [sprintf-Funktion](http://www.php.net/manual/en/function.sprintf.php) direkt von PHP zu nutzen. Alle weiteren Formate können im [sprintf-Manual](http://www.php.net/manual/en/function.sprintf.php) eingesehen werden.

``` php
$format = 'REDAXO ist %s';
$whatitis = 'einfach, flexibel, sinnvoll!';
echo rex_formatter::format($whatitis,'sprintf',$format);
// gibt aus: REDAXO ist einfach, flexibal, sinnvoll!

echo rex_formatter::sprintf($whatitis,$format);
// gibt aus: REDAXO ist einfach, flexibal, sinnvoll!
```

<a name="nl2br"></a>

### nl2br

Formatiert das übergebene Value in einen String mit `<br>` , wenn das Value eine `new line` enthält, z. B. `\n` oder `PHP_EOL` . Achtung: Wenn `rex_formatter::format()` genutzt wird, muss hier zum Schluss ein leeres Format `''` übergeben werden.

``` php
$nl2br = 'REDAXO
ist
einfach,
flexibel,
sinnvoll!';

echo rex_formatter::format($nl2br,'nl2br','');
/* gibt aus:
REDAXO<br>
ist<br>
einfach,<br>
flexibel,<br>
sinnvoll!
*/

$nl2br = 'REDAXO'.PHP_EOL.'ist'.PHP_EOL.'einfach,'.PHP_EOL.'flexibel,'.PHP_EOL.'sinnvoll!';
echo rex_formatter::nl2br($nl2br);
/* gibt aus:
REDAXO<br>
ist<br>
einfach,<br>
flexibel,<br>
sinnvoll!
*/
```

<a name="truncate"></a>

### truncate

Schneidet das übergebene Value nach der eingestellten Länge `length` im Format-Array ab und hängt die bei `etc` definierten Trennzeichen an. Der Parameter `break_words` im Format-Array ist Boolean `(false/true)` . Standard-Einstellung für das Format bei `truncate` ist `array('length' => 80, 'etc' => '...', 'break_words' => false)` .  

``` php
$truncateThis = 'REDAXO ist einfach, flexibel, sinnvoll!';

echo rex_formatter::format($truncateThis,'truncate',array('length' => '18','etc' => '!!!', 'break_words' => false));
// gibt aus: REDAXO ist!!!

echo rex_formatter::truncate($truncateThis,array('length' => '9','etc' => '!!!', 'break_words' => false));
// gibt aus: REDAXO!!!
```

#### truncate Format-Array

| Parameter     | Erklärung                                                                                                                          |
|---------------|------------------------------------------------------------------------------------------------------------------------------------|
| `length` | Die Länge, auf die das Value gekürzt werden soll - Standard ist `80` |
| `etc` | Die anzuhängenden Trennzeichen - Standard ist `...` |
| `break_words` | Boolean `false/true` - Ob die Länge hart berücksichtigt und innerhalb von Wörtern abgeschnitten werden soll - Standard ist `false` |

<a name="widont"></a>

### widont

Sollte ein Wort allein in einer Zeile vorkommen, wird dies unterbunden. Das letzte Leerzeichen wird durch ein geschütztes Leerzeichen ersetzt, sodass die letzten beiden Worte in die nächste Zeile rutschen. Achtung: Wenn `rex_formatter::format()` genutzt wird, muss hier zum Schluss ein leeres Format `''` übergeben werden.

``` php
$widow = 'REDAXO ist einfach, flexibel, sinnvoll!';

echo rex_formatter::format($widow,'widont','');
// gibt aus (im Quelltext): REDAXO ist einfach, flexibel,&#160;sinnvoll!

echo rex_formatter::widont($widow);
// gibt aus (im Quelltext): REDAXO ist einfach, flexibel,&#160;sinnvoll!
```

<a name="version"></a>

### version

Formatiert den übergebenen Versions-String. Die zur Verfügung stehenden Formate können im [sprintf-Manual](http://www.php.net/manual/en/function.sprintf.php) eingesehen werden.

``` php
$version = 5.5.1;
echo rex_formatter::format($version,'version','%d.%d');
// gibt aus: 5.5

echo rex_formatter::version($version,'%s-%s');
// gibt aus: 5-5
```

<a name="url"></a>

### url

Formatiert das übergebene Value als Link-Url. Es können über den Format-Teil zusätzliche Attribute (wie z. B. `target="_blank"` ) sowie anzuhängende Parameter (wie z. B. `subject=Hello%20Friend` ) übergeben werden.<br>
Der Format-Teil ist als Array anzugeben in der Reihenfolge `array('attr' => '', 'params' => '')` . Die `attr` sowie die `params` sind als String in dem Array anzugeben.

``` php
$url = 'www.redaxo.org';
echo rex_formatter::format($url,'url',array('attr' => 'target="_blank" class="whatever"','params' => 'subject=Hello%20Friend'));
// gibt aus (im Quelltext): <a href="http://www.redaxo.org?subject=Hello%20Friend" target="_blank" class="whatever">http://www.redaxo.org</a>

echo rex_formatter::url($url);
// gibt aus (im Quelltext): <a class="extern" href="http://www.redaxo.org">http://www.redaxo.org</a>
```

<a name="email"></a>

### email

Formatiert das übergebene Value als E-Mail-Link in `htmlspecialchars` . Es können über den Format-Teil zusätzliche Attribute (wie z. B. `target="_blank"` ) sowie anzuhängende Parameter (wie z. B. `subject=Hello%20Friend` ) übergeben werden.<br>
Der Format-Teil ist als Array anzugeben in der Reihenfolge `array('attr' => '', 'params' => '')` . Die `attr` sowie die `params` sind als String in dem Array anzugeben.

``` php
$email = 'info@redaxo.org';
echo rex_formatter::format($email,'email',array('attr' => 'target="_blank" class="whatever"','params' => 'subject=Hello%20Friend'));
// gibt aus (im Quelltext): <a href="mailto:info@redaxo.org?subject=Hello%20Friend" target="_blank" class="whatever">info@redaxo.org</a>

echo rex_formatter::email($email);
// gibt aus (im Quelltext): <a href="mailto:info@redaxo.org">info@redaxo.org</a>

```

<a name="custom"></a>

### custom

Über `custom` -Format lässt sich z. B. eine Funktion aufrufen, die dann die gewünschte Formatierung ausführt. Es können auch direkt PHP-Funktionen aufgerufen werden.

``` php
function test($param = '') {
    return $param . ' ist einfach, flexibel, sinnvoll!';
}

$custom = 'REDAXÖ';
echo rex_formatter::format($custom,'custom','test');
// gibt aus: REDAXÖ ist einfach, flexibel, sinnvoll!

echo rex_formatter::custom($custom,'htmlentities');
// gibt aus (im Quelltext): REDAX&Ouml;
```

# Responses

* [Die Klasse rex_response](#rex_response)
* [Methoden](#methoden)
  + [setStatus](#setstatus)
  + [getStatus](#getstatus)
  + [sendRedirect](#sendredirect)
  + [sendFile](#sendfile)
  + [sendResource](#sendresource)
  + [sendPage](#sendpage)
  + [sendContent](#sendcontent)
  + [cleanOutputBuffers](#cleanoutputbuffers)
  + [sendContentType](#sendcontenttype)
  + [sendCacheControl](#sendcachecontrol)
  + [sendLastModified](#sendlastmodified)
  + [sendEtag](#sendetag)
  + [sendGzip](#sendgzip)
  + [md5](#md5) 

<a name="rex_response"></a>

## Die Klasse rex_response

Die Klasse `rex_response` bietet Methoden für das Handling von

* Inhalte senden
* http(s) Statuscodes
* Redirects
* Outputbuffer

<a name="methoden"></a>

## Methoden

<a name="setstatus"></a>

#### setStatus

`setStatus($httpStatus)` 

Setzt den Statuscode. Beispiel: `rex_response::setStatus(rex_response::HTTP_OK)` .

<a name="getstatus"></a>

#### getStatus

`getStatus()` 

Gibt den aktuellen Statuscode zurück. Beispiel: `rex_response::getStatus()` .

<a name="sendredirect"></a>

#### sendRedirect

`sendRedirect($url)` 

Bewirkt einen Redirect auf die übergebene URL mit dem über die Methode `setStatus` gesetzten Statuscode. Die Ausführung von weiterem Code wird per `exit` beendet.

**Beispiel:**
Es soll ein Redirect mit dem Status `301` ausgeführt werden. Das kann z. B. im Template oder auch aus einem Modul heraus geschehen.

    <?php
    rex_response::setStatus(301);
    rex_response::sendRedirect(rex_getUrl(article_id));

**Erweitertes Beispiel:**
Es soll ein Redirect zu einer bestimmten Sprache (clang_id), mit URL-Parametern (param=foo) sowie einem Sprunganker (#anchor) ausgeführt werden.

    <?php
    rex_response::setStatus(301);
    rex_response::sendRedirect(rex_getUrl(article_id,clang_id,["param"=>"foo"],"&")."#anchor");

<a name="getstatus"></a>

#### getStatus

`getStatus()` 

Gibt den aktuellen Statuscode zurück. Beispiel: `rex_response::getStatus()` .

<a name="sendfile"></a>

#### sendFile

`sendFile($file, $contentType, $contentDisposition = 'inline')` 

Leert den Outputbuffer und prüft, ob die in `$file` übergebene Datei vorhanden ist.
Wenn die Datei nicht im Filesystem gefunden wurde, wird ein `HTTP_NOT_FOUND` Statuscode verschickt und die Ausführung per `exit` beendet.
Wenn die Datei gefunden wurde, wird standardmäßig ein `Cachecontrol Header` geschickt. Der Cachecontrol Header kann über die Methode `sendCacheControl` selbst gesetzt werden.
Wenn keine automatische Kompression verfügbar ist, wird der Header für `Content-Length` gesetzt, damit der Browser einen Ladebalken anzeigen kann.

<a name="sendresource"></a>

#### sendResource

`sendResource($content, $contentType = null, $lastModified = null, $etag = null, $contentDisposition = null, $filename = null)`, z.B.
`rex_response::sendResource($content, 'Content-Type: application/pdf', time(), null, 'attachment', "Meine PDF-Datei als Download.pdf");`

Verschickt eine Ressource über die Methoden `sendCacheControl` und `sendContent` .

<a name="sendpage"></a>

#### sendPage

`sendPage($content, $lastModified = null)` 

Verschickt den Inhalt von `$content` . Optional kann ein `Last Modified` -Wert als Timestamp übergeben werden. Der Inhalt von `$content` kann über den Extensionpoint OUTPUT_FILTER modifiziert werden.

<a name="sendcontent"></a>

#### sendContent

`sendContent($content, $contentType = null, $lastModified = null, $etag = null)` 

Verschickt den Inhalt von `$content` .

<a name="cleanoutputbuffer"></a>

#### cleanOutputBuffer

`cleanOutputBuffers()` 

Löscht alle Ausgabepuffer.

<a name="sendcontenttype"></a>

#### sendContentType

`sendContentType($contentType = null)` 

Verschickt einen Content-Type Header. Standard ist `text/html; charset=utf-8` .

<a name="sendcachecontrol"></a>

#### sendCacheControl

`sendCacheControl($cacheControl = 'must-revalidate, proxy-revalidate, private, no-cache, max-age=0')` 

Verschickt den Cache Control Header.

<a name="sendlastmodified"></a>

#### sendLastModified

`sendLastModified($lastModified = null)` 

Verschickt den Last Modified Header. Standard ist das aktuelle Datum und die aktuelle Uhrzeit. Wenn die Zeit identisch ist mit dem vom Browser übermittelten Wert `HTTP_IF_MODIFIED_SINCE` , wird der Ausgabepuffer verworfen und der Statuscode `NOT_MODIFIED` (304) übermittelt.

<a name="sendetag"></a>

#### sendEtag

`sendEtag($cacheKey)` 

Prüft, ob der Inhalt den ETAG Cache Schlüssel geändert hat.

<a name="sendgzip"></a>

#### sendGzip

`sendGzip($content)` 

Wenn der Browser Gzip/x-Gzip unterstützt, wird `$content` komprimiert übertragen.

<a name="md5"></a>

#### md5

`md5($content)` 

Erzeugt einen md5-Hash aus `$content` . Inhalt, der von `<!--DYN-->.*<!--/DYN-->` umschlossen ist, wird ignoriert.

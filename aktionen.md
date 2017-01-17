# Aktionen

Es gibt in der Standardkonfiguration von Redaxo drei Events bzw. Aktionen für Module die automatisch ausgeführt werden.

Aktion | Beschreibung
------------- | -------------
Preview	| Wird vor dem Anzeigen des Moduls ausgeführt.
Presave	| Wird vor dem Speichern des Moduls ausgeführt.
Postsave | Wird nach dem Speichern des Moduls ausgeführt.


## Aktion erstellen

Es ist wichtig die korrekte Aktion zu verwenden, Presave eignet sich sehr gut um Daten vor dem Speichervorgang zu Manipulieren. Postsave eignet sich um Daten nach dem Speichervorgang weiter zu verarbeiten.

### Auf Werte zugreifen

Normalerweise werden beispielsweise in Presave-Aktionen Werte überprüft bzw. verändert, die zuvor in einem Modulblock eingegeben wurden. Auf die entsprechenden Werte kann mit

    $text = $this->getValue(1);  // Beispiel für REX_VALUE[1]

zugegriffen werden.

Wenn die Werte in einer Presave-Aktion geändert werden, so können diese mit

    $this->setValue(1,$text); // Beispiel für REX_VALUE[1]

gespeichert werden.


## Beispiel einer kompletten Aktion

In diesem Beispiel wird eine Presave Aktion gezeigt. In dieser Aktion geht es darum, HTML Text aus Wysiwyg Editoren (z.B. Redactor, TinyMCE) zu prüfen und gegebenenfalls zu ändern.

Diesen Code ins Feld "Presave-Aktion" eintragen und den Events Add und Edit zuweisen

    <?php
    $text = $this->getValue(1);                        // REX_VALUE[1] auslesen
    $text = preg_replace('/ style=".*?"/', '', $text); // alle style="..." Stellen löschen
    $text = preg_replace('/<p>\s*<\/p>/', '', $text);  // alle leeren Absätze löschen
    $text = preg_replace('/ href="(.*?)#(.{1,30})"/', ' href="#$2"', $text); // alle Urls aus Ankerlinks löschen
    $text = preg_replace("/\r|\n|\r\n/", ' ', $text);    // Alle Zeilenumbrüche raus
    $this->setValue(1,$text);                            // ersetzten Text wieder in REX_VALUE[1] schreiben
    ?>

Die fertige Aktion dann dem Modul mit dem Wysywig Text zuweisen. Das Modul muss den Text für dieses Beispiel in die REX_VALUE[1] speichern.

  > **Hinweis:** 
Eine Aktion kann einem Modul erst zugewiesen werden, wenn das Modul gespeichert wurde. Es ist also nicht möglich, die Aktion direkt bei der Erstellung eines Moduls zuzuweisen. Die Auswahlmöglichkeit für die Zuweisung einer Aktion zu einem Modul erscheint erst, wenn das Modul bereits existiert.

Was noch fehlt:
Zugriff auf andere REX_VALUES (Media, Medialist, Link, Linklist)

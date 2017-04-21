# Medienkategorie vorselektieren#

Öffnet man den Medienpool über einen REX_MEDIA_BUTTON, startet die Ansicht meist in der Übersicht. Es ist aber auch möglich, den Medienpool in einer bestimmen Kategorie zu öffnen.

Der Aufruf mit einem REX_MEDIA_BUTTON in der gewohnten Art sieht so aus:

```HTML
<div class="rex-wdgt">
<div class="rex-wdgt-mda">
<p class="rex-wdgt-fld">
<input type="text" size="30" name="MEDIA[1]" value="" id="REX_MEDIA_1" readonly="readonly" />
</p>
<p class="rex-wdgt-icons">
<a href="#" onclick="openREXMedia(1,'');return false;" tabindex="14"><img src="media/file_open.gif" width="16" height="16" title="Medium auswählen" alt="Medium auswählen" /></a>
<a href="#" onclick="addREXMedia(1);return false;" tabindex="15"><img src="media/file_add.gif" width="16" height="16" title="Neues Medium hinzufügen" alt="Neues Medium hinzufügen" /></a>
<a href="#" onclick="deleteREXMedia(1);return false;" tabindex="16"><img src="media/file_del.gif" width="16" height="16" title="Ausgewähltes Medium löschen" alt="Ausgewähltes Medium löschen" /></a>
</p>
<div class="rex-clearer"></div>
</div>
</div>
```

Das gleiche Ergebnis in einer anderen Schreibweise:

```HTML
REX_MEDIA_BUTTON[id="1"]
```

Für das Öffnen der gewünschten Medienpool-Kategorie erweitert man die Angaben wie folgt:


```PHP 
REX_MEDIA_BUTTON[id="1" category="1"]
```


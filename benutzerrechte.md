# Benutzerrechte

In REDAXO werden die Nutzerrechte über Rollen definiert. Rollen sammeln die Berechtigungen die den Benutzern zugeteilt werden können.  Die zuständige Klasse findet man hier: [rex_perm](http://www.redaxo.org/docs/master/class-rex_perm.html)

## Definieren

Berechtigungen können in der Datei `package.yml` definiert werden, oder später im PHP-Code des AddOns.

### Package.yml

<<<<<<< HEAD
```yml
=======
``` 
>>>>>>> 7072b650176e504870baf1d0e0293b3f012a06d8
page:
 title: translate:title
 perm: addonname[]
 subpages:
  foo: {perm: addonname[foo], title: translate:foo}
  bar: {perm: addonname[bar], title: translate:bar}
```

### PHP

in PHP haben wir zusätzlich die Möglichkeit, die Berechtigungen in Gruppen einzuteilen. Ohne den dritten Parameter werden alle Berechtigungen in die Gruppe GENERAL gespeichert. Diese Berechtigungen erscheinen in den Rollen unter `Allgemein` . Dazu gibt es noch OPTIONS und EXTRAS. Diese Zusatzgruppen eigenen sich gut um die einzelnen Features eines AddOns freizugeben, wogegen GENERAL eher genutzt wird, um den Zugriff auf das AddOn/Plugin generell zu erlauben für diese Rolle.

<<<<<<< HEAD
```php
=======
``` 
>>>>>>> 7072b650176e504870baf1d0e0293b3f012a06d8
<?php

if(rex::isBackend() && is_object(rex::getUser())) {
  rex_perm::register('addonname[]', null);
  rex_perm::register('addonname[foo]', null, rex_perm::OPTIONS);
  rex_perm::register('addonname[bar]', null, rex_perm::OPTIONS);
}
```

Es empfiehlt sich zu prüfen, ob der Benutzer eingeloggt ist.

## Berechtigungen prüfen

### Ist Admin

Prüfen ob der User ein Admin ist `rex::getUser()->isAdmin()` 

### Einzelne Rechte prüfen

Prüfen ob der User die nötigen Rechte aktiviert hat:

<<<<<<< HEAD
```php
=======
``` 
>>>>>>> 7072b650176e504870baf1d0e0293b3f012a06d8
if( rex::getUser()->hasPerm('addonname[]') && rex::getUser()->hasPerm('addonname[foo]') ) {
 // code goes here
}
```

### Zugriff auf Module

Weitere Berechtigungen wie Module können wie folgt abgefragt werden:

<<<<<<< HEAD
```php
=======
``` 
>>>>>>> 7072b650176e504870baf1d0e0293b3f012a06d8
if( rex::getUser()->getComplexPerm('modules')->hasPerm($ModuleID) ) {
 // code goes here
}
```

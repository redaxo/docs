# Benutzerverwaltung

In der Benutzerverwaltung (Benutzer) werden die Redakteure und Administratoren des CMS gepflegt. Du kannst die einzelnen Nutzer mit verschiednenen Rollen versehen und diesen Rollen unterschiedliche Rechte zuweisen. 
Sofern du Administrator bist oder dir das entsprechende Recht erteilt wurde findest du die Benutzervaltung im Menüpunkt › ** Benutzer **. 

## Benutzerliste
Bei Aufruf der Benutzerverwaltung wird dir die Liste aller System-Benutzer aufgelistet.
Folgende Informationen zu den einzelen Benutzern werden aufgelistet: 
- ID
- Name
- Login
- Rolle
- letzter Login

Zum Bearbeiten eines Nutzers klickst du auf › ** editieren **.
Zum Löschen eines Nutzers klickst du auf › ** löschen **.
> Das Löschen des aktuell angemeldeten Nutzers (also deines eigenen Accounts) ist nicht möglich. 

## Rollen 
Redaxo verwendet Rollen-Definitionen um die Rechte einzelner Nutzer oder Gruppen festzulegen. Bevor du neue Benutzer anlegst, macht es Sinn, sich über deren Rechte Gedanken zu machen und entsprechende Rollen zu definieren. 
Redakteure benötigen meist einen Bruchteil der verfügbaren Berechtigungen.  Die Rollen können unter ***Benutzer -> Rollen*** erstellt und editiert werden. 

## Erstellen einer Rolle
Klicke im Reiter Rollen auf das Plus-Symbol um eine neue Rolle zu erstellen. 

### Allgemein

Allgemein bedeutet, der Benutzer bekommt generell Zugriff auf Addons bzw. Plugins. Es kann also sein, dass der Benutzer auf das Addon zugreifen können muss um eine Option nutzen zu können. Ein Beispiel: Ein Benutzer hat zugriff auf ein Addon und kann die Option Hilfe nutzen, aber nicht die Einstellung.

Eine Rollendefinition ist in mehrere Abschnitte unterteilt. 

### Optionen

Einige Addons bzw. Plugins haben mehrere Optionen. Diese können in dem Feld Optionen aktiviert werden.

### Extras
Hier werden weitere Berechtigungen angezeigt, die eventuell vorher definierte Rechte verfeinern. 


### Sprachen

Manche Benutzer dürfen nur auf bestimmte Sprachen zugreifen. Der Vorteil ist, dass sich diese Benutzer nicht über andere Sprachen Gedanken machen müssen, sondern lediglich über die zugeordnete. Das macht das Backend übersichtlicher und reduziert die Gefahr dass falsche Inhalte manipuliert werden.

### Kategorien

Hier legst Du fest auf welche Kategorien (Rubriken) der Redakteur Zugriff erhält. 


### Medienordner

Lege hier fest auf welche Medienpool-Kategorien der Benutzer eine Schreibberechtigung erhält. 
> Er besitzt weiterhin das Lese- und Nutzrecht für alle Medien, kann diese aber darüber hinaus nicht bearbeiten. 

### Module

Um das Backend für einige Benutzer noch einfacher bzw. übersichtlicher zu gestalten, kann der Zugriff auf wenige Module - oder auch Slices - beschränkt werden. Damit könnte man Benutzer, die lediglich News Pflegen können sollen, nur die News-Module freigeben.

## Anlegen eines Benutzers

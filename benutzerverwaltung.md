# Benutzerverwaltung

* [Einleitung](#einleitung)
* [Benutzerliste](#liste)
* [Rollen](#rollen)
* [Anlegen einer Rolle](#rollenerstellen)
  + [Beschreibung](#beschreibung)
  + [Allgemein](#rolleallgemein)
  + [Optionen](#rolleoptionen)
  + [Extras](#rolleextras)
  + [Sprachen](#rollesprachen)
  + [Kategorien](#rollekategorien)
  + [Medienordner](#rollemedienordner)
  + [Module](#rollemodule)
* [Anlegen eines Benutzers](#benutzer)

<a name="einleitung"></a>

## Einleitung

In der Benutzerverwaltung (Benutzer) werden die Redakteure und Administratoren des CMS gepflegt. Man kann die einzelnen Nutzer mit verschiedenen Rollen versehen und diesen Rollen unterschiedliche Rechte zuweisen. So muss man neuen Usern nur noch die entsprechende Rolle zuwiesen und nicht mehr alle Rechte definieren.

Administratoren oder User mit entsprechenden Rechten finden die Benutzverwaltung im Menüpunkt `Benutzer` .

<a name="liste"></a>

## Benutzerliste

![Systemcheck](/assets/v5.2.0-Benutzerverwaltung--liste.png)

Benutzerliste

Bei Aufruf der Benutzerverwaltung erscheint die Liste aller System-Benutzer.
Folgende Informationen zu den einzelnen Benutzern werden aufgelistet:

* ID
* Name
* Login
* Rolle
* letzter Login

Zum Bearbeiten eines Benutzers klickt man auf `editieren` , zum Löschen eines Benutzers klickst du auf `löschen` .

> Das Löschen des aktuell angemeldeten Nutzers (also der eigene Account) ist nicht möglich.

[Ein neuer Benutzer](#benutzer) wird erstellt durch Klick auf das Plus-Symbol.

<a name="rollen"></a>

## Rollen

REDAXO verwendet Rollen-Definitionen, um die Rechte einzelner Nutzer oder Gruppen festzulegen. Bevor man neue Benutzer anlegt, sollte man sich über deren Rechte Gedanken machen und entsprechende Rollen definieren.
Redakteure benötigen meist nur einen Bruchteil der verfügbaren Berechtigungen. Die Rollen können unter `Benutzer, Rollen` erstellt und editiert werden.

<a name="rollenerstellen"></a>

## Anlegen einer Rolle

Im Reiter `Rollen` klickt man auf das Plus-Symbol, um eine neue Rolle zu erstellen.
Eine Rollendefinition ist in mehrere Abschnitte unterteilt. Je nach installiertem AddOn können weitere Abschnitte hinzukommen. Nachfolgend werden die Standardabschnitte erklärt, die nach der Installation zur Verfügung stehen.

<a name="beschreibung"></a>

### Beschreibung

Eine Beschreibung für die Rolle kann verwendet werden, um gegebenenfalls anderen Administratoren zu erklären, für wen diese Rolle gedacht ist oder welche Einschränkungen man durchgeführt hast.

<a name="rolleallgemein"></a>

### Allgemein

Im Abschnitt `Allgemein` wird der generelle Zugriff auf ein AddOn oder PlugIn definiert. Es kann sein, dass der Benutzer auf das AddOn zugreifen können muss, um die für die Redaktion erforderlichen Funktionen zu nutzen. Er benötigt aber nicht die Funktionen zur Konfiguration des AddOns.

> Ein Beispiel: Ein Benutzer soll eine Tabelle eines Glossars pflegen, aber nicht die Struktur der Tabelle verändern dürfen.

<a name="rolleoptionen"></a>

### Optionen

Einige AddOns oder PlugIns haben mehrere zusätzliche Optionen. Diese können in dem Feld Optionen aktiviert werden.

<a name="rolleextras"></a>

### Extras

Hier werden weitere Berechtigungen angezeigt, die eventuell vorher definierte Rechte verfeinern.

<a name="rollesprachen"></a>

### Sprachen

Manche Benutzer sollen nur auf bestimmte Sprachen zugreifen dürfen. Der Vorteil ist, dass sich diese Benutzer nicht über andere Sprachen Gedanken machen müssen, sondern lediglich über die zugeordnete. Das macht das Backend übersichtlicher und reduziert die Gefahr, dass falsche Inhalte manipuliert werden.

<a name="rollekategorien"></a>

### Kategorien

Hier legt man fest, auf welche Kategorien (Rubriken) der Redakteur Zugriff erhält.

<a name="rollemedienordner"></a>

### Medienordner

Es kann definiert werden, für welche Medienpool-Kategorien der Benutzer eine Schreibberechtigung erhält.

> **Hinweis:** Er besitzt weiterhin das Lese- und Nutzrecht für alle Medien, kann diese aber nicht bearbeiten.

<a name="rollemodule"></a>

### Module

Um das Backend für einige Benutzer noch einfacher, bzw. übersichtlicher zu gestalten, kann der Zugriff auf wenige Module beschränkt werden. Damit könnte man beispielsweise Benutzern, die lediglich News Pflegen können sollen, nur die News-Module freigeben.

<a name="benutzer"></a>

## Anlegen eines Benutzers

Einen neuen Benutzer legt man an, idem man auf das Plus-Symbol in der Benutzerliste klickt.

![Systemcheck](/assets/v5.2.0-Benutzerverwaltung--benutzer.png)

Benutzer anlegen

Man kann folgende Einstellungen festlegen:

* Benutzername
* Passwort (*kann durch den Nutzer im Profil geändert werden*)
* Name
* Beschreibung (z. B. Chefredakteur)
* E-Mail-Adresse (wird eventuell von einigen AddOns benötigt)
* [Admin](#qdmin)
* User ist aktiv
* [Rolle](#rollen)
* [Startseite](#startseite)
* Backendsprache

<a name="admin"></a>

## Admin

Der Admin erhält alle Rechte und Zugriff auf alle System- und AddOn-Funktionen.

> Um Fehlbedienungen zu vermeiden sollten Redakteure geeignete Rechte über eine Rolle erhalten.

<a name="startseite"></a>

## Startseite

Hier legt man fest, welche Seite direkt nach dem Login im Backend aufgerufen werden soll, der Standard ist `Struktur` .

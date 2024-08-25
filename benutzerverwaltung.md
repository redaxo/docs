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

In der Benutzerverwaltung (Benutzer) werden die Redakteure und Administratoren des CMS gepflegt. Nutzer können mit verschiedenen Rollen versehen werden und diesen Rollen können wiederum unterschiedliche Rechte zugewiesen werden. So muss neuen Nutzern nur noch die entsprechende Rolle zugewiesen und nicht alle Rechte einzeln definiert werden.

Administratoren oder Nutzer mit entsprechenden Rechten finden die Benutzerverwaltung im Menüpunkt `Benutzer`.

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

Unter Funktionen besteht die Möglichkeit die Benutzerdaten zu `editieren` und Benutzer zu `löschen`. 
Administratoren haben hier zudem die Möglichkeit, die aktuelle Ansicht eines Benutzers zu testen, ohne sich ab- und wieder anmelden zu müssen, in dem sie die Funktion `Identität wechseln` verwenden. 
Nach dem Wechsel erscheint rechts oben ein Link zum `zurückwechseln` in den Administratormodus.

> Das Löschen des aktuell angemeldeten Nutzers (also der eigene Account) ist nicht möglich.

[Ein neuer Benutzer](#benutzer) lässt sich durch Klick auf das Plus-Symbol erstellen.

<a name="rollen"></a>

## Rollen

REDAXO verwendet Rollen-Definitionen, um die Rechte einzelner Nutzer oder Gruppen festzulegen. Bevor neue Benutzer angelegt werden, sollten die notwendigen Rechte in einer entsprechenden Rolle definiert sein.
Redakteure benötigen meist nur einen Bruchteil der verfügbaren Berechtigungen.

<a name="rollenerstellen"></a>

## Anlegen einer Rolle

Im Reiter `Rollen` lassen sich neue Rollen durch Klick auf das Plus-Symbol erstellen.
Eine Rollen-Definition ist in mehrere Abschnitte unterteilt. Je nach installiertem AddOn können weitere Abschnitte hinzukommen. Nachfolgend werden die Standardabschnitte erklärt, die nach der Installation zur Verfügung stehen.

<a name="beschreibung"></a>

### Beschreibung

Eine Beschreibung für die Rolle kann verwendet werden, um gegebenenfalls anderen Administratoren zu erklären, für wen diese Rolle gedacht ist oder welche Berechtigungen/Einschränkungen damit verbunden sind.

<a name="rolleallgemein"></a>

### Allgemein

Im Abschnitt `Allgemein` wird der generelle Zugriff auf ein AddOn oder PlugIn definiert. Es kann sein, dass der Benutzer auf das AddOn zugreifen können muss, um die für die Redaktion erforderlichen Funktionen zu nutzen. Er benötigt aber nicht die Funktionen zur Konfiguration des AddOns.

> Ein Beispiel: Ein Benutzer soll eine Tabelle eines Glossars pflegen, aber nicht die Struktur der Tabelle verändern dürfen.

<a name="rolleoptionen"></a>

### Optionen

Einige AddOns oder PlugIns haben zusätzliche Optionen. Diese können in dem Feld Optionen aktiviert werden.

Hier finden sich u.a. auch Rechte zur Einschränkung der Strukturbearbeitung

- `addArticle[]` Artikel erstellen
- `editArticle[]` Artikel bearbeiten
- `deleteArticle[]` Artikel löschen
- `addCategory[]` Kategorien erstellen
- `editCategory[]` Kategorie bearbeiten
- `deleteCategory[]` Kategorie löschen 


<a name="rolleextras"></a>

### Extras

Hier werden weitere Berechtigungen angezeigt, die eventuell vorher definierte Rechte verfeinern.

<a name="rollesprachen"></a>

### Sprachen

Manche Benutzer sollen nur auf bestimmte Sprachen zugreifen dürfen. Der Vorteil ist, dass sich diese Benutzer nicht über andere Sprachen Gedanken machen müssen, sondern lediglich über die zugeordnete. Das macht das Backend übersichtlicher und reduziert die Gefahr, dass falsche Inhalte manipuliert werden.

<a name="rollekategorien"></a>

### Kategorien

Hier kann festgelegt werden, auf welche Kategorien (Rubriken) der Redakteur Zugriff erhält.

<a name="rollemedienordner"></a>

### Medienordner

Es kann definiert werden, für welche Medienpool-Kategorien der Benutzer eine Schreibberechtigung erhält.

> **Hinweis:** Der Benutzer besitzt weiterhin das Lese- und Nutzrecht für alle Medien, kann diese aber nicht bearbeiten.

<a name="rollemodule"></a>

### Module

Um das Backend für einige Benutzer noch einfacher bzw. übersichtlicher zu gestalten, kann der Zugriff auf wenige Module beschränkt werden. Damit könnte beispielsweise Benutzern, die lediglich eine Kategorie *Neuigkeiten* pflegen können sollen, nur die dafür benötigten Module freigeben werden.

<a name="benutzer"></a>

## Anlegen eines Benutzers

Ein neuer Benutzer lässt sich durch Klick auf das Plus-Symbol erstellen.

![Systemcheck](/assets/v5.2.0-Benutzerverwaltung--benutzer.png)

Benutzer anlegen

Folgende Einstellungen können festlegt werden:

* Benutzername
* Passwort (*kann durch den Nutzer im Profil geändert werden*)
* Name
* Beschreibung (z. B. Chefredakteur)
* E-Mail-Adresse (wird eventuell von einigen AddOns benötigt)
* [Admin](#admin)
* User ist aktiv
* [Rolle](#rollen)
* [Startseite](#startseite)
* Backendsprache

<a name="admin"></a>

## Admin

Der Admin erhält alle Rechte und Zugriff auf alle System- und AddOn-Funktionen.

> Um Fehlbedienungen zu vermeiden, sollten Redakteure geeignete Rechte über eine Rolle erhalten.

<a name="startseite"></a>

## Startseite

Hier wird festgelegt, welche Seite direkt nach dem Login im Backend aufgerufen werden soll. Der Standard (Default) ist `Struktur`.

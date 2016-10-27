# Strukturverwaltung

Die Strukturverwaltung ist der zentrale Teil der Websiteverwaltung, sie stellt die Übersicht der Inhalte dar und dient derer Verwaltung.

Die Navigationsstruktur ist hierarchisch eingeteilt. Es gibt Kategorien und Artikel. Artikel werden in den verschiedenen Kategorien sortiert. In der jeweiligen Kategorie sind verschiedene Artikel (meist lediglich ein Startartikel). Jeder Artikel besteht wiederum aus verschiedenen Blöcken (Slices).

Zum Verständnis: Man kann sich für dieses Beispiel durchaus die Internetseite mit einem Buch vergleichen: Der Umschlag und Schriftart ist von jemanden festgelegt. Die Struktur ist eingeteilt in Kapitel (= Kategorien) jedes Kapitel kann aus mehrere Seiten bestehen (= Artikel). Meistens hat ein Kapitel jedoch nur eine Seite (= Startartikel). Jeder Artikel besteht aus mehreren Absätzen (= Blöcken/Slices).

Kategorien und Artikel erhalten stets einen Namen. Mit der Priorität wird die Reihenfolge bestimmt, in der die Kategorie oder der Artikel angezeigt werden. Dies gilt auch für das Frontend. Der Status zeigt an, ob das Element online – also sichtbar oder offline – also nicht sichtbar ist. In Einzelfällen kann es vorkommen, dass Redaxo von den Entwicklern anders konfiguriert wurde. Dann hat online/offline keine oder eine andere Funktion. Über editieren und löschen können Sie den Artikel / die Kategorie verändern (Name und Priorität) oder ganz entfernen. Eine Kategorie kann jedoch nur gelöscht werden, wenn Sie keine Artikel außer dem Startartikel enthält.

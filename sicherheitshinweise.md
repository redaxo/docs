# Sicherheitshinweise

> **Eine Bitte an unsere Community**
> 
> Wenn Sie eine Sicherheitslücke feststellen, melden Sie sie bitte umgehend dem REDAXO-Team (info@redaxo.de).
Wir werden dann sofort Gegenmaßnahmen ergreifen.
> Stellen Sie diese Information nach Möglichkeit nicht ins Forum. Dies könnte sonst den Spieltrieb von Leuten wecken, die solche Lücken gerne mal für ihre Zwecke missbrauchen.


Um es gleich vorwegzunehmen: Absolute Sicherheit gibt es nicht. Man kann nur eine Reihe von Maßnahmen ergreifen, um potenziellen Angreifern das Leben möglichst schwer zu machen.

Für eine REDAXO-Installation ist es wichtig, dass der redaxo/include-Ordner vor Zugriff von außen geschützt wird. Wir haben standardmäßig eine .htaccess-Datei eingebaut, so dass ein Apache-Server im Normalfall keinen Zugriff auf die Dateien im Include-Ordner erlaubt.

Bei der Version 4.x wurde eine Überprüfung der .htaccess-Datei eingebaut. Sollte sie nicht vorliegen, erhält man bei der Installation eine Warnmeldung.

Bei anderen Serverarten funktioniert dieser Schutz nicht und man muss dies entsprechend der Servermöglichkeiten selbst einstellen.
Allgemein: Der Zugriff auf den include Ordner muss so gesperrt werden, dass man über die Webseite nicht darauf zugreifen kann!

Wir gehen hier nicht auf allgemeine Sicherheitvorkehrungen ein, die bei der PHP-Programmierung oder bei den Servereinstellungen beachtet werden sollten. Dies würde den Rahmen unserer REDAXO-Doku sprengen. Hier verweisen wir auf entsprechende Literatur zu diesem Thema.

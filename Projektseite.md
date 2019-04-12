# Informatikprojekt: Jump and Run in Greenfoot
## Inhaltsverzeichnis
### 1. Einführung
### 2. Code
####  2.1 World
* 2.1.1 Startscreen
    * 2.1.2 Level
      * Level 1
      * Level 2
      * Level 3
   * 2.1.2 End Screen
      * GameOver
   * 2.1.3 Scrolling
 
 ####  2.2 Actor
 * 2.2.1 Objekte
      * Zwei Blockvarianten
      * Beweg. Plattform
      * Gegenspieler
      * Übergangsobjekt
      * Designobjekt 
      
 * 2.2.2 Protagonist
      * Bewegungsprinzip
        * Interaktionen
      * Kostüm
        * Animation
      
  ### 3. Fazit
<hr>

### 1.Einführung
#### Vorwort

Im folgenden findet sich eine konkrete Dokumentation zum Code des Projekts. Dieser Text zielt darauf die Umsetzung bzw. Gestaltung der Projektidee zu vermitteln.Das Verfahren wird, je nach Komplexität des Codes, in der Detailtreue variiert.

Anzumerken ist, dass das Programm sich noch in der Weiterentwicklung befindet. Daher folgt eine teils "unschöne" Form, bspw. durch zwei Schrägstriche `//` deaktivierter Code. Dies wird im nötigen Fall kommentiert, generell sind meine Notizen im Code einfach zu überlesen.
#### Codeumgebung
Greenfoot ist eine java-basierte, für Studienzwecke möglichst interaktiv gestaltete, Entwicklungsplattform. Durch die vordefinierten Klassen wie bspw. World oder Actor ist die spätere Einbindung von Objekten in die graphische Oberfläche um einiges erleichtert.
#### Projektidee
Meine Projektidee ist ein klassisches "Jump and Run"-Spiel. Die Thematik hat sich im Verlauf der Arbeit ergeben. Man spielt eine 2dimensionale Figur, welche durch unterschiedliche Welten - im Sinne der klassischen J&R-Vorstellung-zu bewegen ist. 
<hr>

### 2.Code
Der Code wird (grob formuliert) von außen nach innen betrachtet, bei späterer Betrachtung des `Protagonisten` sei dessen Umgebung bereits erklärt.
### 2.1 World
Ähnlichkeiten der einzelnen Welten sind: Alle vorkommenden Objekte werden vorher, durch Angabe der Koordinaten einzeln definiert. 
#### 2.1.1 Startscreen
Als Beginn des Spiels befindet sich hier der Titel, eine kurzes Tutorial und der Start-Button um das Spiel beginnen zu können.
Bisher ist der Code begrenzt auf einfache `addObject-Funktionen`, um dies zu vereinfachen sind manche Dinge durch Variablensetzung abgekürzt.
#### 2.1.2 Level
Diese Welt ist selbst nicht begehbar, stellt jedoch die höhere Klasse für alle anderen Level dar. Auf Grund des Hintergrundkonzepts (genauer 2.2.1 Designobjekt), waren mehrere Bilder pro Level nötig. Um Zeit zu sparen sind allgemein benötigte Zeilen bereits hier definiert (die untereren Klassen erweitern die Level-Klasse und übernehmen daher `public-Blöcke`). Die `Scrolling-Funktion` ist aktuell (zumindest in x-Richtung) deaktiviert.
##### Level 1,2 und 3
Hier sind die Objekte für diesen Bildschirm definiert. Dies ist ebenfalls bei Level 2 und 3 der Fall. Eine Besonderheit bei Level 3 ist, dass diese keine! Unterklasse von `Level` ist. Da es zwei Skalierungen gibt, in x- und y-Richtung gibt, war die Trennung auf diese Weise am effektivsten. Ansonsten wären die vordefinierten "Listen" (z.B. `public void generateWorld(img0, img1, img2)` nicht immer erfüllt gewesen). 
#### 2.1.2 Endscreen und GameOver
Der Endscreen, sowie der Gameover-Screen hat, wie alle Welten, min. ein richtig skaliertes Bild auf (in meinem Fall `1200,700,1`). Außerdem gibt es die Möglichkeit bei Gameover durch Klicken auf ein Textobjekt das Spiel neu zu starten. Der Code für diesen Übergang befindet sich allerdings in der Actorklasse dieses Objekts.
#### 2.1.3 Scrolling
Nun genauer zu der Scrollingfunktion. Diese funkioniert so, dass zuerst ein Bild in der Mitte der Welt, sowie eines am rechten Rand eingefügt wird. Über die untenstehende Funktion, wird der Ort des Bildes definiert und das passende Bild angesteuert. Dieses wird dann über die vorher definierte Funktion `scroll()` bewegt. Anfänglich war die Idee, dass bei seitlicher Bewegung der Figur auch der Hintergrund mitbewegt wird. Leider sah dies nicht so gut wie erwartet aus, daher habe ich den Bewegungswert in x-Richtung auf 0 gesetzt. Das Scrolling ist in beide Richtungen programmiert, ich habe jedoch eine Variabel für den Bewegungswert in x und y-Richtung erstellt, diese lässt sich schnell (falls doch benötigt) ändern. Aktuell soll eine scrollender Hintergrund bei Level 3 in das noch nicht programmierte Zusatzlevel führen. 

### 2.2 Actor
Als Actor sind nicht nur stationäre Objekte definiert, sondern auch die Hauptspielfigur, sowie die Hintergrundbilder -dies war für die Scrollfunktion nötig.
#### 2.2.1 Objekte
Zuerst werden alle Objekte beschrieben.
#### Zwei Blockvarianten
Im Spiel habe ich hauptsächlich zwei Blockarten verwendet. Beide haben ein thematisch passendes Bild sind jedoch unterschiedlich groß (Skalierung durch Funktion). Block1 ist für kleinere Flächen da und kann sehr gut kombiniert werden, die Größe ist `40x40`. Block2 dagegen dient eher der Untergrundgestaltung. Beide sind als `intersectingObj.` festgelegt, daher kann die Spielfigur auf diesen stehen. Die Transparenzfunktion in Block1 habe ich aus einem Javaforum, hat bisher jedoch noch keinen Einsatz gefunden. Die meisten Bilder, welche später z.B. die Textur eines Blocks darstellen habe ich mit Photoshop ausgeschnitten. Beim Verwenden eines solchen bearbeiteten Bildes mit transparenten Flächen ist jedoch zu bedenken, dass man im `.png-Format` speichert. Bei jpeg, werden die transparenten Bereiche automatisch weiß.
#### Bewegliche Plafformen
Ein Jump and Rum ohne bewegliche Plattformen ist nahezu undenkbar, daher gibt es diese auch bei mir. Die Funktion funktioniert so, dass zu Beginn die movingRight korrekt ist. Die Plattform bewegt sich dann im definierten Bereich der Variabeln (`intXa undXb`) auf der horizontalen Achse hin und her. Wenn bspw. das festgelegt Maximum einer X-Koordinate überschritten wurde, wird die `else` Klammer ausgefürt. Die Bewegung der Plattform funkionert (wie bei meiner Spielfigur) durch setLocation, in der benötigten Richtung wird dann (in diesem Fall) je 1 add- bzw. subtrahiert.
#### Gegenspieler
Bisher ist der "Gegenspieler" nur ein einzelner Fliegenpilz, dieser wird auf einer Plattform mitbewegt. Da jedoch die Actors unabhängig voneinander sind, hat der Pilz die gleiche Bewegungsfunktion wie die Plattform auf der er sich befindet. Für eine perfekte Ausführung dieser "gemeinsamen" Bewegung müsste eig. die größere Länge der Plattform im Vergleich zum Pilz einberechnet werden. Dies habe ich jedoch bewusst ausgelassen, da sich der Pilz so bei einem Richtungswechsel auf der Plattform verschiebt. (und somit interessanter wird)
Da das Spiel noch nicht fertig ist, sind noch weitere Gegner und Interaktionen geplant. (Bisher war dies zeitlich jedoch schwer, da dies mein erstes GF-Projekt ist und ich mich neu einarbeiten musste.)
#### Übergangsobjekt
Dieses Objekt, in Form eines Fasses, dient der Verbindung zwischen den einzelnen Welten. Wenn die Spielfigur das Fass berührt wird eine neue Welt erstellt. In dieser bestehen dann die vorher definierten Objekte. Funktionen wie `iftouching` waren sehr leicht zu finden und umzusetzen, da man mit strg+Leertaste ein Fenster öffnen kann um sich `completions` anzeigen zu lassen (diese sind außerdem erklärt). 
#### Designobjekt
Das Designobjekt steht für die vielen einzelnen Actors als Unterklassen vom Actor Hintergrund. Um die 2dimensionale Welt etwas interessanter zu gestalten, wird die Spielfigur von manchen Dingen überdeckt. Dies funktioniert, indem ich vom jeweiligen Bildhintergrund die vorderen Pflanzen ausgeschnitten und das gesamte Bild so gespeichert habe, dass nur diese übrig sind. Nun ist das bearbeitete Bild an der gleichen Stelle wie sein Original einzufügen. Mit der Funktion setPaintOrder (umso weiter links desto weiter oben) ließ sich nun genau einstellen welche Bilder im Vor- oder Hintergrund sein sollen. Beim Scrollen einer Welt ist natürlich an diese Ausschnitte mitzudenken, außerdem müssen alle Objekt in der `PaintOrder` erwähnt werden, sonst sind diese nicht sichtbar. Falls man eine unsichtbare Plattform erzeugen möchte ist dies vllt. eine unkonventionelle/einfachere Möglichkeit.
### 2.2.2 Protagonist
Der Programmiercode für diesen `Actor` war insgesamt wesentlich komplizierter im Vergleich zu den vorherigen. Oft war die Lösung bei der Fehlersuche jedoch auch ein kleiner unnötiger Fehler. 
### Bewegungsprinzip
Zu Beginn der Klasse sind alle Variabeln definiert, darunter z.B. die für eine Bewegung in x-Richtung, ebenso die `boolean`-Funktion um zu testen ob etwas Bestimmtes `true`oder `false` ist. Dies ist sehr nützlich um spätere Änderungen vorzunehmen. 
Über die `checkKeys() Method` wird erkannt, ob die für die Bewegung (bei der `if-Schleife`festgelegte Taste) gedrückt ist. Falls ja, wird die Spielfigur mit Hilfe von `setLocation` um die gewünschte `Geschwindigkeit` bewegt. Außerdem wird `jump()`ausgeführt, falls `"space"`gedrückt wird. Wenn sich die Spielfigur in der Luftbefindet, also `jump=true`gilt, wird `fall()`ausgeführt.
### Interaktionen
Das Springen soll nur vom Boden aus funktionieren, daher wird nur bei`if(gtotal()`ist ungleich 0 die `Geschwindigkeit_v` angewandt. Dies basiert darauf, dass in `List<Block>` `g=...` mit der jeweiligen Klasse und der Methode `getObjectsAt()`durch Kontakt mit dem Objekt ein Wert größer als Null entsteht.
Außerdem wird `jump=true`gestellt.
Damit sich der Protagonist über einem Objekt befinden kann, ohne weiter zu fallen, wird `groundlist`verwendet. Die einzelnen Objekte, die als Untergrund dienen sollen müssen daher in `List<Objekt> etc.`definiert werden.
Falls die Spielfigur in eine "Abgrund" -also aus der Welt hinaus fällt- soll der GameOver-Screen erscheinen, daher `if()` und `setWorld`. 
### Kostüm
Als Skin für die Spielfigur verwende ich eine Gif-Datei, wenn die Figur nicht läuft wird nur ein Screenshot aus der Animation verwendet.
### Animation
Der Code für die Gif-Funktion geht aktuell nicht und ich konnte den Fehler nicht finden. Mit der folgenden Codeidee hat die Animation bereits funktioniert, daher sollte der theoretische Gedanke richtig sein. Das `GifImage`wird zu Beginn (direkt unter den Variabeln) definiert. Danach wird das Bild in `public Protagonist()`skaliert und ein `new GifImage` durch Kombination mit der gerade genannten Definition erstellt (auch gespiegelt). Dennoch ist das `gif`pausiert, schließlich soll die Animation im Stand nicht laufen. In der `act()`ist zu Beginn `mirror=false`und `moving=false`. Die folgende If-Schleife unterscheidt und fügt später die richtig gespiegelte Version als Bild ein. Wenn z.B. "a" gedrückt wird bewegt sich die Spielfigur nach links, daher ist `moving`=true und `mirror` nun ebenfalls. Wenn das gif nicht läuft und "a" gedrückt wird, soll es starten(`gif.resume`).Ein Ausrufezeichen vor dem Gleichzeichen macht dies zu einem Ungleich. Während des Springens soll die `Gif-Datei` natürlich pausieren. 


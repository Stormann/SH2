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

Anzumerken ist, dass das Programm sich noch in der Weiterentwicklung befindet. Daher folgt eine teils "unschöne" Form, bspw. durch zwei Schrägstriche (//) deaktivierter Code. Dies wird im nötigen Fall kommentiert, generell sind meine Notizen im Code einfach zu überlesen.
#### Codeumgebung
Greenfoot ist eine java-basierte, für Studienzwecke möglichst interaktiv gestaltete, Entwicklungsplattform. Durch die vordefinierten Klassen wie bspw. World oder Actor ist die spätere Einbindung von Objekten in die graphische Oberfläche um einiges erleichtert.
#### Projektidee
Meine Projektidee ist ein klassisches "Jump and Run"-Spiel. Die Thematik hat sich im Verlauf der Arbeit ergeben. Man spielt eine 2dimensionale Figur, welche durch unterschiedliche Welten - im Sinne der klassischen J&R-Vorstellung-zu bewegen ist. 
<hr>

### 2.Code
Der Code wird (grob formuliert) von außen nach innen betrachtet, bei späterer Betrachtung des Protagonisten sei dessen Umgebung bereits erklärt.
### 2.1 World
Ähnlichkeiten der einzelnen Welten sind: Alle vorkommenden Objekte werden vorher, durch Angabe der Koordinaten einzeln definiert. 
#### 2.1.1 Startscreen
Als Beginn des Spiels befindet sich hier der Titel, eine kurzes Tutorial und der Start-Button um das Spiel beginnen zu können.
Bisher ist der Code begrenzt auf einfache "addObject"-Funktionen, um dies zu vereinfachen sind manche Dinge durch Variablensetzung abgekürzt.
#### 2.1.2 Level
Diese Welt ist selbst nicht begehbar, stellt jedoch die höhere Klasse für alle anderen Level dar. Auf Grund des Hintergrundkonzepts (genauer 2.2.1 Designobjekt), waren mehrere Bilder pro Level nötig. Um Zeit zu sparen sind allgemein benötigte Zeilen bereits hier definiert (die untereren Klassen erweitern die Level-Klasse und übernehmen daher "public"-Blöcke). Die Scrolling-Funktion ist aktuell (zumindest in x-Richtung) deaktiviert.
##### Level 1,2 und 3
Hier sind die Objekte für diesen Bildschirm definiert. Dies ist ebenfalls bei Level 2 und 3 der Fall. Eine Besonderheit bei Level 3 ist, dass diese keine! Unterklasse von "Level" ist. Da es zwei Skalierungen gibt, in x- und y-Richtung gibt, war die Trennung auf diese Weise am effektivsten. Ansonsten wären die vordefinierten "Listen" (z.B. public void generateWorld(img0, img1, img2) nicht immer erfüllt gewesen). 
#### 2.1.2 Endscreen und GameOver
Der Endscreen, sowie der Gameover-Screen hat, wie alle Welten, min. ein richtig skaliertes Bild auf (in meinem Fall 1200,700,1). Außerdem gibt es die Möglichkeit bei Gameover durch Klicken auf ein Textobjekt das Spiel neu zu starten. Der Code für diesen Übergang befindet sich allerdings in der Actorklasse dieses Objekts.
#### 2.1.3 Scrolling
Nun genauer zu der Scrollingfunktion. Diese funkioniert so, dass zuerst ein Bild in der Mitte der Welt, sowie eines am rechten Rand eingefügt wird. Über die untenstehende Funktion, wird der Ort des Bildes definiert und das passende Bild angesteuert. Dieses wird dann über die vorher definierte Funktion "scroll()" bewegt. Anfänglich war die Idee, dass bei seitlicher Bewegung der Figur auch der Hintergrund mitbewegt wird. Leider sah dies nicht so gut wie erwartet aus, daher habe ich den Bewegungswert in x-Richtung auf 0 gesetzt. Das Scrolling ist in beide Richtungen programmiert, ich habe jedoch eine Variabel für den Bewegungswert in x und y-Richtung erstellt, diese lässt sich schnell (falls doch benötigt) ändern. Aktuell soll eine scrollender Hintergrund bei Level 3 in das noch nicht programmierte Zusatzlevel führen. 

### Actor

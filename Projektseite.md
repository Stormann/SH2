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
#### 2.1 World
Ähnlichkeiten der einzelnen Welten sind: Alle vorkommenden Objekte werden vorher, durch Angabe der Koordinaten einzeln definiert. 
##### 2.1.1 Startscreen
Als Beginn des Spiels befindet sich hier der Titel, eine kurzes Tutorial und der Start-Button um das Spiel beginnen zu können.
Bisher ist der Code begrenzt auf einfache "addObject"-Funktionen, um dies zu vereinfachen sind manche Dinge durch Variablensetzung abgekürzt.

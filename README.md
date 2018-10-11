# Javascript

## MD Formatierungsregeln
[Link](http://agea.github.io/tutorial.md/)

## Visual Studio code
* Live Server als Extension installieren

## Git Hub <https://www.theregister.co.uk/2015/12/07/visual_studio_code_git_integration/>
* auf git hub ein neues Repository anlegen
* https Link kopieren
* Laufwerk/Order im Explorer öffnen in der das Repository lokal abgelegt werden soll
### Git Bash
* mit Rechtsklick git bash öffnen
* git config --global user.name "username"
* git config --global user.email "eMail@host"
* Repository nach lokal kopieren:
    * git clone  https://github.com/grisham88/Javascript.git
### Visual Studio Code
* Den neuen Ordner öffnen
* mit Rechtsklick "Open with Code"
* Nun ist das Repository mit git verknüpft und alle Änderungen sind direkt commit und pushbar 
    * Über die Source control (Link in Visual Studio Code) sieht man alle offenen Dateien die geändert wurden
    * Mit Button "V" können diese direkt commited werden oder einzeln zum Commit freigegeben werden
    * Beim ... kann dann push ausgeführt werden -> Git wird nach Git Hub aktualisiert

## Kursinhalt
### Javascript Variablen
* wird kein Wert zugewiesen ist der Typ des Objects undefined
* wird ein Wert zugewiesen, wird durch die Wertzuweisung der Typ definiert
#### Types
    var a = null; -> object
    var a = undefined; -> undefined
#### primitive Typen
    var a = 1.5; -> Number
    var a = true; -> bool
    var a = 'Test'; -> string
#### komplexe Typen
    var a = ['Rosen','Tulpen','Nelken'];
    var a = { x: "X", y: "Y", z: 'Z' };
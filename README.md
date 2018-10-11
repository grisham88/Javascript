# JavaScript Seminar


## Markdown (.md) Formatierungsregeln
* [Markdown Tutorial Git](http://agea.github.io/tutorial.md/)
* [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)


## Visual Studio code
* Live Server als Extension installieren
** mit ALT + L + O wird der Server gestartet und die aktuelle Webseite geöffnet und bei jedem Speichern aktualisiert im Browser
* Formatierung des Texts mit ALT + Shift + F
* Zeilenumbruch aktivieren mit ALT + Z

## Git Hub
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
* [Visual Studio Code: How to integrate Git](https://www.theregister.co.uk/2015/12/07/visual_studio_code_git_integration/)
* Den neuen Ordner öffnen
* mit Rechtsklick "Open with Code"
* Nun ist das Repository mit git verknüpft und alle Änderungen sind direkt commit und pushbar 
    * Über die Source control (Link in Visual Studio Code) sieht man alle offenen Dateien die geändert wurden
    * Mit Button "V" können diese direkt commited werden oder einzeln zum Commit freigegeben werden
    * Beim ... kann dann push ausgeführt werden -> Git wird nach Git Hub aktualisiert


## Kursinhalt JavaScript

### Variablen & Typen
* wird kein Wert zugewiesen ist der Typ des Objects undefined
* wird ein Wert zugewiesen, wird durch die Wertzuweisung der Typ definiert

#### Types
```javascript
var a = null; -> object
var a = undefined; -> undefined
```

#### Primitive Typen
```javascript
var a = 1.5;    //Number
var a = true;   //bool
var a = 'Test'; //string
```

#### Komplexe Typen
```javascript
var a = ['Rosen','Tulpen','Nelken'];
var a = { x: "X", y: "Y", z: 'Z' };
var a = function () {
            //tut nix
        };
```
        
#### Definition von Zuständen ob eine Variable als gefüllt gilt
```javascript
//Variablen auf TRUE prüfen
var a;
a = undefined;  // FALSE
a = null;       // FALSE

a = true;       // TRUE
a = false;      // FALSE

a = -42;        // TRUE
a = 0;          // FALSE
a = NaN;        // TRUE

a = 'String'    // TRUE
a = '';         // FALSE

a = [1, 2, 3];  // TRUE    
a = []          // TRUE !!!

a = { x: "X" }; // TRUE
a = {};         // TRUE !!
    
a = function () { } //TRUE

//Variablen auf FALSE prüfen
a = false;      //false... ok
//FALSY Übersicht
a = undefined;  // nope
a = null;       // nope
a = NaN;        // nope
a = 0;          // oops...
a = '';         // oops...
    
//Typsicherer und Wert-Vergleich (===) > Wertgleich wird mit == verglichen
if (a === false) {
     console.log('a:', a, 'ist FALSE mit Typ', typeof a)
}
else {
     console.log('a:', a, 'ist nicht FALSE mit Typ', typeof a)
}

if (42 === '42') {
     console.log("42 ist gleich '42'")
}
 else {
     console.log("42 ist NICHT gleich '42'")
}
```

> HINWEIS
> Vermutlich werden alle Defaultzustände wenn man weiß welcher Typ die Variable hat, als FALSE empfunden

### Functions
#### Function
> Ausgabe gibt bei beiden Aufrufen die 2.te Deklaration aus.
> HOISTING bewirkt, dass Variablen und Funktionen egal an welcher Stelle sie deklariert wurden in der Ausführung am Anfang stehen.
> Wird eine Function mit gleichem Namen deklariert, besteht in der Laufzeit immer nur die letzte Deklaration

> Der Code selbst wird dann liner abgearbeitet wobei Variablen immer zuerst deklariert sind und Funktionen global bereit stehen.

##### Globale Funktionen
```javascript
var x;
//1. Deklaration der Funktion
function beispiel() {
    console.log("Das ist ein Beispiel");
}

//Aufruf der Funktion
beispiel();

//2. Deklaration der Funktion
function beispiel() {
    console.log("Das ist ein ANDERES Beispiel");
}

//Erneuter Aufruf der Funktion
beispiel();
```

##### Funktionen in Variable speichern
```javascript
var x, beispiel;

// linearer Ablauf:

if (x) { // klappt nicht, da die Zuweisung erst später passiert
    console.log('Bin ich ein Error?')
} else {
    console.log('...oder nicht?')
}

// Variable wird initialisiert
x = "X";

// 1. Function-Statement
beispiel = function () {
    console.log("Das ist ein Beispiel.");
};
// 1. Aufruf
beispiel();

/*
ACHTUNG
Funktion wird gekapselt und das Ergebnis ausgegeben
*/

// 2. Function-Statement
beispiel = function () {
    console.log("Das ist ein ANDERES Beispiel.");
}

// 2. Aufruf
 beispiel();    

 //Funktion wird gekapselt und das Ergebnis ausgegeben
```

##### Funktionen und Scope
```javascript
// globale Variable
var a = "A";
console.log('Vor der Funktion ist a:', a);      //A
var b = "B";
console.log('Vor der Funktion ist b:', b);      //B

function test() {
    a = 'Neues A';
    console.log('In der Funktion ist a:', a);   //Neues A
    // lokale Variable
    var b = 'Neues B';
    console.log('In der Funktion ist b:', b);   //Neus B
    var c = 'Ein C';
    console.log('In der Funktion ist c:', c);   //Ein C
    d = 'Ein D';
    console.log('In der Funktion ist d:', d);   //Ein D
}

// console.log('Vor der Funktion ist d:', d);
//REFERROR -> Variable existiert er nach Ausführung der Funktion
test();

console.log('Nach der Funktion ist a:', a);     //Neues A

console.log('Nach der Funktion ist b:', b);     //B, da die Variable b nochmals lokal erzeugt wurde

// console.log('Nach der Funktion ist c:', c);  
//REFERROR -> existierte nur lokal zur Ausführungszeit der Funktion

console.log('Nach der Funktion ist d:', d);     
//Ooops-> Ein D wird nun global als Variable zur Verfügung gestellt, nach der Durchführung der Funktion test  
```
* Strict Mode
    * Gibt an ob eine Kompilierugn eigentlicht nicht mögilch ist Variable ohne Deklaration werden so aufgedeckt
# JavaScript Seminar
[Einführungswerke](https://github.com/getify/You-Dont-Know-JS)

## Markdown (.md) Formatierungsregeln
* [Markdown Tutorial Git](http://agea.github.io/tutorial.md/)
* [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)


## Visual Studio code
* Live Server als Extension installieren
** mit ALT + L + O wird der Server gestartet und die aktuelle Webseite geöffnet und bei jedem Speichern aktualisiert im Browser
* Formatierung des Texts mit ALT + Shift + F
* Zeilenumbruch aktivieren mit ALT + Z
* Aus-/Einkommentieren mit STRG + #

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

1. Types
```javascript
var a = null; -> object
var a = undefined; -> undefined
```

2. Primitive Typen
```javascript
var a = 1.5;    //Number
var a = true;   //bool
var a = 'Test'; //string
```

3. Komplexe Typen
```javascript
var a = ['Rosen','Tulpen','Nelken'];
var a = { x: "X", y: "Y", z: 'Z' };
var a = function () {
            //tut nix
        };
```
        
4. Definition von Zuständen ob eine Variable als gefüllt gilt
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

1. Globale Funktionen
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

2. Funktionen in Variable speichern
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

3. Funktionen und Scope
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
* [Strict Mode](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Strict_mode)
    * Gibt an ob eine Kompilierung eigentlicht nicht möglich ist.
    * Variablen ohne Deklaration werden so aufgedeckt.

4. Funktionen und Parameter
* Returns
    * Mit erneuter lokaler Deklaration
        ```javascript
        function addiere(a, b) {
            var a;
            var b = 5;
            return a + b;
        }

        var ergebnis = addiere(17, 6);
        console.log('ergebnis:', ergebnis); //22
        ```

    * Ohne erneute lokale Deklaration
        ```javascript
        function addiere(a, b) {
            return a + b;
        }

        var ergebnis = addiere(17, 6);
        console.log('ergebnis:', ergebnis); //23
        ```

    * Parameteranzahl variieren
        * Zusätzlicher Parameter mitgegeben
            ```javascript
            function addiere(a, b) {
                return a + b;
            }

            /*  KEIN Overload
            function addiere(a, b, c) {
                return a + b + c;
            } 
            */ 

            ergebnis = addiere(13, 14, 15); // Überschuss
            console.log('ergebnis:', ergebnis); //27
            ```

        * Zu wenig Parameter mitgegeben
            ```javascript
            function addiere(a, b) {
                return a + b;
            }

            /*  KEIN Overload
            function addiere(a) {
                return a;
            }
            */
            
            ergebnis = addiere(18); // fehlender Wert
            console.log('ergebnis:', ergebnis); //NaN
            ```

        > Überladung einer Funktion (eindeutiger Name) mit verschiedenen Parametern nicht möglich

* Defaults
     ```javascript
	// ECMA6: function addiere(a=0, b=0) { ... }
	function addiere(a, b) {
		a = a || 0;
		b = b || 0;
		return a + b;
	}

	var ergebnis = addiere(17, 6);
	console.log('ergebnis:', ergebnis); //23

	ergebnis = addiere(13, 14, 15); // Überschuss
	console.log('ergebnis:', ergebnis); //27

	ergebnis = addiere(18); // fehlender Wert
	console.log('ergebnis:', ergebnis); //18

	ergebnis = addiere(); // kein  Wert
	console.log('ergebnis:', ergebnis); //0
     ```

     > Wenn die Variable nicht gefüllt werden, dann werden Sie mit einem Defaultwert überschreiben

* Arguments
    ```javascript
    // HIER NICHT!!!
	// console.log('arguments:', arguments);

	// 1. impliziter Parameter: arguments-Object
	function addiere(a, b) {
		a = a || 0;
		b = b || 0;
		console.log('arguments:', arguments);
		console.log('arguments.length:', arguments.length);
		if (arguments.length > 2) {
	console.log('arguments[2]:', arguments[2]);
		}
		return a + b;
	}

	var ergebnis = addiere(17, 6);
	console.log('ergebnis:', ergebnis); //Wert 23 | Arguments-Anzahl:2

	ergebnis = addiere(13, 14, 15); // Überschuss
	console.log('ergebnis:', ergebnis); //Wert 27 | Arguments-Anzahl:3 | 3.ter Wert -> 15

	ergebnis = addiere(18); // fehlender Wert
	console.log('ergebnis:', ergebnis); //Wert 18 | Arguments-Anzahl:1

	ergebnis = addiere(); // kein  Wert
	console.log('ergebnis:', ergebnis); //Wert 0 | Arguments-Anzahl:0
     ```
     
     > In der Funktion ist es möglich auf die Parameterliste mittels argument zuzugreifen. Diese kann man per index durchlaufen und darauf zugreifen
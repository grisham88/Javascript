# JavaScript Seminar
[Einführungswerke](https://github.com/getify/You-Dont-Know-JS)

## Markdown (.md) Formatierungsregeln
* [Markdown Tutorial Git](http://agea.github.io/tutorial.md/)
* [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)


## Visual Studio Code
* Live Server als Extension installieren
** mit ALT + L + O wird der Server gestartet und die aktuelle Webseite geöffnet und bei jedem Speichern aktualisiert im Browser
* Formatierung des Texts mit ALT + Shift + F
* Zeilenumbruch aktivieren mit ALT + Z
* Aus-/Einkommentieren mit STRG + #
* Kommentar in JavaScript /**/ (Ein-/Mehrzeilig) oder // (Einzeilig)

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
> HOISTING bewirkt, dass Variablen und Funktionen egal an welcher Stelle sie deklariert wurden in der Ausführung am Anfang stehen.
Wird eine Function mit gleichem Namen deklariert, besteht in der Laufzeit immer nur die letzte Deklaration

> Der Code selbst wird dann linear abgearbeitet wobei Variablen immer zuerst deklariert sind und Funktionen global bereit stehen.

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
> Ausgabe gibt bei beiden Aufrufen die 2.te Deklaration aus.

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

        > Überladung einer Funktion (eindeutiger Name) mit verschiedenen Parametern nicht möglich.

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

     > Wenn die Variablen nicht gefüllt werden, dann werden Sie mit einem Defaultwert 0 (a = a || 0) überschrieben.

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
     
     > In der Funktion ist es möglich auf die Parameterliste mittels argument zuzugreifen. Diese kann man per Index durchlaufen und darauf zugreifen.

* Das geheimnisvolle 'this'
    > [Unterscheidung von Nutzung des this](https://www.w3schools.com/js/js_this.asp)
    * Nutzung von 'this' alleinestehend
        ```javascript
        var x = this;
        ```
        > Wenn es alleinestehend genutzt wird, bezieht es sich auf das globale Objekt. In einem Browser ist dieses Object das Window

    * Nutzung von 'this' in einer Function
        ```javascript
        function myFunction() {
            return this;
        }
        ```
        > Wenn es in einer Funktion genutzt wird, bezieht es sich auf das globale Objekt. In einem Browser ist dieses Object das Window.

    * Nutzung von 'this' in einer Function (scrict mode)
        ```javascript
        "use strict";
        var that = this; // Kontext aufbewahren

        function myFunction() {
            //return this;    // ERROR
            return that;      // erlaubt
        }
        ```
        > Wenn es in einer Funktion mit dem Strict Mode genutzt wird,ist 'this' undefiniert, da der Strict Mode keine Standardbindung erlaubt (default binding).
        Nur durch Aufbewahrung des Kontexts in einer anderen Variable ist der Zugriff möglich.

    * Nutzung von 'this' in einem Objekt
        ```javascript
        var person = {
            firstName  : "John",
            lastName   : "Doe",
            id         : 5566,
            myFunction : function() {
                return this;
            }
        };
        ```
        > Wenn es in einer Objekt genutzt wird, bezieht sich das 'this' auf das Ojekt in dem es direkt aufgerufen wurde.
        Das Ojekt ist der Besitzer der Funktion.

    * Nutzung von 'this' im Kontext 'Explicit Function Binding'
         ```javascript
        var person1 = {
            fullName: function() {
                return this.firstName + " " + this.lastName;
            }
        }
        var person2 = {
            firstName:"John",
            lastName: "Doe",
        }
        person1.fullName.call(person2);  // Gibt "John Doe" zurück
        ```
        > Die Methoden call () und apply () sind vordefinierte JavaScript-Methoden.
        Sie können beide verwendet werden, um eine Objektmethode mit einem anderen Objekt als Argument aufzurufen.
        In diesem Beispiel, wenn person1.fullName mit person2 aufgerufen wird, bezieht sicht 'this' zu person2, auch wenn es sich um eine Methode von person1 handelt.
        
#### Closures: Lexikalischer Kontext

* Funktionen haben dort ihren Gültigkeitsraum in dem sie deklariert wurden
* Das Ergebnis der Funktionsaufrufe wird immer als neue Instanz erzeugt und zeigt auf einen eigenen Speicherplatz

* Aufruf einer Funktion durch eine andere
    ```javascript
    var a = "Ein A";

    function aLesen() {
        console.log('Lese A:', a);
    }

    aLesen();   //Lese A: ein A

    function aLesenVerwenden() {
        console.log('Verwende aLesen()!');
        var a = "Anderes A";
        // liest - lexikalisch! - das äußere a!
        aLesen()
    }

    aLesenVerwenden()   //Verwende aLesen()! -> Lese A: ein A
    ``` 
    > Funktion merkt sich sozusagen als Objekt was es bei der Deklaration kennt und interessiert sich nicht für das neue 'a' das in Aufruf-Kontext existiert.

* Funktionen als Objekt speichern
    ```javascript
    function geheimnis(meinGeheimnis) {
    var geheim = meinGeheimnis;
    // console.log('Lese geheim:', geheim)

    // lokale Funktion:
    function geheimLesen() {
        console.log('Lese geheim:', geheim);
    }

    // geheimLesen(); 
    return geheimLesen;
    }

    var dasGeheimnis = geheimnis('Ganz furchtbar geheim...');
    console.log('dasGeheimnis:', dasGeheimnis)
    dasGeheimnis(); //Lese geheim: Ganz furchtbar geheim...

    var zweitesGeheimnis = geheimnis('Mein anderes Geheimnis!');
    console.log('dasGeheimnis:', dasGeheimnis)
    dasGeheimnis(); //Lese geheim: Ganz furchtbar geheim...

    zweitesGeheimnis(); //Lese geheim: Mein anderes Geheimnis!
    ```

    > Die Funktion wird als Object abgespeichert in dasGeheimnis, dieses wird nun nicht mehr geändert, da es sich um eine Instanz handelt

* Funktionen als Objekt speichern und Property per Setter ersetzen
    ```javascript
    function geheimnis(meinGeheimnis) {
    var geheim = meinGeheimnis;

    // lokale Funktion:
    function geheimLesen() {
        console.log('Lese geheim:', geheim);
    }

    function geheimSchreiben(meinNeuesGeheimnis) {
        geheim = meinNeuesGeheimnis;
    }
    
    /*Zugriff auf interen Methoden wird durch neue Methodennamen freigegeben 
    (Parameter werden implizit erzeugt für das Property der Methode)
    */
    
    return {
        getGeheim: geheimLesen,
        setGeheim: geheimSchreiben
    };
    }

    var dasGeheimnis = geheimnis('Ganz furchtbar geheim...');
    dasGeheimnis.getGeheim();   //Lese geheim: Ganz furchtbar geheim...
    dasGeheimnis.setGeheim('Geht das auch? Mal sehen...');
    dasGeheimnis.getGeheim();   //Lese geheim: Geht das auch? Mal sehen...    
    ```

    > Mittels Properties im return der Function können interne Methoden erreicht werden
    > Object existiert durchgehend und weiß noch alles was jemals gesetzt wurde
    
### Arrays
* Sammlung (Collection) von Daten die per Index aufgerufen/verändert werden können
* Handelt sich um ein Object
* Anzahl der Elemente im Array definiert die Länge des Arrays
* Arrays verhält sich in JavaScript wie eine Mischung aus Array/ Liste und Map
    ```javascript
    var arr = ['Rosen', 'Tulpen', 'Nelken'];

    console.log('arr.length:', arr.length); //3
    console.log('arr[1]:', arr[1]); //Tulpen

    arr[4] = "Veilchen";
        
    console.log('arr.length:', arr.length); //5
    console.log('arr[4]:', arr[4]); //Veilchen
    
    //modifizierende Methoden: push(), pop(), shift(), unshift()
    arr.push('Geranien');

    console.log('arr.length:', arr.length); //6
    console.log('arr[5]:', arr[5]); //Geranien

    // Array auslesen:
    for (i = 0; i < arr.length; i++) {
        console.log(arr[i]);
    }
    //Rosen, Tulpen, Nelken, undefined, Veilchen, Geranien

    //Inhalt des Arrays vertauschen 0-> n, n->0 etc.
    arr.reverse();

    // Array auslesen:
    for (var i = 0; i < arr.length; i++) {
        console.log('i:', arr[i]);
    }
    //Geranien, Veilchen, undefined, Nelken, Tulpen, Rosen

    console.log('What" "? i:', i); // 6 
    // Mit Ecma6 wird i nicht global definiert

    ```

    * Durch Setzung eines Werts in einen Index der vorher nicht definiert war, wird das Array bis zu diesem Index erweitert. Sind Indizes nicht gesetzt, sind diese nun undefined und erreichbar.
    * Modifizierende Methoden
        * Mittels der Methoden push/pop/shift/unshift ist das Array um einen Wert erweiterbar oder reduzierbar.
    * Es ist auch möglich nur durch die enthaltenen Elemente zu laufen (mittels Key). Der Index der undefined ist, wird nicht durchlaufen
    * Auswertende Methoden (Arbeiten auf dem Array möglich)
        * for-in-Schleife
        ```javascript
        for (var item in arr) {
            console.log(item, arr[item]);
        }
        //0 Geranien, 1 Veilchen, 3 Nelken, 4 Tulpen, 5 Rosen
        ```
                
        * forEach(fn) (Higher Order Methode)
        ```javascript
         // ECMA6 : arr.forEach(el => console.log(el))
        arr.forEach(function () {
            // this können wir hier NICHT brauchen
            console.log('Hepp', arguments)
        });
        //Es werden immer 3 Argumente beim ArrayElement mitgegeben

        //Zugriff auf die einzelnen Argumente möglich
        arr.forEach(function (value, index, arrayInstance) {
            console.log('Hepp', val)
        });
        /*
        "Geranien", 0, Array(6)
        "Veilchen", 1, Array(6)
        "Nelken", 3, Array(6)
        "Tulpen", 4, Array(6)
        "Rosen", 5, Array(6)
        */
        ```

        * some(fn) => boolean
        ```javascript
        var daten = [3, 7, 4, 89, 12, 8, 4, 80, 4, 23, 7];

        if (daten.some(function (val) {
            return val > 7;
        })) {
        console.log('Werte sind brauchbar...');
        }
        //Werte sind brauchbar
        ```

        * every(fn) => boolean
        * filter(fn) => new Array
        ```javascript
        var daten = [3, 7, 4, 89, 12, 8, 4, 80, 4, 23, 7];

        var gefiltert = daten.filter(function (val) {
            return val > 7;
        })

        console.log(gefiltert.length); // Neues Array mit 5 Elementen
        ```

        * map(fn) => new Array
        ```javascript
        var daten = [3, 7, 4, 89, 12, 8, 4, 80, 4, 23, 7];

        var quadriert = daten.map(function (item) {
            return item * item;
        });
        //Gibt ein neues Array zurück (gleiche Größe/Neue Inhalte)
        ```

        * reduce(fn) => value ()
         ```javascript
        var daten = [3, 7, 4, 89, 12, 8, 4, 80, 4, 23, 7];

        var summe = daten.reduce(function (a, b) {
            return a + b;
        });
        
        console.log(summe); // Kombiniert alle Werte miteinander
        ```

### DOM
* Wird der DOM-Baum durchlaufen muss das Script berücksichtigen, dass der Baum auch bereits erzeugt wurde.
* Script-Block im Head, kennt ggf. den body noch nicht.
    * Scriptblock am Ende des Bodys setzen, sofern der DOM verarbeitet werden soll
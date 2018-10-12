# JavaScript Seminar
* [Einführungswerke](https://github.com/getify/You-Dont-Know-JS)
* [Das Curry-Buch - Funktional programmieren lernen mit JavaScript](https://github.com/grisham88/Javascript/blob/master/unterlagen/Das%20Curry-Buch%20-%20Funktional%20programmieren%20lernen%20mit%20JavaScript.pdf)

## Markdown (.md) Formatierungsregeln
* [Markdown Tutorial Git](http://agea.github.io/tutorial.md/)
* [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
* [Mastering Markdown](https://guides.github.com/features/mastering-markdown/)


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
Vermutlich werden alle Defaultzustände wenn man weiß welcher Typ die Variable hat, als FALSE empfunden

### Functions
#### Function
> HOISTING bewirkt, dass Variablen und Funktionen egal an welcher Stelle sie deklariert wurden in der Ausführung am Anfang stehen.  
Wird eine Function mit gleichem Namen deklariert, besteht in der Laufzeit immer nur die letzte Deklaration.  
Der Code selbst wird dann linear abgearbeitet wobei Variablen immer zuerst deklariert sind und Funktionen global bereit stehen.

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
            Das Objekt ist der Besitzer der Funktion.

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
    
    /*
    Zugriff auf interne Methoden, wird durch neue Methodennamen freigegeben 
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

    > Mittels Properties im return der Function können interne Methoden erreicht werden.  
    Object existiert durchgehend und weiß noch alles was jemals gesetzt wurde
    
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
            var arr = ['Rosen', 'Tulpen', 'Nelken'];

            for (var item in arr) {
                console.log(item, arr[item]);
            }
            //0 Geranien, 1 Veilchen, 3 Nelken, 4 Tulpen, 5 Rosen
            ```                
        * forEach(fn) (Higher Order Methode)
            ```javascript
            var arr = ['Rosen', 'Tulpen', 'Nelken'];

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
#### Script Verhalten
* Wird der DOM-Baum durchlaufen muss das Script berücksichtigen, dass der Baum auch bereits erzeugt wurde.
* Script-Block im Head, kennt ggf. den body noch nicht.
    * Scriptblock am Ende des Bodys setzen, sofern der DOM verarbeitet werden soll
##### OnLoad-Event
* Mittels window.onload können die Änderungen/Abfragen auf dem DOM auch im Header mittels Script gesetzt werden. Sie werden dann erst gesetzt, wenn das Element existiert
* Javascript onload feuert, wenn der Browser das HTML-Dokument mit CSS-Dateien, Bildern und iframes geladen hat. Bilder werden allerdings asynchron geladen, so dass sie beim load-Event u.U. noch nicht verfügbar sind, weil der Ladevorgang noch andauert.
* [weitere Infos](https://www.mediaevent.de/javascript/onload.html)
##### Änderung von DOM-Elementen mittels Skript
```javascript
<script>
    window.onload = function () {
    var p11 = document.getElementById("p11");
    console.log(p1);
    // Attribut setzen
    p11.title = 'Ich bin der Titel!';
    // CSS-Style setzen
    p11.style.backgroundColor = 'yellow';
    // CSS-Class setzen
    p11.className = 'rahmen';
    // Inhalte ändern:
    p11.innerHTML = 'Das ist ein <b>ganz</b> neuer Inhalt!';

    // der Node hat auch Methoden:
    var p20 = document.getElementById("p20");
    p20.addEventListener('click', function (e) {
        console.log('Observer:', this);
        console.log('EventObjekt:', e);
    })
    };
</script>
```

```html
<body>
<h1>DOM</h1>
<p id="p1">Textabsatz, der selektiert wird</p>
<p id="p10">Textabsatz, der selektiert wird</p>
<p id="p11">Textabsatz, der selektiert wird</p>
<p id="p19">Textabsatz, der selektiert wird</p>
<p id="p20">Textabsatz, der selektiert wird</p>
</body>
```
> Durch das Skript wird das komplette p11-element verändert.  
Durch das Skript wird das p20-element überwacht und beim click auf das Element das p Element und die Position der Clicks der Maus im Log ausgegeben.

#### Zugriffsmethoden
##### document
* getElementById
* getElementsByTagName
* getElementsByClassName
* querySelector
* querySelectorAll
* head
* body
* createElement
    ```javascript
    var meinDiv = document.createElement('div');
    //Setzen von Properties im Div
    meinDiv.id = 'FirstCreatedDiv';
    meinDiv.title = 'Mein neues Div';
    meinDiv.className = 'rahmen';
    meinDiv.innerHTML = 'Mein <i>neues</i> Div-Element.';

    console.log(meinDiv)
     ```

* Element an eine bestimmte Stelle im Dokument einfügen
    > Hier wird nur die Parentreferenz geändert, das Element wird dadurch nicht an mehreren Stellen gleichzeitig eingefügt
    * PARENT.appendChild(NEUER_KNOTEN)
        ```javascript    
        var meinDiv = document.createElement('div');
        //Setzen von Properties im Div
        meinDiv.id = 'FirstCreatedDiv';
        meinDiv.title = 'Mein neues Div';
        meinDiv.className = 'rahmen';
        meinDiv.innerHTML = 'Mein <i>neues</i> Div-Element.';

        document.body.appendChild(meinDiv);
        ```
    * PARENT.insertBefore(NEUER_KNOTEN, REFERENZ))
        ```javascript
        var meinDiv = document.createElement('div');
        //Setzen von Properties im Div
        meinDiv.id = 'FirstCreatedDiv';
        meinDiv.title = 'Mein neues Div';
        meinDiv.className = 'rahmen';
        meinDiv.innerHTML = 'Mein <i>neues</i> Div-Element.';

        var bezugsknoten = document.getElementById('p1');
        // okay, aber ich muss ZWEI Knoten kennen:
        document.body.insertBefore(meinDiv, bezugsknoten);
        // besser
        bezugsknoten.parentNode.insertBefore(meinDiv, bezugsknoten);
        ```

* Element kopieren
    > ACHTUNG  
    Events werden nicht mitkopiert
    * ohne Unterelemente -> cloneNode()
        ```javascript    
        var meinDiv = document.createElement('div');
        //Setzen von Properties im Div
        meinDiv.id = 'FirstCreatedDiv';
        meinDiv.title = 'Mein neues Div';
        meinDiv.className = 'rahmen';
        meinDiv.innerHTML = 'Mein <i>neues</i> Div-Element.';
        
        var klonDiv = meinDiv.cloneNode();
        console.log('Klon: ', klonDiv);
        document.body.appendChild(klonDiv);
        ```
    * mit Unterelementen -> cloneNode(true)
        ```javascript    
        var meinDiv = document.createElement('div');
        //Setzen von Properties im Div
        meinDiv.id = 'FirstCreatedDiv';
        meinDiv.title = 'Mein neues Div';
        meinDiv.className = 'rahmen';
        meinDiv.innerHTML = 'Mein <i>neues</i> Div-Element.';
        
        var klonDiv = meinDiv.cloneNode(true);
        console.log('Klon: ', klonDiv);
        document.body.appendChild(klonDiv);
        ```
    
##### HTMLElementNode
* getElementsByTagName
* getElementsByClassName
* addEventListener()
    > Mehrere Funktionszuweisungen zum Event möglich

    ```javascript
    var meinDiv = document.createElement('div');
    meinDiv.id = 'FirstCreatedDiv';
    meinDiv.title = 'Mein neues Div';
    meinDiv.className = 'rahmen';
    meinDiv.innerHTML = 'Mein <i>neues</i> Div-Element.';
    
    //Events mit Funktionen füllen
    meinDiv.addEventListener('click', function (e) {
        console.log('1. Listener: Neues Div wurde geklickt...');
    });

    meinDiv.addEventListener('click', function (e) {
        console.log('2. Listener: Neues Div wurde geklickt...');
    });

    //Beide Funktionen werden beim Ausführen des Events nacheinander abgearbeitet
    ```
* data-*-> dataSet
    ```javascript
    var article = document.getElementById('electriccars');

    article.dataset.columns // "3"
    article.dataset.indexNumber // "12314"
    article.dataset.parent // "cars"

    /*
    Each property is a string and can be read and written.
    In the above case setting article.dataset.columns = 5 would change that attribute to "5".
    */
    ```

### JSON
#### Definition
> Die JavaScript Object Notation, kurz JSON, ist ein kompaktes Datenformat in einer einfach lesbaren Textform zum Zweck des Datenaustauschs zwischen Anwendungen. Jedes gültige JSON-Dokument soll ein gültiges JavaScript sein und per eval interpretiert werden können.

#### Sonderfälle
> Wird ein Objekt nach Json geparst, fallen alle Funktionen weg.   Das bedeutet beim zurückparsen enthält dieses im Objekt nur reine Informationen und keine Funktionen mehr.

#### Anwendungsbeispiel für JSON Behandlung 
Objekt -> json / json -> Objekt
```javascript
var person = {
    vorname: 'Peter',
    alter: 30,
    haustier: ['Dackel', 'Katze'],

    hallo: function () {
        console.log('Hi! Ich bin nicht erlaubt!');
    }
};

console.log(person);        // {vorname: "Peter", alter: 30, haustier: Array(2), hallo: ƒ}

// JSON-Methoden
// Objekt in String umwandeln
var jsonString = JSON.stringify(person);
console.log(jsonString);    // {"vorname":"Peter","alter":30,"haustier":["Dackel","Katze"]}

// String in Objekt
var ojbAusJson = JSON.parse(jsonString);
console.log(ojbAusJson);    // {vorname: "Peter", alter: 30, haustier: Array(2)}
```

### AJAX
* [AJAX Einführung (Tutorial)](https://www.html-seminar.de/ajax-einfuehrung.htm)
* [HTTP - Requests](https://www.tutorialspoint.com/http/http_requests.htm)

#### Definition
    Asynchronous  
    JavaScript  
    And  
    XML  
    
#### Ablauf
```javascript
// 1) Request bilden
var req = new XMLHttpRequest(); // readyState: 0

// 2) Request konfigurieren
req.open('GET', 'data/data.html', true) // readyState: 1

/*
Listener auf den ReadyState legen (Function frühzeitig zuweisen/Ausführung automatisch)
Dadurch wird abgewartet bis der Aufruf abgearbeitet wurde 
und erst dann sind die Daten verfügbar
*/
req.onreadystatechange = function () {
    console.log(this.readyState);
    if (this.readyState === 4)
        console.log("Daten:", req.responseText);
    
    //Erhaltende Daten werden dann, wenn Sie da sind an einem gewünschten Punkt eingefügt
    document.getElementById('ausgabe').innerHTML = req.responseText;
}
    
// 3) Request ausführen
req.send();

// Daten sind im req-object ... aber: NICHT JETZT!!!
console.log("Daten:", req.responseText); // Keine Daten da asynchron
```
```html
<body>
    <div id="ausgabe">Hier erscheint der Text, sobald der Request den Readystate 1 hat</div> 
</body>
```

#### Ablauf mit JSON
* Zugriff auf Objekte und deren Inhalt
    ```javascript
    window.onload = function () {
        // hier ajaxen! Diesmal JSON
        var req = new XMLHttpRequest(); // readyState: 0

        req.open('get', 'data/personen.json', true); // readyState: 1

        req.onreadystatechange = function () {
            console.log(this.readyState);
            if (this.readyState === 4) {
                console.log('DataString:', this.responseText);
                /*
                DataString: {
                    "success": true,
                    "dataProp" : "personen",
                    "primKey": "mId",
                    "personen" : [
                        {"vorname":"Peter", "nachname":"Panter","mId":"m001"},
                        {"vorname":"Theo", "nachname":"Tiger","mId":"m002"},
                        {"vorname":"Leo", "nachname":"Löwe", "mId":"m004"},
                        {"vorname":"Anton", "nachname":"Ameise", "mId":"m007"},
                        {"vorname":"Bruno", "nachname":"Büffel", "mId":"m006"}
                    ]
                }
                */


                var dataObj = JSON.parse(this.responseText);
                console.log('DataObject:', dataObj);
                /*
                DataObject: 
                {success: true, dataProp: "personen", primKey: "mId", personen: Array(5)}
                dataProp
                :
                "personen"
                personen
                :
                (5) [{…}, {…}, {…}, {…}, {…}]
                primKey
                :
                "mId"
                success
                :
                true
                __proto__
                :
                */
                    
                //Hier muss man wissen wie das Ojekt heißt
                var dataList = dataObj.personen;
                    
                //Hier ist es nicht notwendig zu wissen wie das Ojekt heißt
                var dataList = dataObj[dataObj.dataProp];
                console.log('DataList:', dataList);
                /*
                DataList: DataList: 
                (5) [{…}, {…}, {…}, {…}, {…}]
                0
                :
                {vorname: "Peter", nachname: "Panter", mId: "m001"}
                1
                :
                {vorname: "Theo", nachname: "Tiger", mId: "m002"}
                2
                :
                {vorname: "Leo", nachname: "Löwe", mId: "m004"}
                3
                :
                {vorname: "Anton", nachname: "Ameise", mId: "m007"}
                4
                :
                {vorname: "Bruno", nachname: "Büffel", mId: "m006"}
                length
                :
                5
                __proto__
                :
                Array(0)
                */
            }
        }
        req.send();
    }
    ```
* Zugriff auf Objekte und Ausgabe in HTML
    ```javascript
    window.onload = function () {
        // hier ajaxen! Diesmal JSON
        var req = new XMLHttpRequest(); // readyState: 0

        req.open('get', 'data/states.json', true); // readyState: 1

        req.onreadystatechange = function () {
            if (this.readyState === 4) {
                // console.log('DataString:', this.responseText);

                // Da das json direkt die Einzelemente enthält, kommt der Inhalt als Array zurück
                var dataObj = JSON.parse(this.responseText);
                console.log('DataObject:', dataObj);

                var array = dataObj;
                console.log('Elemente durchlaufen:');

                var bezugsknoten = document.getElementById('ausgabe');

                array.forEach(element => {
                    console.log(element.name + " (" + element.abbreviation + ")");

                    var pElement = document.createElement('p');
                    pElement.textContent = element.name + " (" + element.abbreviation + ")";
                    bezugsknoten.appendChild(pElement);
                });
            }
        }
        req.send();
    }
    ```
    ```html
    <body>
        <div id="ausgabe">Hier erscheinen die Aufbereiteten JSON-Elemente, sobald der Request den Readystate 1 hat</div> 
    </body>
    ```
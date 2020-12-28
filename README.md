# Web Programming - Toolbox of Mithusan Sivakumar

## Semesterwoche 01
`setInterval()` ist eine Funktion, um gewisse Funktionen, Expression, etc. in vorgegebenen Intervallen immer wieder aufzurufen. Die angegebene Zeit ist in ms.
```javascript
setInterval(() => {
    FUNCTION_CALL;
    EXPRESSION;
    WAS_IMMER_DAS_HERZ_BEGEHRT;
}, 1000 / 5); // entspricht hier 5x pro Sekunde => alle 200 ms
```

## Semesterwoche 02
Variablen sollten immer als `const` (immutable) oder als `let` (mutable) deklariert werden. **NIE** `var` oder globale Variablen verwenden.

Lambda-Reduktionen ($\alpha$, $\beta$, $\eta$):
```javascript
const id = x => x;
const konst x => y => x;
const snd = konst (id);

document.writeln( id(id) === id );
document.writeln( konst(id)(undefined) === id );
document.writeln( snd(undefined)(id) === id );
```

## Semesterwoche 03
Strategie mit Konstruktoren und Accessoren (`the basic sum type`):
```javascript
const Left   = x => f => g => f (x);        // ctor 1
const Right  = x => f => g => g (x);        // ctor 2
const either = e => f => g => e (f) (g);    // accessor
```

Einsatz von `either`, um null / undefined zu umgehen:
```javascript
either (expression) (Fehlerbehandlung) (positiveRueckmeldung);
```

## Semesterwoche 04
Array deconstructor:
```javascript
let [x, y] = [1, 2]     // x = 1, y = 2
const swap = ([x, y]) => [y, x];
```

Map:
```javascript
const twoTimes = x => x * 2;
[1, 2, 3].map(x => twoTimes(x));
[1, 2, 3].map(twoTimes);            // [2, 4, 6]
```

Filter
```javascript
const odd = x => x % 2 === 1;
[1, 2, 3].filter(x => odd(x));
[1, 2, 3].filter(odd);              // [1, 3]
```

Reduce:
```javascript
const plus = (accu, cur) => accu + cur;
[1, 2, 3].reduce((accu, cur) => accu + cur);
[1, 2, 3].reduce(plus);             // 6
```

## Semesterwoche 05
Strings in JavaScript:
```javascript
const str1 = 'string ' + VARIABLE;
const str2 = "string " + VARIABLE;
const str3 = `string ${VARIABLE}`;  // multiple line möglich
const str4 = String( ELEMENT );     // ELEMENT kann ein Typ sein, bsp number oder boolean
                                    // aber auch ein RegEx.
```

Strings als code durchführen:
```javascript
eval(STRING_HERE);                          // wird bei jedem Aufruf neu geparst -> evaluiert
Function(PARAMETER, 'return ' + FUNCTION);  // wird ein mal global evaluiert
```

## Semesterwoche 06
Objekte erstellen:
```javascript
// open, dynamic
const Person = {
    firstname: "Max",
    lastname: "Muster",
    getName: function() {
        return this.firstname + " " + this.lastname
    }
};

// closed, explicit
function Person(firs, last) {
    let firstname = first;
    let lastname = last;
    return {
        getName: function() {
            return firstname + " " + lastname
        }
    }
}

// mixed, classified
const Person = ( () => {
    function Person(first, last) {
        this.firstname = first;
        this.lastname = last;
    }

    Person.prototype.getName = function() {
        return this.firstname + " " + this.lastname;
    }

    return Person;
}) (); // new Person("Max", "Muster") instance of Person
```

## Semesterwoche 07
Klassen erstellen:
```javascript
class Person {
    constructor(first, last) {
        this.firstname = first;
        this.lastname = last;
    }

    getName() {
        return this.firstname + " " + this.lastname;
    }
} // new Person("Max", "Muster") instance of Person
```

```javascript
class Student extends Person {
    constructor(first, last, grade) {
        super(first, last); // WICHTIG!
        this.grade = grade;
    }
}

const s = new Student("Max", "Muster", 5.5);
```

Prototype:
```javascript
Number.prototype.times = function(callback) {
    return Array.from({ length: this }, (_, idx) => callback(idx));
}

(10).times(n => console.log(n));
```

## Semesterwoche 08
Testing, z. B. das Prototype Beispiel aus Semesterwoche 07:
```javascript
test("util-times1", assert => {

    const collect = [];

    (10).times( n => collect.push(n) );

    assert.equals(collect.length ,  10);
    assert.equals(collect[0]     ,   0);
    assert.equals(collect[9]     ,   9);
}) ;
```

Ein Weg um JavaScript zu laden:
```javascript
const testNames = [
    'util',
    'todo'
];

testNames.forEach( testName => {
    document.write(`<script src="${testName}/${testName}.js"></s`+'cript>');
    document.write(`<script src="${testName}/${testName}Test.js"></s`+'cript>');
});
```

## Semesterwoche 09
Einfacher Observer:
```javascript
const Observable = value => {
    const listeners = [];
    return {
        onChange: callback => listeners.push(callback),
        getValue: ()       => value,
        setValue: val      => {
            if (val === value) return;
            value = val;
            listeners.forEach(notify => notify(val));
        }
    }
}
```

### Higher-order Functions:
Funktionen als Argumente einer Funktion übergeben. Dies ist möglich, weil in JavaScript Funktionen auch Objekte sind.
```javascript
const logger = (message) => console.log(message); // Erinnerung: ETA-Reduktion möglich zu:
                                                  // const logger = console.log;

const someFunction = (logFn) => {
    // do some stuff here
    const msg = ...;
    logFn(msg);  // erstellt ein console.log
}
```
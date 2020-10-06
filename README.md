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
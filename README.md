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
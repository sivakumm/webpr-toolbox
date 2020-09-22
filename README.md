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
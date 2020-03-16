# Loops and Iteration

## 'For' loop

Nejzákladnější forma iterace, s pevným počtem opakování.

```
Obecně:
for ([initialExpression]; [condition]; [incrementExpression])
  statement

Konkrétně:
const orderNumbers = ['1548526', '1548527', '1548531', '1548542']

for (let i = 0; i < orderNumbers.length, i++) {
  console.log(`Číslo objednávky je: ${orderNumbers[i]}`)
}
```

'For' loop používá `counter`, u kterého nejprve přiřadíme iniciální hodnotu, toto je tzv. řídící proměnná
`let i = 0 //initial expression`

dále určíme podmínku pro vykonání kroku cyklu
`i < orderNumbers.length //condition`

a na závěr příkaz, který modifikuje řídící proměnnou v každém kroku iterace
`i++ //increment expression`

## Inkrementace & Dekrementace - operátory

`i++` je zápis, který umožní přičíst proměnné 1 a navrátit její hodnotu.
Stejně tak můžeme použít `i--` pro dekrementaci.

```
let a = 5

a++ // 5 - hodnota 'a' před inkrementací

let b = 5

++b // 6 - hodnota 'b' po inkrementaci

```


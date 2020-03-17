# Loops and Iteration

## 'For' loop

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for

Nejzákladnější forma iterace, s pevným počtem opakování.

```
Obecně:
for ([initialExpression]; [condition]; [incrementExpression])
  statement

Konkrétně:
const orderNumbers = ['1548526', '1548527', '1548531', '1548542']

for (let i = 0; i < orderNumbers.length, i++) {
  console.log(i + '. objednávka má číslo: ' + orderNumbers[i]) // lépe: console.log(`${i}. objednávka má číslo: ${orderNumbers[i]}`)
}
```

'For' loop používá `counter`, u kterého nejprve přiřadíme iniciální hodnotu, toto je tzv. řídící proměnná
```
let i = 0 //initial expression
```

dále určíme podmínku pro vykonání kroku cyklu
```
i < orderNumbers.length //condition
```

a na závěr příkaz, který modifikuje řídící proměnnou v každém kroku iterace
```
i++ //increment expression
```

## Inkrementace & Dekrementace - operátory (odbočka)

`i++` je zápis, který umožní přičíst proměnné 1 a navrátit její hodnotu.
Stejně tak můžeme použít `i--` pro dekrementaci.

```
let a = 5

a++ // 5 - hodnota 'a' před inkrementací

let b = 5

++b // 6 - hodnota 'b' po inkrementaci

```

## 'For...In' loop

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in

Pro iteraci skrze objekty (pozor, můžete použít i na polle, ale není to doporučované, viz dokumentace) můžeme použít cyklus 'For...In', který je zjednodušením klasického 'For' cyklu, neboť se obejdeme bez počítadla.

```
const orders = {
  1548526: { item: 'Pračka' }, 
  1548527: { item: 'Myčka' },
  1548531: { item: 'Sušička' },
  1548542: { item: 'Kávovar' }
}

for (let order in orders) {
  console.log(orders[order])
}
```

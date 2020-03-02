# Datové typy

Javascript je jazyk, který je dynamicky typovaný (dynamically typed). To znamená, že datový typ proměnné se vyhodnotí při runtime na základě jeho hodnoty.

Rozlišujeme celkem 8 základních datových typů.

## Number

Datový tym Number reprezentuje jak celá čísla, tak čísla desetinná.
Můžeme s nimi provádět matematické operace `+`, `-`, `*`, `/` atd.
Kromě čísel, se můžeme setkat i s hodnotami speciálními, které spadají pod tento datový typ, jsou to:
`Infinity`, `-Infinity` a `NaN` (Not a Number)

`1 / 0 // Infinity`
`-1 / 0 // -Infinity `
`'myString' / 2 // Nan`

Můžeme si všimnou, že svět javascriptu je na nás hodný a nechá nás např. dělit nulou, matematické operace, jakkoliv špatně postavené jsou "safe".

## BigInt

https://javascript.info/bigint

Nedávno přidaný datový typ, který slouží pro reprezentaci velmi velkých celých čísel (>2^53 || <-2^53).
V tuto chvíli je podporováno pouze na FF a Chrome.

```
Deklarace:
const myBigInt = 1234567890123456789012345678901234567890n;

Převod:
const myBigInt = BigInt("1234567890123456789012345678901234567890");
```

## String

Řetězce vždy obalujeme uvozovkami.
```
let myString = "Pikachu" // doublequotes
let myString = 'Pikachu' // singlequotes
let myString = `Pikachu` // backticks
```

Backticks jsou uvozovky umožňující vkládání proměnných a výrazů do řetězce obalením ${myVariable}.

```
let myVariable = 'Ahoj'

console.log(`${myVariable} pikachu.`)
```

```
let myVariable = 'Ahoj'

console.log(`9 děleno 3 jsou ${1 + 2}.`)
```

## Boolean

Boolean je logický typ nabývající hodnot `true` nebo `false`.
Jako `false` jsou vyhodnoceny hodnoty `0`, `-0`, `null`, `false`, `Nan`, `undefined` nebo `''` (prázdný string). Všechny ostatní nabývají hodnoty true, např. `[]`, `'false'` atd.







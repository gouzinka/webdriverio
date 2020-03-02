# Datové typy

Javascript je jazyk, který je dynamicky typovaný (dynamically typed). To znamená, že datový typ proměnné se vyhodnotí při runtime na základě jeho hodnoty.

Rozlišujeme celkem 8 základních datových typů.

## Number

Datový tym Number reprezentuje jak celá čísla, tak čísla desetinná.
Můžeme s nimi provádět matematické operace `+`, `-`, `*`, `/` atd.
Kromě čísel, se můžeme setkat i s hodnotami speciálními, které spadají pod tento datový typ, jsou to:
`Infinity`, `-Infinity` a `NaN` (Not a Number)

```
1 / 0 // Infinity

-1 / 0 // -Infinity

'myString' / 2 // Nan
```
Můžeme si všimnou, že svět javascriptu je na nás hodný a nechá nás např. dělit nulou, matematické operace, jakkoliv špatně postavené jsou "safe".

Chceme-li hodnotu převést na datový typ Number, použijeme funkci Number()

```
Number('17') // -> 17
Number('Ahoj') // -> Nan
Number(new Date()) // -> 1583146263453
```

Existuje celá řada zajímavých metod https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number
Např. metoda `Number.isNaN()` nebo `Number.isFinite()`.


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
console.log(`9 děleno 3 jsou ${1 + 2}.`)
```

Na String převádíme pomocí funkce `String()` nebo metody `toString()`.

## Boolean

Boolean je logický typ nabývající hodnot `true` nebo `false`.
Jako `false` jsou vyhodnoceny hodnoty `0`, `-0`, `null`, `false`, `Nan`, `undefined` nebo `''` (prázdný string). Všechny ostatní nabývají hodnoty true, např. `[]`, `'false'` atd.

Na Boolean převádíme pomocí funkce `Boolean` nebo `!!` (double NOT operator).

## Null

Speciální hodnota `null` reprezentuje 'neznámou hodnotu' (nic :D).

```
let age = null
```

Typicky používáme jako "prázdnou" či "neznámou" hodnotu.

## Undefined

Speciální hodnota `undefined` reprezentuje 'hodnota nebyla přidána'.

```
let myVariable

console.log(myVariable) // undefined
```

Typicky používáme pro zjištění, zda hodnota byla udána.

## Symbol

Slouží jako unikátní identifikátor objektům, více na
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol

## Object

Objekt je datová struktura obsahující data a instrukce pro jejich zpracování. Jako jediný není primitivním datovým typem, neboť může uložit kolekce dat a komplexní entity.

```
let user = new Object() // "object constructor" syntax
let user = {}  // "object literal" syntax
```

Vlastnosti objektu - páry klíčů (key) a hodnot (value):
```
let user = {     // an object
  name: "John",  // by key "name" store value "John"
  age: 30        // by key "age" store value 30
}
```








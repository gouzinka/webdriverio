# Odbočka k JavaScriptu

JavaScript je programovací jazyk, který je multiplatformní, setkáme se s ním na webových stránkách, kde vykonává úlohy na straně klienta, zároveň je však užit v prostředích jako je Node.js.

Standardem pro JavaScript, je ECMAScript https://developer.mozilla.org/en-US/docs/Web/JavaScript/Language_Resources. V roce 2015 vyšel po 6 letech průlomový update s označením ECMAScript 2015, nebo také často jako ES6. Přinesl mnoho novinek (např. let/const klíčová slova pro označení proměnných, deklaraci tříd, import/export...). Od tohoto vydání dochází k publikaci nového každý rok, aktuálně se tedy můžeme těšit z ECMAScript 2019 (ES10), který například přinesl nové možnosti práce s poli - https://blog.logrocket.com/5-es2019-features-you-can-use-today/
Tyto nové featury jsou implementovány postupně, podporu pro Node.js můžeme vidět zde https://node.green/, abychom mohli využívat nejnovějších featur a nemuseli se bát, že je nebude naše prostředí podporovat, můžeme použít kompilátor - https://babeljs.io/

## Jak definovat proměnnou

Proměnné slouží k uložení hodnot, v javaScriptu deklarujeme proměnnou pomocí klíčového slova `let`, `const`, nebo méně doporučovaného `var`.
Jak proměnné vlastně fungují? https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_Types#Variables

## `var` vs. `let`

Historicky existovalo pro definování proměnných v javaScriptu pouze klíčové slovo `var`. To však bylo změněno v roce 2015, kdy ES6 přinesl nové klíčové slovo `let`.
Jak se vlastně liší? Najdete zde https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/Variables#The_difference_between_var_and_let

## Jak psát funkce

Společně s `let` a `const` ES6 přinesla také tzv. 'arrow functions'. Ty představují kompaktnější syntaxi pro zápis funkcí.
https://hacks.mozilla.org/2015/06/es6-in-depth-arrow-functions/
https://www.freecodecamp.org/news/when-and-why-you-should-use-es6-arrow-functions-and-when-you-shouldnt-3d851d7f0b26/

# Odbočka k Selektorům

https://webdriver.io/docs/selectors.html

Typicky budeme používat CSS, nebo xPath.


# Assertions

Assertions porovnávají dvě hodnoty, pokud jsou rozdílné, vytvoří error a test vyhodnotí negativně.

* Zabudovaná Node.js assertion knihovna (https://nodejs.org/api/assert.html)
Knihovnu vkládáme pomocí require statementu `var assert = require('assert');`

Pozitivní průchod
```
let assert = require('assert')

assert.strictEqual(1,1)
```

Negativní průchod
```
let assert = require('assert')

assert.strictEqual(1,2)
```

NotEqual příklad:
```
let assert = require('assert')

let expected = 1
let actual = 1 + 1

assert.notStrictEqual(expected, actual)
```

# Reporter

Pokud jsme jej neinstalovali jako součást wdio/cli, nainstalujeme jej příkazem

`npm install @wdio/dot-reporter --save-dev`

Spusťme negativní průchod
```
let assert = require('assert')

describe('Mall.cz homepage', () => {
    it('should have the right title', () => {
        browser.url('./')

        const expected = 'MALL.CZ – bílé zboží, elektronika, PC, outdoor, hobby, hračky, kosmetika, chovatelské potřebi'
        const actual = browser.getTitle()

        assert.strictEqual(expected, actual)
    })
})
```


Defaultně podporovaný reporter je `dot`.
```
reporters: ['dot']
```

# Čáj

https://www.chaijs.com/

Chai je assertion knihovna, která stejně jako node.js assertion knihovna, umožňuje porovnávat expected a actual hodnoty. Její výhodou je však větší počet assertions (https://www.chaijs.com/api/assert/). Také umožňuje 3 různé varianty stylů assertů - `should`, `expect` a `assert`. Ty umožňují psát testy ve formátu, který je pro daný problém nejvhodnější.

Nainstalujeme

`npm install --save-dev chai`

A jak se změní náš kód?
```
let assert = require('chai').assert

describe('Mall.cz homepage', () => {
    it('should have the right title', () => {
        browser.url('./')

        const expected = 'MALL.CZ – bílé zboží, elektronika, PC, outdoor, hobby, hračky, kosmetika, chovatelské potřebi'
        const actual = browser.getTitle()

        assert.strictEqual(expected, actual)
    })
})
```

Nakonec si chai přidáme do configu:
```
before: function (capabilities, specs) {
    assert = require('chai').assert
}
```

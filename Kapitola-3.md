# Píšeme druhý test (abychom jej následně celý rozcupovali)

```javascript
const assert = require('assert')

describe('Daily deal', () => {
    it('should add correct item in the cart', () => {
    	const dailyDealButton = $('.daily-deal-2__add-to-cart .btn--primary')
        const productTitle = 'Trust Arys Compact RGB (23120)'
        const widgetDrawerBtn = $('#navigation-widget > ul > li:nth-child(4) > div.drw--down.drw--right #proceed-to-cart')
        const cartTitleElement = $('//*[@id="cart-overview"]/div[2]/div/div[2]/div[2]/article/div[1]/div[1]/div/h3/a')

    	// Go to HP
        browser.url('./')

        dailyDealButton.waitForExist(5000)

        // Add to cart from daily deal box
        dailyDealButton.click()

        widgetDrawerBtn.waitForClickable({ timeout: 5000 })

        widgetDrawerBtn.click()

        cartTitleElement.waitForExist(5000)

        // Compare values via assert - actual vs. expected
        assert.strictEqual(cartTitleElement.getText(), productTitle)
    })
})
```

# Page Object

Ačkoliv by název mohl vést k domnění, že Page Object se bude vztahovat pouze na stránky jako celek, jedná se o návrhový vzor, vztahující se především k důležitým komponentám stránek.
Slouží k obalení (zabstraktnění) stránky/komponenty, díky čemuž dovoluje libovolně manipulovat s HTML elementy skrze něj a nikoliv jakožto součást testu. Veškeré selektory a instrukce, specifické pro danou stránku/komponentu, by měly být uloženy právě jako Page object. Díky tomu nedochází k nežádoucí závislosti testů na designu stránky, který se může měnit.

Více najdete zde: https://martinfowler.com/bliki/PageObject.html

## Píšeme první Page object

Z rootu našeho projektu si vytvoříme nový adresář `pageobjects`
```
mkdir -p ./test/pageobjects
```

A zde si vytvoříme soubor `page.js`
```
touch ./test/pageobjects/page.js
```

Tímto jsme si vytvořili hlavní Page object, ze kterého budou ostatní dědit. Umisťujeme sem generické selektory a metody.

Doplníme obsah
```javascript
// Vytvoříme třídu pro každou stránku/komponentu
class Page {
    // Vytvoříme metodu open s parametrem path => url stránky bude součástí jejího page objektu, namísto konkrétního testu
    open(path) {
        browser.url(path)
    }
}

// Exportujeme instanci Page object
export default Page
```

Třídy byly do javascriptu uvedeny s ES6. Jsou to speciální funkce, které fungují jako konstrukt pro objektově orientované programování.

Zajímají vás třídy v javascriptu? Čtěte více zde:
https://javascript.info/class
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes

## Import a Export

https://javascript.info/import-export

## Daily deal jako Page object

Konkrétní komponenta `Daily deal`, kterou najdeme na HP bude mít také svůj vlastní Page object.

Vytvoříme soubor
```
touch ./test/pageobjects/daily-deal.page.js
```

A vytvoříme třídu `DailyDeal`
```javascript
// dědíme z hlavní Page třídy
import Page from '../pageobjects/page'

// a extendujeme ji novou třídou DailyDeal
class DailyDeal extends Page {
    // gettery pro selektor
    get addToCartBtn() {
        return $('.daily-deal-2__add-to-cart .btn--primary')
    }
    
    get addedToCartBtn() {
        return $('.daily-deal-2__add-to-cart .btn--primary.action--done')
    }
    
    // metoda pro přidání do košíku
    addProductToCart() {
        this.addToCartBtn.waitForDisplayed()
        this.addToCartBtn.click()
        this.addedToCartBtn.waitForDisplayed()
    }
}

export default new DailyDeal()
```

A použijeme abstrakci v našem testu
```javascript
// nejprve importujeme Page object
import DailyDeal from '../pageobjects/daily-deal.page'
```

```javascript
// nejprve importujeme Page object
import DailyDeal from '../pageobjects/daily-deal.page'
```

```javascript
// následně využijeme metodu pro přidání do košíku
DailyDeal.addProductToCart()
```

# Destructuring

Destructuring assignment syntax umožňuje uložení vlastností objektu či hodnot pole do proměnných.

Jak to vypadá bez této featury?
```javascript
let myArray = [1, 2, 3];

let a = myArray[0];
let b = myArray[1];
let c = myArray[2];
```

A jak s ní?
```javascript
let myArray = [1, 2, 3];

let [a, b, c] = myArray; // a=1, b=2, c=3
```

A s defaultními hodnotami?
```javascript
let myArray = [1];
// not enough values in an array
let [a, b, c] = myArray; // a=1, b=undefined, c=undefined
```

```javascript
let myArray = [1];
// use fallback values
let [a=2, b=4, c=6] = myArray; // a=1, b=4, c=6
```

Přeskočení
```javascript
let myArray = [1, 2, 3];
let [a, , b] = myArray; // a=1, b=3
```

Spread operator
```javascript
let myArray = [1, 2, 3, 4, 5, 6];
let [a, b, ...others] = myArray; // a=1, b=2, others = [3, 4, 5, 6]
```

https://www.vojtechruzicka.com/destructuring-javascript/
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment

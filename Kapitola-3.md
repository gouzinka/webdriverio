# Page Object

Ačkoliv by název mohl vést k domnění, že Page Object se bude vztahovat pouze na stránky jako celek, jedná se o návrhový vzor, vztahující se především k důležitým komponentám stránek.
Slouží k obalení stránky/komponenty do API, jež dovoluje libovolně manipulovat s HTML elementy skrze něj a nikoliv jakožto součást testu. Veškeré selektory a instrukce, specifické pro danou stránku/komponentu, by měly být uloženy právě jako page object. Díky tomu nedochází k nežádoucí závislosti testů na designu stránky, který se může měnit.

Více najdete zde: https://martinfowler.com/bliki/PageObject.html

## Píšeme první page object

Z rootu našeho projektu si vytvoříme nový adresář pageobjects
```
mkdir -p ./test/pageobjects
```

A zde si vytvoříme soubor
```
touch ./test/pageobjects/page.js
```

Tímto jsme si vytvořili hlavní Page object, ze kterého budou ostatní Page objects dědit. Umisťujeme sem generické selektory a metody.

Doplníme obsah
```
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

## Daily deal jako Page object

Konkrétní komponenta `Daily deal`, kterou najdeme na HP bude mít také svůj vlastní Page object.
Vytvoříme proto soubor
```
touch ./test/pageobjects/page.js
```

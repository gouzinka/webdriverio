# Instalace

Nejprve je potřeba mít nainstalovaný Node.js a to ve správné verzi.
Pro aktuální verzi WDIO je potřeba v8.11.2 a vyšší.
Verzi lze zjistit příkazem
```
node -v
```

Potřebuješ-li pro různé projekty různé verze Node.js, doporučuji instalovat Node Version Manager
https://github.com/nvm-sh/nvm (mac/linux)
https://github.com/coreybutler/nvm-windows (win)

Nemáš-li Node.js nainstalovaný, postupuj podle oficiální dokumentace https://nodejs.org/en/

A nyní již k webdriverio:

```
mkdir webdriver-io && cd webdriver-io
npm init -y
npm i --save-dev @wdio/cli
```

Testy můžeš spouštět i přímo v prohlížeči (a třeba je i sdílet) http://try.webdriver.io/

# Konfigurace

Dokumentace: https://webdriver.io/docs/configurationfile.html

```
./node_modules/.bin/wdio config -y
```

Dopadlo-li vše v pořádku, najdeš v projektu soubor

```
wdio.conf.js
```

Zde si můžeš všimnout Node.js `exports` globální proměnné. Tento objekt je připravený pro přidávání vlastností. WebdriverIO se dívá na vlastnost `config`.
V nastavení si všimneme:
 - specs - cesta k našim testům
 - capabilities.browser - prohlížeč pro spouštění testů [array - můžeme definovat vícero prohlížečů pro test]
 - framework - název frameworku pro psaní testů
 - mochaOpts - behaviour driven development style (bdd)
 
# Píšeme první test
Vytvoříme složku pro naše testy, dle konfigurace

```
mkdir -p ./test/specs
```

A v adresáři vytvoříme soubor
```
touch ./test/specs/example.js
```

A vložíme kód
```
const assert = require('assert')

describe('Mall.cz homepage', () => {
    it('should have the right title', () => {
        browser.url('https://www.mall.cz')
        const title = browser.getTitle()
        assert.strictEqual(title, 'MALL.CZ – bílé zboží, elektronika, PC, outdoor, hobby, hračky, kosmetika, chovatelské potřeby')
    })
})
```

Nakonec test spustíme
```
./node_modules/.bin/wdio wdio.conf.js
```

Tento zápis si můžeme dovolit s config sync: true.

Čeho si všimneme? Webdriverio testrunner nám zpřístupní browser proměnnou.
https://webdriver.io/docs/browserobject.html

To se hodí, pokud chceme například identifikovat, že test běží na mobilním zařízení.
Vzpomínáte na wdio.conf.js? Nastavení `capabilities` může vypadat i takto:

```
capabilities: {
    platformName: 'iOS',
    app: 'net.company.SafariLauncher',
    udid: '123123123123abc',
    deviceName: 'iPhone',
    // ...
}
```

A objekt `browser` se zachová:
```
console.log(browser.isMobile) // outputs: true
console.log(browser.isIOS) // outputs: true
console.log(browser.isAndroid) // outputs: false
```
Testy tak můžeme vytvářet pro konkrétní typ zařízení.

# Poznejme Mocha
Mocha je javascriptový test framework, který nabízí množství benefitů. Mezi ty patří lepší organizace, lepší error reporting, ale i funkcionality navíc, jakými jsou pre a post-test hooks.

Testy jsou organizované za pomoci `describe` a `it` funkcí. `Describe` je použité pro seskupení sady testů podle části (featury), jež testují. `It` definuje konkrétní test k běhu. Typicky je uvnitř `describe` vnořeno několik `it` funkcí. V některých případech, pro větší přehlednost v hiearchii testů, je uvnitř `describe` zanořeno několik dalších `describe` funkcí.

 * `describe` je funkce, jež přijímá 2 parametry - název feature a funkci, jež obsahuje kód, sloužící k otestování dané feature
 * `it` je funkce, jež přijímá 2 parametry - název specifického testu a funkci, jež obsahuje samotný test
 
# Příkazy

Příkazy jsou jednoduchý způsob, jak přetížit/přidat konfiguraci při spuštění.
https://webdriver.io/docs/clioptions.html

Chceme-li změnit baseUrl:
```
./node_modules/.bin/wdio --baseUrl=https://www.mall.cz.test/
```
V tuto chvíli na v5 zabugované :(

Pro debuggování se může hodit:
```
./node_modules/.bin/wdio --logLevel=debug
```

Jak vlastně WDIO funguje?
![Webdriverio](https://i.imgur.com/0TyF0pvl.png)

- WDIO požádá Selenium o prohlížeč k použití - session
- pošle post request s daty na selenium server
- selenium server přijme požadavek a inicializuje session na základě dostupných dat

WDIO představuje javascript interface pro zasílání příkazů seleniu skrze REST API volání. Selenium se stará o automatizaci v prohlížeči.
WDIO posílá HTTP požadavky na endpointy na selenium serveru.

1. WDIO pošle příkazy seleniu k běhu
2. Selenium je spustí a výsledku pošle zpět WDIO

Příklad:
```
COMMAND getTitle()
// kontaktuje title endpoint
[GET] http://127.0.0.1:4444/session/011d5c4b7f9cbbeba7fb8fa87e063b0c/title
// navrácená data
RESULT MALL.CZ – bílé zboží, elektronika, PC, outdoor, hobby, hračky, kosmetika, chovatelské potřeby
```

# Vlastní argumenty

Vytvořením dočasné proměnné prostředí (environmental variable), můžeme modifikovat běh skriptu.
Node nám umožňuje přístup k proměnným prostředí skrze `process.env` objekt. Ukážeme si jak na to.

Upravíme config, hodnotu baseUrl, přesuneme do proměnné:
```
let baseUrl = 'https://www.mall.cz'

if (process.env.SERVER === 'test') {
    baseUrl = 'https://www.mall.cz.test'
}
```

```
baseUrl: baseUrl
```
A upravíme test
```
browser.url('./')
```

Spustíme
```
SERVER=test ./node_modules/.bin/wdio wdio.conf.js
```

# NPM skripty
https://docs.npmjs.com/misc/scripts

NPM skripty slouží ke zjednodušení příkazů.
Existují 2 typy:
1. supported scripts - běžně používané příkazy pro npm moduly (spouštíme pomocí `npm start | stop | test`... - zápis zkratkou bez `run`)
2. custom scripts - skripty s vlastními názvy (spouštíme pomocí `npm run <nazev>`)

Tyto skripty definujeme v souboru `package.json`:

```
// wdio wdio.conf.js - název souboru můžeme ommitovat, wdio jej bere defaultně
"scripts": {
  "test": "wdio"
}
```
Nyní můžeme testy spouštět příkazem `npm test`.

Budeme-li nyní chtít použít příkazy při spuštění, musíme je uvádět v tomto tvaru.
`npm test -- --logLevel=debug` tento zápis npm říká, aby všechny argumenty uvedené za dvojíma pomlčkama přidal k příkazu, který skript vykonává. V našem případě tedy `wdio --logLevel=debug`

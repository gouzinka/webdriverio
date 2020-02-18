# Práce s poli:
https://sdras.github.io/array-explorer/

# Práce s objekty:
https://objectexplorer.netlify.com/

# Práce s řetězci:

```
let string = 'This is string.'
```

Vytvořením stringu, získáme proměnnou, která je instancí string objectu. Díky tomu máme k dispozici velké množství vlastností a metod pro práci s nimi.
Kompletní výčet najdeme zde: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String

Jaké jsou však užitečné?

## Délka

```
let string = 'Webdriverio'
string.length // 11
```

## Získání znaku

Pomocí notace hranatých závorek můžeme přistupovat k jednotlivým znakům řetězce.
```
let string = 'Webdriverio'
string[0] // 'W' - první pozice
string[string.length-1] // 'o' - poslední pozice (indexujeme od 0, proto odečítáme)
```

## Vyhledání subřetězce

```
let string = 'Webdriverio'
string.indexOf('driver') // 3 - substring začíná na pozici 3 (0, 1, 2, 3 - 4. znakem)
string.indexOf('codeception') // -1 - substring nenalezen
```

## Extrakce subřetězce

```
let string = 'Webdriverio'
string.slice(0,3) // 'Web' - první parametr říká od jaké pozice extrahujeme, druhý říká pozici před kterou chceme extrahovat
```

```
let string = 'Webdriverio'
string.slice(3) // 'driverio' - první parametr říká od jaké pozice extrahujeme (včetně), druhý říká pozici před kterou chceme extrahovat
```

## Konvertování - upper, lower

```
let string = 'Webdriverio'
string.toLowerCase() // 'webdriverio'
string.toUpperCase() // 'WEBDRIVERIO'
```

## Nahrazování

```
let string = 'Webdriverio'
string = string.replace('Web','Chrome').replace('io','') // 'Chromedriverio' - pozor, je nutné přiřazení do proměnné (v konzoli funguje i bez)
```




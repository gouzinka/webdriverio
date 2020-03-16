# Loops and Iteration

## 'For' loop

Nejzákladnější forma iterace.

```
const orderNumbers = ['1548526', '1548527', '1548531', '1548542']

for (let i = 0; i < orderNumbers.length, i++) {
  console.log(`Číslo objednávky je: ${orderNumbers[i]}`)
}
```

'For' loop používá `counter`, u kterého nejprve přiřadíme iniciální hodnotu:

`let i = 0` (initial expression)
`i < orderNumbers.length` (condition)
`i++`

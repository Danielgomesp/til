## Map

O map percorre um array e cria um novo array com o resultado.

*Se não for necessário uma nova array, use o foreach().*

```
const numbers = [20, 30, 40, 50]

function doubleNumber(num){
  return num * 2
}

numbers.map(doubleNumber)
```
## Filter

Retorna um novo array somente com os elementos que satisfazem o filtro.

```
const ages = [26, 16, 56, 80, 76, 15];

function selectElderly(age) {
  return age >= 60;
}

ages.filter(selectElderly);
```

## Reduce

```
array.reduce( (prevVal, elem, index ) => {
    
    cool stuff here...

}, initialValue );
```
- prevVal: Valor aculumado. Por exemplo, o resultado de uma soma.
- elem: Valor do elemento atual.
- index: Valor do indice atual. (optional)

Exemplo:
```
const numbers = [ 1, 2, 3, 4, 5 ]

function sum(total, number) {
  return total + number
}

numbers.reduce(sum, 0)
```
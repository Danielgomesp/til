Como diz Mary Rose Cook:
> "Functional code is characterised by one thing: the absence of side effects"


## Pure Function

Para evitar efeitos colaterais, a função não deverá contar com dados que estejam fora do seu escopo e de igual modo também não deverá alterar dados fora da mesma. 

Exemplo: 

**bad**
  ```
  let name = 'Daniel'

  function greeting() {
    console.log( 'Hello' + name )
  }
  ```
  Vemos que a função recebe a variável 'name' de fora.
  Além disso, ele da o resultado no console, fora do seu escopo.

  **good**
  ```
  function greeting(name){
    return 'Hello' + name
  }
  ```

  Agora recebemos o 'name' via parametro e damos o retorno via return.


## Don't ever iterate over lists

  Evite o uso de 'for' ou 'while'. No lugar, use map, reduce, filter.

  O map 'mapeia' o array original permitindo que para cada item possamos executar uma função criando um novo array com os resultados. O map não altera o array original.

  Exemplo:
  ```
  const numbers = [1, 2, 3, 4]
  const newNumbers = numbers.map( num => num * 2 )
  ```

  O resultado será um novo array 'newNumbers' com o conteúdo multiplicado por 2.

## Declarative, not imperative

*Como deve ser feito* x *O que deve ser feito*

Resumidamente, na programação imperativa nós dizemos explicitamente cada passo que a função deverá executar. Ou seja, nós dizemos ao computador como alguma coisa deve ser feita. 

Enquanto na declarativa, nós dizemos o que queremos. Nesse paradigma nós descrevemos o que ele faz e não como seus procedimentos funcionam.

Imperative e.g.
```
const numbers = [2,4,6,8]
let total = 0;

for (let i = 0; i < numbers.length; i++){
	total += numbers[i]
}
```

Declarative e.g.
```
const numbers = [2,4,6,8]

numbers.reduce((previous, current) => {
  return previous + current
})
```


## Use functions

A programção pode se tornar mais declarativa se juntarmos o código dentro de funções.
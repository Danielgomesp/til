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

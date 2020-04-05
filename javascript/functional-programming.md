Como diz Mary Rose Cook:
> "Functional code is characterised by one thing: the absence of side effects"


E para evitar efeitos colaterais, usamos o conceito de **Pure Function**. 

Ou seja, a função não deverá contar com dados que estejam fora do seu escopo e de igual modo também não deverá alterar dados fora da mesma. 

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

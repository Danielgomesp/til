Como sabemos, não podemos usar if/else dentro do JSX. Isso faz do ternário nosso grande amigo.
Porém uma característica do ternário é retornar um valor para **true** ou outro valor para **false**.
Acontece que nem sempre queremos retornar algo para o **false** e acabamos escrevendo o código assim:
```
true ? '<div> Exibe se for verdadeiro </div>' : ''
```
Ou seja, dizemos ao ternário para retornar um "nada" **''** quando for falso.

Há uma maneira mais elegante de trabalhar nesses casos que é utilizando o **Short Circuit Evaluation**

Com ele verificamos somente se o valor é verdadeiro ou somente se ele é falso.
&& - Para verificar se é verdadeiro
|| - Para verificar se é falso.

Exemplo:
```
true && '<div> Exibe se for verdadeiro </div>'
``
Pronto, só isso. 
Nesse caso, se a condição for falsa, ele retornará falso.

O mesmo acontece, de maneira invertida, com o usso de ||

```
false || '<div> Exibe se for falso </div>'
```

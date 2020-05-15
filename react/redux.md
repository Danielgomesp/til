**disclaimer:** Esse assunto é complexo e eu ainda estou estudando-o. Por esse motivo esse documento, assim como meus estudos sobre o assunto, ainda não estão concluídos e certamente sofrerá alterações. Considere o conteúdo abaixo como um Work in Progress.

## O que é o Redux

É uma implementação do Flux. Uma library de gerenciamento de estado. Assim como a [Context API](../react/context.md), ele também resolve o problema de "prop-drilling", porém vai muito mais além. Podemos usar o Redux para centralizar as regras de negócio da nossa aplicação em um único lugar.



## Como ele funciona?

Ele tem uma definição clara de como um estado deverá ser alterado e lido.

### Store
Aqui fica armazenado todos os states da aplicação. É como um objeto javascript gigante.
Para os componentes, ele é somente leitura. Somente um reducer poderá alterar o store.
```
const store = createStore(reducer);

```

### Action
Ele é um pacote de informação.  Algo como "adicione ingrediente" ou "remova aluno". Ele poderá conter um payload. Por exemplo, precisamos dizer qual o ingrediente queremos adicionar.

A action não contém lógica, ele não sabe como adicionar a informação, ela é só um mensageiro. Uma função que retona um objeto.

A razão disso tudo é disponibilizar o estado para os componentes e permití-los alterar esses estados.
Para isso, os **componentes** precisarão usar uma action. Componentes nunca acessarão a storage diretamente.

Quem realmente irá alterar a store é o reducer.

```
store.dispatch({type: 'ADD_COUNTER', value=1 })
```

### Reducer

Ele irá checar o tipo da action que o acionou e então identificar o código para esse tipo de ação no reducer.

Deve ser uma pure-function que receberá a action e o antigo state e atualizará o state. Não pode ser uma função assíncrona. 
Quando ele atualizar o state, isso será feito de maneira imutável, ou seja, ele criará um novo estado baseado no antigo, porém um novo objeto. 

```
function rootReducer(state = initialState, action){
    if (action.type === 'ADD_COUNTER'){
        return {
            ..state,
            couter: state.counter + action.value
        };
    }
}
```

### Subscription

A storage aciona todas as **subscriptions** sempre que o estado muda. O que devemos fazer é inscrever nossos componentes à essas subscriptions, assim elas receberão o estado via props sempre que ele for atualizado.

## Mão na massa!

- Adicinamos o Redux ao projeto:

```
yarn add redux react-redux@next
```
- Criamos o arquivo de configuração do Redux

No mesmo nível da pasta de componentes, criamos uma pasta "store" e um arquivo "index.js" dentro dela.

index.js:
```
import { createStore } from 'redux';

const store = createStore( courses );  //É necessário passar um reducer como parâmetro. Aqui passei o 'courses'.

export default store;
```

configuração do Reducer:
```
const INITIAL_STATE = {
    data: [
        'Course 1',
        'Course 2',
    ],
};

function courses (state = INITIAL_STATE, action) {
    switch (action.type) {
        case 'ADD_COURSE' :
            return { ...state, data: [..state.data, action.title] };
        default :
            return state;
    }
}
```




## Atenção

Esse documento ainda está sendo construído. Em breve será adicionado aqui um exemplo prático com um repositório para consulta assim como fiz com o [Context](../react/context.md).
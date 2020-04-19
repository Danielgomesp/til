Uma das grandes vantagens de usar Context Api é que isso nos salva do famoso "Prop-Drilling", que é a tecnica de passar variáveis para sub-componentes. A ideia principal é [functional programming](../javascript/functional-programming.md), onde passamos os parâmetros para próximas funções e assim por diante.

A Context API faz o mesmo papel do Redux.

Criei um exemplo usando Context API nesse repositório [aqui](https://github.com/Danielgomesp/context) e irei usá-lo para exemplificar esse tópico.

No nosso exemplo, temos um contador de segundos em um elemento [Counter](https://github.com/Danielgomesp/context/blob/master/src/components/Counter/index.js). Ele faz uso de estado para saber o tempo que você está na página.

Criamos um outro elemento [Mirror](https://github.com/Danielgomesp/context/blob/master/src/components/Mirror/index.js) que somente exibe lê o estado e exibe a informação.

**O problema**

Como fazer o **Mirror** ter acesso ao estado do **Counter**? Usando **Context**.

Basicamente, vou criar uma pasta chamada **context** e nela criar um arquivo para a configuração.
Criei o arquivo [Counter.js](https://github.com/Danielgomesp/context/blob/master/src/context/Counter.js) com o seguinte código:

1 - Importo **createContext** para criar o contexto, **useState** para gerenciar o estado e **useContext** porque eu vou exportar um hook diretamente desse arquivo, o que facilitará nossa vida no futuro.

```
import React, { createContext, useState, useContext } from 'react';
```

2 - Vou instanciar o createContext em uma constante.

```
const CountContext = createContext()
```

3 - Agora Vou exportar uma função **Provider**. (*A boa prática ao criar uma nova implementação é utilizar [componentes funcionais](javascript/functional-programming.md) ao invés de classes*).

O Provider é o provedor dos dados para os seus filhos, os consumers.

Nela eu declaro os estados, e retorno o provedor do contexto passando o estado por parametro dentro de uma prop. Esses valores ficarão disponíveis para todos os filhos.

```
export function CounterProvider({ children }) {
  const [seconds, setSeconds] = useState(0)

  return (
    <CountContext.Provider value={{ seconds, setSeconds }}>
      {children}
    </CountContext.Provider>
  );
}
```
 4 - Finalmente, vou exportar uma função que funcionará como hook para facilitar a nossa vida na hora de usar o context nos componentes filhos.

 Obs: *o nome da função deverá começar com  "**use**", assim como qualquer hook *

 primeiro eu defino uma constante recebendo o contexto;
 Depois eu uso [desestruturação](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) para receber somente os valores que me interessam de dentro da constante, que no nosso caso são *seconds* e *setSeconds*;
 Por último eu retorno esses valores para que eles fiquem acessíveis.
 ```
 export function useCount() {
  const context = useContext(CountContext)
  const { seconds, setSeconds } = context

  return { seconds, setSeconds }
}
 ```

 5 - Agora é a hora de usar o **hook** que criamos.
 Vamos importá-lo no componente que queremos conceder acesso ao estado criado no Context.

 ```
 import { useCount } from '../../context/Counter'
 ```
 E usar novamente a desestruturação para retirar do useCount as nossas variáveis que dão acesso ao estado:
```
const { seconds, setSeconds } = useCount()
```
Agora já podemos usá-lo livremente no nosso componente.

6 - Último passo:
Vá ao componente pai, que no meu caso é o APP, importe o Provider e adicione-o como componente envolvendo todos os demais.
```
import { CounterProvider } from "./context/Counter";

function App() {
  return (
    <CounterProvider>
      <div className="App">
        <Counter />
        <Mirror />
      </div>
    </CounterProvider>
  );
}
```

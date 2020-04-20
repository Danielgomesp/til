A partir do [Preact X](https://preactjs.com/), é possível utilizar styled-components em sua última versão sem problemas.
A única coisa que devemos nos certificar de fazer é criar um alias corretamente.

Basta entrar no arquivo [package.json](https://github.com/Danielgomesp/preact-boilerplate/blob/master/package.json) e criar um alias confome o código abaixo:
```
"alias": {
    "react": "preact/compat",
    "react-dom": "preact/compat"
  }
```
Caso queira começar um projeto novo usando essas tecnologias, basta clonar esse repositório [aqui](https://github.com/Danielgomesp/preact-boilerplate) que eu criei para facilitar nossa vida.

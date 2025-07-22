# DOM (Document Object Model) - Conceitos Teóricos

## O que é DOM(Document Object Model)?

É uma `interface` que representa documentos HTML e XML através de objetos. COm ela é possível manipular a estrutura, estilo e conteúdo destes documentos.

``` javascript
console.log(window);
//window é o objeto global do browser
// possui diferentes métodos e propriedades

window.innerHeight;
```

>*Ao inspecionar elemento com o Chrome(ou qualquer outro navegador), o que vemos é a representação oficial do DOM*

### Window e Document
São os objetos principais do DOM, boa parte da manipulação é feita através dos seus métodos e propriedades.

``` javascript
window.alert('Isso um alerta');
alert('Isso e um alerta'); // Funciona

document.querySelector('h1'); // Seleciona o primeiro h1
document.body; // Retorna o body
```
>*`window` é o objeto global, por isso não precisamos chamar ele na frente dos seus métodos e propriedades.*

### Node
Toda tag html é representada pelo objeto `Element` e por isso herda os seus métodos e propriedades. `Element` é um tipo de objeto `Node`.

``` javascript
const titulo = document.querySelector('h1');
titulo.innerText; // Retorna texto
titulo.classList; // Retorna as classes
titulo.id; // Retorna o id
titulo.offsetHeight; // Retorna a altura do elemento

titulo.addEventListerner('click', callback);
// ativa a funcao callback ao clicar no titulo
```


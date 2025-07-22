# DOM (Document Object Model)

## Selecão de Elementos?

### ID
`getElementByID` seleciona e retorna elementos do DOM.

``` javascript
// Seleciona pelo ID
const animaisSection = document.getElementById('animais');
const animaisSection = document.getElementById('contato');

//Retorna null caso nao exista
const naoExiste = document.getElementById('teste');
```

### CLASS e TAG
`getElementsByClassName` e `getElementsByTagName` selecionam e retornam uma lista de elementos do DOM. A lista retornada está `ao vivo`, significa que se elementos forem adicionados, ela sera automaticamente atualizada.

``` javascript
// Seleciona pela CLASS, retorna uma HTMLCollection
const gridSection = document.getElementsByClassName('grid-section');
const contato = document.getElementsByClassName('grid-section contato');

// Seleciona todas as UL`s, retorna uma HTMLCollection
const ul = document.getElementsByTagName('ul');

//Retorna o primeiro elemento
console.log(gridSection[0]);
```

### SELECTOR GERAL ÚNICO
`querySelector` retorna o primeiro elemento que combinar com o seu seletor `CSS`.

``` javascript
const animais = document.querySelector('.animais');
const contato = document.querySelector('#contato');
const ultimoItem = document.querySelector('.animais-lista li:last-child');
const linkCSS = document.querySelector('[href^="https://"]');
const primeiroUl = document.querySelector('ul');

// Busca dentro do Ul apenas
const navItem = primeiroUl.querySelector('li')
```

### SELECTOR GERAL LISTA
`querySelectorAll` retorna todos elementos compativeis com o seletor `CSS` em uma NodeList.

``` javascript
const gridSection = document.querySelectorAll('.grid-section');
const listas = document.querySelectorAll('ul');
const titulos = document.querySelectorAll('.titulo');
const fotosAnimais = document.querySelectorAll('.animais-lista img');

// Retorna o segundo elemento
console.log(gridSection[1]);
```
>*Diferente do getElementsByClassName, a lista aqui é estática*

## HTMLCollection vs NodeList
A diferenca esta nos metodos e propriedades de ambas. Alem disso a NodeList retornada com querySelectorAll e estatica.

``` javascript
const titulo = document.querySelector('.titulo');
const gridSectionHTML = document.getElementsByClassName('grid-section');
const gridSectionNode = document.querySelectorAll('.grid-section');

titulo.classList.add('grid-section');

console.log(gridSectionHTML); // 4 itens
console.log(gridSectionNode); // 3 itens
```

### ARRAY-LIKE
`HtmlCollection` e `NodeList` sao array-like, parecem uma array mas nao sao. O metodo de Array `forEach()` por exemplo, nao existe apenas em `NodeList`.

>*É possível transformar array-like em uma Array real, utilizando o método `Array.from(gridSection)`*

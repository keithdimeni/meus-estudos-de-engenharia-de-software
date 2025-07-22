# DOM (Document Object Model)

## ForEach e Arrow Function

### FOREACH
Constantemente vamos selecionar uma lista de itens do `DOM`. A melhor forma para interagirmos com os mesmos é utlizando o método `forEach`.

``` javascript
const imgs = document.querySelectorAll('img');

imgs.forEach(function(item){
  console.log(item);
});
```

### PARÂMETROS DO FOREACH
O primeiro parâmetro é o callback, ou seja, a função que será ativada a cada item. Essa função pode receber três parâmetros. `valorAtual`, `index` e `array`.

``` javascript
const imgs = document.querySelectorAll('img');

imgs.forEach(function(valorAtual, index, array){
  console.log(valorAtual); // o item atual no loop
  console.log(index); // o número do index
  console.log(array); // a Array completa
});
```

### FOREACH E ARRAY
`forEach` é um método de Array, alguns objetos array-like possuem este método. Caso não possua, o ideal é transformá-los em uma array.

``` javascript
const titulos = document.getElementsByClassName('titulo');
const titulosArray = Array.from(titulos);

titulosArray.forEach(function(item){
  console.log(item);
});
```

### ARROW FUNCTION
Sintaxe curta em relação a `function expresion`. Basta remover a palavra function e adicionar a fat arrow `=>` após argumentos.

``` javascript
const imgs = document.querySelectorAll('img');

imgs.forEach((item) => {
  console.log(item);
});
```

### PARÂMETROS E PARÊNTESES

``` javascript
const imgs = document.querySelectorAll('img');

// parâmetro único não precisa de parênteses
imgs.forEach(item => {
  console.log(item);
});

// multiplos parâmetros precisam de parênteses
imgs.forEach((item, index) => {
  console.log(item, index);
});

// sem parâmetro precisa dos parênteses, mesmo vazio
let i = 0;
imgs.forEach(() => {
  console.log(i++);
});
```
>*É melhor utlizar os parênteses*

### RETURN
É possível omitir as chaves `{}` para uma função que retorna uma linha.

``` javascript
const imgs = document.querySelectorAll('img');

imgs.forEach(item => 
  console.log(item)
);

imgs.forEach(item => console.log(item));
```
>*Não é permitido fechar a linha com `;`*
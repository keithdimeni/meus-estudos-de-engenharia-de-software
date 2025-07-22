# DOM (Document Object Model)

## Eventos

### ADDEVENTLISTENER
Adiciona uma função ao elemento, esta chamada de `callback`, que será ativada assim que certo `evento` ocorrer neste elemento.

``` javascript
const img = document.querySelector('img');

// elemento.addEventListener(event, callback, options)
img.addEventListener('click', function() {
  console.log('Clicou');
})
```
>*O terceiro parâmetro é opcional*

### CALLBACK
É boa prática separar a função de callback do addEventListener, ou seja, declarar uma função ao invés de passar diretamente uma função anônima.

``` javascript
const img = document.querySelector('img');
function callback() {
  console.log('Clicou');
}

img.addEventListener('click', callback); // 🚀
img.addEventListener('click', callback()); // undefined
img.addEventListener('click', function() {
  console.log('Clicou');
})
img.addEventListener('click', () => {
  console.log('Clicou');
})
```

### EVENT
O primeiro parâmetro do callback é referente do evento que ocorreu.

``` javascript
const img = document.querySelector('img');

function callback(event) { // event
  console.log(event);
}

img.addEventListener('click', callback);
```
>*Geralmente utizam `e` como nome do parâmetro*

#### PROPRIEDADES DO EVENT

``` javascript
const animaisLista = document.querySelector('.animais-lista');

function executarCallback(event) {
  const currentTarget = event.currentTarget; // this
  const target = event.target; // onde o clique ocorreu
  const type = event.type; // tipo de evento
  const path = event.path;
  console.log(currentTarget, target, type, path);
}

animaisLista.addEventListener('click', executarCallback);
```

### EVENT.PREVENTDEFAULT()
Previne o comportamento padrão do evento no navegador. No caso de um link externo, por exemplo, irá previnir que o link seja ativado.

``` javascript
const linkExterno = document.querySelector('a[href^="http"]');

function clickNoLink(event) {
  event.preventDefault();
  console.log(event.currentTarget.href);
}

linkExterno.addEventListener('click', clickNoLink);
```

### THIS
A palavra chavse `this` ´euma palavra especial de Javascript, que pode fazer referência a diferentes objetos dependendo do contexto. No caso de eventos, ela fará refência ao elemento em que addEventListener foi adicionado.

``` javascript
const img = document.querySelector('img');

function callback(event) {
  console.log(this); // retorna a imagem
  console.log(this.getAttribute('src'));
}

img.addEventListener('click', callback);
```
>*Geralmente igual ao event.currentTarget*

### DIFERENTES EVENTOS
Existem diversos eventos com `click`, `scroll`, `resise`, `keydown`, `keyup`, `mouseenter`, e mais. Eventos podem ser adicionados a diferentes elementos, como `window`, e `document` também.

``` javascript
const h1 = document.querySelector('h1');

function callback(event) {
  console.log(event.type, event);
}

h1.addEventListener('click', callback);
h1.addEventListener('mouseenter', callback);
window.addEventListener('scroll', callback);
window.addEventListener('resize', callback);
window.addEventListener('keydown', callback);
```
>*link: https://developer.mozilla.org/en-US/docs/Web/Events*

### KEYBOARD
Podemos adicionar atalhos para facilitar a navegação no seu site, através de eventos do `keyboard`.

``` javascript
function handleKeyboard(event) {
  if(event.key === 'a')
    document.body.classList.toggle('azul');
  else if(event.key === 'v')
    document.body.classList.toggle('vermelho');
}

window.addEventListener('keydown', handleKeyboard);
```

### FOREACH E EVENTOS

O método `addEventListener` é adicionado à um único elemento, então é necessário um loop entre elementos de uma lista para adicionarmos à cada um deles.

``` javascript
const imgs = document.querySelectorAll('img');

function imgSrc(event) {
  const src = event.currentTarget.getAttribute('src');
  console.log(src);
}

imgs.forEach((img) => {
  img.addEventListener('click', imgSrc);
});
```
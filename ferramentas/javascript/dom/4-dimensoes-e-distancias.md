# DOM (Document Object Model)

## Dimensões e Distâncias

### HEIGHT E WIDTH
Estas são propriedades e métodos dos objetos `Element` e `HTMLElement`, a maioria delas são Read Only.

``` javascript
const section = document.querySelector('.animais');

section.clientHeight; // height + padding
section.offsetHeight; // height + padding + border
section.scrollHeight; // height total, mesmo dentro de scroll
```
>*Mesma coisa par Width, `clientWidth`...*

### OFFSETTOP E OFFSETLEFT

``` javascript
const section = document.querySelector('.animais');

// Distância entre o topo do elemento e o topo da página
section.offsetTop;

// Distância entre o canto esquerdo do elemento
// e o canto esquerdo da página
section.offsetLeft;
```

### GETBOUNDINGCLINETRECT()
Método que retorna um objeto com valores de width, height, distâncias do elemento e mais.

``` javascript
const section = document.querySelector('.animais');

const rect = section.getBoundingClientRect();
rect.height; // height do elemento
rect.width; // width do elemento
rect.top; // distância entre o topo do elemento e o scroll
```

### WINDOW

``` javascript
window.innerWidth; // width do janela
window.outerWidth; // soma dev tools também
window.innerHeight; // height do janela
window.outerHeight; // soma a barra de endereço

window.pageYOffset; // distância total do scroll vertical
window.pageXOffset; // distância total do scroll horizontal

if(window.innerWidth < 600) {
  console.log('Tela menor que 600px');
}
```

### MATCHMEDIA()
Utilize um media-querie como no CSS para verificar a largura do browser.

``` javascript
const small = window.matchMedia('(max-width: 600px)');

if(small.matches) {
  console.log('Tela menor que 600px')
} else {
  console.log('Tela maior que 600px')
}
```
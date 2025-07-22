# DOM (Document Object Model)

## Classes e Atributos

### CLASSLIST
Retorna uma lista com classes do elemento. Permite adicionar, remover e verificar se contém.

``` javascript
const menu = document.querySelector('.menu');

menu.className; // string
menu.classList; // lista de classes
menu.classList.add('ativo');
menu.classList.add('ativo', 'mobile'); // duas classes
menu.classList.remove('ativo');
menu.classList.toggle('ativo'); // adiciona/remove a classe
menu.classList.contains('ativo'); // true ou false
menu.classList.replace('ativo', 'inativo');
```

### ATRIBUTES
Retorna uma array-like com os atributos do elemento.

``` javascript
const animais = document.querySelector('.animais');

animais.attributes; // retorna todos os atributos
animais.attributes[0]; // retorna o primeiro atributo
```

#### GETATTRIBUTE E SETATTRIBUTE
Métodos que retornam ou definem de acordo com o atributo selecionado.

``` javascript
const img = document.querySelector('img');

img.getAttribute('src'); // valor do src
img.setAttribute('alt', 'Texto Alternativo'); // muda o alt
img.hasAttribute('id'); // true / false
img.removeAttribute('alt'); // remove o alt

img.hasAttributes(); // true / false se tem algum atributo
```
>*É muito comum métodos de get e set*

### READ ONLY VS WRITABLE
Existem propriedades que não permitem a mudançã de seus valores, essas são considerados Read Only, ou seja, apenas para leitura.

``` javascript
const animais = document.querySelector('.animais');

animais.className; // string com o nome das classes
animais.className = 'azul'; // substitui completamente a string
animais.className += ' vermelho'; // adiciona vermelho à string

animais.attributes = 'class="ativo"'; // não funciona, read-only
```
>*Podemos modificar o valor de uma propriedade usando `objeto.propriedade = ''`*
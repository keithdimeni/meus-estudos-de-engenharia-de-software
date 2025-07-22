# DOM (Document Object Model)

## Navegação po Tabs

### ADICIONAR CLASSES PARA MANIPULAÇÃO
A ideia de navegação por tabs, é ter uma lista de itens que controla a visualização de uma lista de conteúdo. Cada item da lista possui um conteúdo relacionado ao mesmo.

``` javascript
<!-- Primeiro, adicionar classes que irão
facilitar a manipulação dos elementos -->
<ul class="animais-lista js-tabmenu">
  ...
</ul>
<div class="animais-descricao js-tabcontent">
  ...
</div>
```

### SELECIONAR OS ITENS

``` javascript
const tabMenu = document.querySelectorAll('.js-tabmenu li');
const tabContent = document.querySelectorAll('.js-tabcontent section');
```

### FUNÇÃO CALLBACK
Recebe index como parâmetro para ativar a tab. Sempre que ativar, remove a classe ativo de todos os outros elementos.

``` javascript

function activeTab(index) {
  tabContent.forEach((content) => {
    content.classList.remove('ativo');
  });
  tabContent[index].classList.add('ativo');
}
```

### ADICIONAR O EVENTO
Neste caso precisamos passar antes a função anônima no callback, para podermos passar o index como argumento de `activeTab`

``` javascript
tabMenu.forEach((itemMenu, index) => {
  itemMenu.addEventListener('click', () => {
    activeTab(index);
  });
});
```

### ASSIM QUE CARREGAR
Adicionar a classe ativo ao primeiro elemento e adicionar a classe js ao html. ASsim identificamos se o Javascript está habilitado ou não.

``` javascript
<!-- No head do borwser -->
<script>document.documentElement.className += ' js';</script>
```

``` javascript
// Verificar se existe elemento em tabContent e tabMenu
if(tabContent.length && tabMenu.length) {
  tabContent[0].classList.add('ativo');
  ...
}
```

### ANIMAÇÃO COM CSS
Animação simples com css, sai de display none para display block.

``` css
.js .js-tabcontent section {
  display: none;
}

.js-tabcontent section.ativo {
  display: block !important;
  animation: show .5s forwards;
}

@keyframes show {
  from {
    opacity: 0;
    transform: translate3d(-30px, 0, 0);
  }
  to {
    opacity: 1;
    transform: translate3d(0px, 0, 0);
  }
}
```

>*O display none remove o texto até dos leitores de tela(acessibilidade)*
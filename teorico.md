# Teórico

1\) Qual a diferença do operador `==` para o operador `===` em JavaScript?

[Resposta]

A diferença é que no caso de se utilizar == haverá uma coerção do valor para que ambos os lados da expressão tenham o mesmo tipo.

No caso do === não haverá coerção 

1.1) Dê 2 exemplos de quando os operadores produziriam resultados diferentes

01 var var1 = 'true' == true;                 // false
02 var var2 = '0' == false;                   // true
03 var var3 = null == undefined;              // true
04 var var4 = false == null;                  // false
05 var var5 = null == 0;                      // false
06 var var6 = '' == 0;                        // true
07 var var7 = '\t\n' == 0;                    // true
08 var var8 = '1' == true;                    // true 


2\) Recursos/Práticas:

2.1) Qual recurso do javascript é mais recomendado para tratar processamentos asíncronos? Justifique.

assíncrono fazem uso de callbacks. Callbacks são porções de código que serão executados no futuro, em um tempo conveniente.

O JavaScript interage com os fluxos assíncronos através de troca de mensagens. Sempre que uma tarefa assíncrona entra em ação, a callback é registrada e fica a espera de uma mensagem para ser executada. Existe então um loop de eventos que aguarda por mensagens emitidas por timers, requisições, eventos do DOM e outras chamadas assíncronas.

As mensagens, quando recebidas, são mantidas em uma fila e disparam a execução da callback, uma por vez. É importante notar que duas callbacks não são disparadas no mesmo instante. Existe um único fluxo de execução JavaScript nos navegadores e as callbacks são executadas nele também.


2.2) Quais os recursos mais recomendados para incluir ícones em um site? Justifique.

No Find Icons, você pode baixar ícones organizados por temas e agrupados em pacotes. Para encontrá-los, a pesquisa pode ser feita por tema ou mesmo nome. Você ainda pode filtrá-los de acordo com o tamanho, podendo assim escolher o mais compatível para o seu site.

Mais de 1.700 ícones podem ser baixados no Dry Icons. Eles estão separados por categoria e agrupados em pacotes, o que torna a busca mais fácil, caso você esteja a procura de elementos de um determinado tema.

Basta acessar o site e fazer o download    é grátis. Além disso, é possível adquirir direitos de revenda ou obter acesso ao arquivo fonte de cada pacote. Para essas outras modalidades, você pode consultar diretamente os valores e a política aplicada à cada tipo de licença no site.

Formatos
.ICO
Este tipo de arquivo ainda é o mais utilizado devido ao grande suporte por parte dos navegadores e pela opção de conter diversas imagens encapsuladas. Ou seja, em um mesmo arquivo é possível atender diversas funções e resoluções de tela. (E não. Você não vai conseguir isto simplesmente renomeando um .gif ou .png. É necessário buscar um software próprio)/ Mas é necessário cuidado para que o arquivo final não fique muito pesado. eu recomendo o  tamanho máximo de 20K.

Antigamente você provavelmente faria isto da seguinte maneira:

<link rel="icon" type="image/png" href="img/favicon.png" />
Como somos bacanas e utilizamos HTML5 as coisas ficam mais simples:

<link rel="icon" href="img/favicon.png" />


2.3) Qual recurso dos browsers é usado para carregar dados/conteúdos dinâmicos sem recarregar a página? Existem alternativas?

É o seguinte, farei um esquema simples de como você deve fazer para carregar esses conteúdos sem precisar atualizar a página com PHP e AJAX.

index.php

<html>
<head>
<script type='text/javascript' src='http://code.jquery.com/jquery-1.5.1.min.js'></script>
<script type='text/javascript'>
$(document).ready(function(){
// Executa o evento CLICK em todos os links do menu
$('#menu a').live('click',function(){
 // Faz o carregamento da página de acordo com o COD da página, que vai pegar os valores da página page.php.
 $('#conteudo').load($(this).attr('href'));
 return false;

});

});
</script>
</head>
<body>
<div id='menu'>
<ul>
<li><a href='page.php?cod=1'>Home</a></li>
<li><a href='page.php?cod=2'>Serviços</a></li>
</ul>
</div>
<!-- Aqui serão mostrados os conteúdos -->
<div id='conteudo'>

</div>
</body>
</html>


Agora vou mostrar como pegar os valores utilizando PHP.

 

page.php

 

<?php
// Aqui ele pega o valor da varíavel do navegador.
$cod = $_GET['cod'];
// A condição switch faz com que o valor dos códigos do primeiro script represente uma página html que carregará na div conteudo.
switch($cod){
case '1'; // Aqui por exemplo, lá é page.php?cod=1, certo? Então ela vai carregar a página home.html na div conteúdo.
include('home.html');
break;
case '2'; // Aqui tambem, lá é page.php?cod=2, então ela carregará a página de noticias.html.
include('noticias.html');
}

?>


2.4) Qual recurso angular pode ser usado para aumentar a performance de campos que realizam algum processamento ao alterar o texto?


Uso o angular.copy() dentro da função edit que retorna apenas uma cópia do objeto, e um segundo argumento nesta que seria o index do array users que correspondente ao objeto modificado. Uso este index posteriormente para atualizar somente a parte que foi modificada:

angular.module('app', []).controller('Test', function($scope) {
    var index;
    $scope.users = [{
      name: 'Wallace',
      email: 'wallacemaxters@gmail.com'
    }, {
      name: 'Wayne',
      email: 'wayne.souza@gmail.com'
    }];
    $scope.edit = function(user, i) {
      $scope.update = angular.copy(user);
      index = i;
    }
    $scope.save = function() {
      $scope.users[index] = $scope.update; // captura o objeto modificado e atualiza no original
      $scope.update = ""; // reseta o update
    }
  });
<link href="https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/3.3.7/css/bootstrap.css" rel="stylesheet"/>
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.2.23/angular.min.js"></script>
<div ng-app="app" ng-controller="Test" class="container">
  <table class='table'>
    <tr ng-repeat="user in users">
      <td>Name: {{ user.name }}</td>
      <td>E-mail: {{ user.email }}</td>
      <td>
        <button class="btn btn-primary" ng-click="edit(user, $index)">editar</button>
      </td>
    </tr>
  </table>
  <form ng-if="update">
    <input type="text" ng-model="update.name" class="form-control" />
    <input type="email" ng-model="update.email" class="form-control" />
    <button type="submit" ng-click="save()" ng-submit="save()" class="btn btn-primary">Salvar</button>
  </form>
</div>


[Resposta]

2.5) Por quê é importante diminuir a quantidade de watchers do angular em uma página e como fazer?

[Resposta]

2.6) Por quê é importante evitar escopos isolados em diretivas do angular e como fazer?


O Angular JS (versão 1.x) utiliza uma verificação muito poluída para acompanhar todas as alterações na app, o framework tem que passar por cada watcher para verificar se eles precisam ser atualizados, esse processo é chamado como digest (ciclo de digestão) do Angular JS. Toda vez que um evento maior ocorre em sua app (ex: quando a página é carregada pela primeira vez, quando ocorre uma nova requisição AJAX ou quando a URL muda) o Angular recebe as alterações e prepara uma digestão (digest). Essa digestão nada mais é que um loop interno que é rodado dentro de um membro chamado $scope. Apesar disto levar milissegundos, o Angular executa somente um processo por vez. O grande mindset é compreender se todos watchers são realmente necessários em sua aplicação Angular JS e se valem mais do que a performance de toda sua app.


Watchers são configurados assim:

$scope.$watch
Nos tipos de bindings {{ }}
Na maioria das diretivas (ex: ng-hide,ng-show)
Nas variáveis de escopo $scope.artist: { xuxa : 'pele' }
Filtros {{ value | meuFiltro }}
Nos repeats ng-repeat
Watchers (ciclo de digest) são disparados:

Na ação do usuário (ex: ng-click). A maioria das diretivas incorporadas em sua página chamam o$scope.applyapós sua conclusão, o que dispara o ciclo de digestão do Angular JS.
ng-model
$http events (todas chamadas AJAX)
ng-change
$p promises resolvidas
$timeout
$interval
Chamadas manuais $scope.apply ou $scope.digest

[Resposta]

---

3\) CSS:

3.1) Por quê é importante não fazer seletores por tags html?

O id é quando você precisa de uma estilização específica daquele elemento. E a classe é para um grupo qualquer de elementos, muitas vezes seria todos que usam uma determinada tag, aí não tem porque usar.

Então eu vou no meio termo, não use até que precise usar. Não tem como estilizar apenas um elemento pela tag, a não ser que tenha certeza que nunca terá outro elemento com a mesma tag, aí é risco. É muito comum que o estilo se aplique a todos os elementos daquela tag, pleo menos dentro daquela área do documento. Exemplo:

<div id="produtos">
    <section>
        <h3>Brinquedos</h3>
No CSS só precisa:

#produtos h3 { ... }
E não há confusão com outros h3 do documento fora desta div.

O Bacco já comentou o que eu acho, quanto mais simples, melhor.

O único caso que talvez usaria id ou class onde pode ser resolvido com a tag é quando vai fazer algo para terceiros estilizarem como quiserem. Mesmo assim pensaria muito antes de fazer e tentaria evitar. Ainda dá para deixar as pessoas estilizarem pelas tags, mas nem sempre será tão prático.

[Resposta]

3.2) Para criar um site que desse a opção do usuário escolher um tema, qual tecnogia/recurso de css você utilizaria?

JavaScript, jQuerry, CSS, e Html 

[Resposta]

3.3) Quais práticas/recursos devem ser usados para criar sites responsivo?
1. Comece por uma tela pequena
Essa dica é ótima para quem ainda não tem um site para sua empresa, mas também vale para repensar o projeto que já existe. Ao invés de criar o layout do desktop para, só então, adaptá-lo ao mobile, faça o contrário. Isso porque é importante que o conteúdo seja idêntico em ambas as versões. Logo, pode ser mais difícil ter que suprimi-lo ao fazer o caminho inverso.

2. Aplique elementos flexíveis
Há layouts que não são exatamente perfeitos para o design responsivo. Por isso, tome cuidado ao escolher o mais adequado. Considere também a flexibilidade das imagens do seu site, afinal, fotos pesadas e estáticas — assim como ultrapassadas — podem não ser carregadas em qualquer dispositivo. Procure aplicar imagens leves e evite definir largura e altura fixas. Assim, elas podem se adaptar a todos os tipos de tamanho de tela.

3. Garanta a legibilidade
Lembra do teste que fizemos anteriormente? Imaginamos que você não tenha sentido dificuldade de leitura entre ambas as versões do blog, certo? Justamente porque uma das nossas práticas foi garantir a legibilidade. É por isso que você não sente a necessidade de usar o zoom, por exemplo. Uma dica é usar fontes especiais para leitura no tamanho 16px. Use também o aplicativo FitText para ajustar os textos.

4. Crie botões que convertam
O zoom de que falamos acima vale também para todo e qualquer botão que o usuário desejar usar no seu site. Ainda que o intuito da ferramenta pitch-to-zoom seja facilitar o acesso aos botões, você não vai querer dificultar a compra de um produto, certo? Para facilitar as conversões, crie botões com dimensões de 44x44px, o tamanho mínimo recomendável para otimizar os toques na tela.

5. Favoreça a velocidade do site
Outra característica básica do design responsivo é diminuir ao máximo o tempo de carregamento e resposta a comandos. Além de serem ignorados pelos crawlers do Google, que começam a penalizar o site já a partir de 2 segundos de espera, o próprio usuário tende a abandoná-lo se as páginas não responderem imediatamente. Portanto, procure usar ferramentas para reduzir o carregamento das suas páginas internas.

6. Elimine o que não é essencial
A partir de agora, o seu mantra deve ser limpar, enxugar e eliminar todo e qualquer elemento desnecessário à compreensão das mensagens. É uma maneira de melhorar ainda mais a flexibilidade do site e torná-lo mais amigável a dispositivos móveis. O design responsivo faz o possível para que nada interfira na interação do usuário com a plataforma. Portanto: limpe, enxugue e elimine o que for possível.

7. Faça testes de usabilidade
Para saber se o design responsivo adotado tem sido efetivo, experimente acessar seu site por diversos modelos de smartphone — dos mais velhos aos mais recentes. Peça para seus amigos acessarem de outros dispositivos e pergunte como foi a experiência. Você também pode usar algumas ferramentas de testes eficientes, como o Screenfly, o PageSpeed Insights e o Responsinator. Esta última é gratuita e permite que você simule ações.

[Resposta]

3.4) Quais metodologias CSS você costuma seguir? Explique um pouco delas.

O conteúdo de um website geralmente é bem específico em cada uma das páginas. É pouco comum que o mesmo conteúdo se manifeste em diferentes seções de um projeto. Portanto, classes nomeadas com base no conteúdo são bastante difíceis de serem reusadas.

Segundo o OOCSS, um objeto de CSS é todo padrão visual que pode se repetir no projeto e é identificado através de uma classe. O estilo enfatiza a separação de propriedades de estrutura e de skin. Propriedades como background, color e border, quando fizerem parte da identidade visual do projeto, são consideras parte do skin e devem ser agrupadas em classes próprias. Observe a classe de skin anchor-icon, que define um background, utilizada juntamente com duas classes de estrutura: <button class="button anchor-icon">Abrir</button> e <a class="link anchor-icon">Tableless</a>.

O uso dos objetos ao longo do projeto não deve causar surpresas, o que significa que sua localização não deve interferir na sua apresentação. Isto significa não utilizar nesting de seletores. Caso sejam necessárias variações, objetos podem estender outros diretamente no HTML: <div class="graph graph-big">.

Classes como .wrapper, .image-replacement e .clearfix aparecem em alguns exemplos que aplicam este sistema. O argumento é que se tratam de classes de estrutura com um padrão que pode ser reusado. Um exemplo: <div class="graph graph-big clearfix wrapper">.

O maior ensinamento é o de utilizar classes baseadas na aparência ao invés de conteúdo ou até mesmo funcionalidade, que até pouco eu acreditava ser o ideal. Apesar dos demais conceitos serem interessantes, a documentação é vaga e não há um padrão de nomenclatura que diferencie classes de estruturação e de skins.

[Resposta]

[Explicacão]

---

4\) Análise de código

4.1) Quanto tempo vai demorar para o código a seguir imprimir "finished"? Justifique. (Levando em consideração que `somePromise()` vai retornar uma Promise resolvida)
```js
function doSomething() {
    return new Promise(resolve => {
        setTimeout(resolve, 1000)
    })
}

function doSomethingElse() {
    return new Promise(resolve => {
        setTimeout(resolve, 2000)
    })
}

somePromise()
    .then(() => {
        doSomething()
        doSomethingElse()
    })
    .then(() => {
        console.log('finished')
    })

```

[Resposta]

[Justificativa]

4.2) O que o código a seguir imprime? (Levando em consideração que `somePromise()` vai retornar uma Promise resolvida)
```js
somePromise()
    .then(() => {
        throw new Error('uh oh!')
    }, err => {
        console.log(err.message)
    })
    .then(() => {
        console.log('ok now!')
    })
```


se tiver um novo erro ele irá mostrar ('uh oh!')

se não tiver erro  ele irá aparesentar ('ok now!')

[Resposta]

[Justificativa]

4.3\) Quais as vantagens/desvantagens da segunda função em relação a primeira?
```js
function doSomething(options) {
    return fetch(options.url).then(r => r.json())
    
    Uma função normalmente contém um conjunto de comandos para uma finalidade específica que você deseja executar em um determinado momento. Cada função em um script recebe um nome exclusivo. O exemplo abaixo é chamado "doSomething", embora possa ser dado qualquer nome que você gosta.
    
    
}

async function doSomethingAsync(options) {
    return fetch(options.url).then(r => r.json())
    
    
     Essa é a conexão entre async / await e promises. Quando você coloca async na frente de uma função, você está dizendo que ela retornará uma promessa com o valor da declaração de retorno resolvido!

}
```

ainda não tenho conheciment, estou estudando no momento 

[Resposta]

---

5\) Quais as vantagens de usar ES modules em vez de usar commonjs?

Os módulos CommonJS possuem um formato dinâmico, tanto o que é importando quanto o que é exportado pode ser alterado em tempo de execução (runtime). Uma das principais motivações para o ES6 adicionar o próprio formato de módulos foi possibilitar um formato estático que traz vários benefícios conforme vamos ver em detalhes a seguir.

No modelo CJS de módulos era possível fazer o seguinte:

var module;
  if (condition) {
    module = require('lib.js');
  } else {
    module = require('other_lib.js');
  }

[Resposta]

---

6\) Cite as principais diferenças entre um componente e uma diretiva no AngularJS.

[Resposta]

O Component é uma Directive especial, ele foi criado para suprir e corrigir problemas que a directive possui quando voce quer criar um componente html que possui um controller e um html proprio, esses problemas seriam: nao possui bindings, nao possui scope isolado e ambiguidades geradas pelas especificações das directives do tipo link e atributo.

Voce deve usar um Component: Sempre que quiser criar um componente html de scopo isolado (substitui a criação de um html com binding via ng-controller de um controller).

Voce deve usar uma Directive: Apenas quando voce quiser criar um atributo que executa algum javascript de manipulação de DOM ou manipulação simples de informação.

# Botoes-praticas-FrontEnd
Conteúdo do curso Desenvolvimento Web - Praticas FrontEnd 


Por que esta abordagem com um elemento não funciona?
O trecho de código abaixo leva ao site do freeCodeCamp quando ele é clicado.

  <a href="https://www.freecodecamp.org/">
    <button>freeCodeCamp</button>
  </a> 
No entanto, essa não é uma marcação válida em HTML.

O elemento a pode ser envolvido por parágrafos inteiros, listas, tabelas e assim por diante. É possível usar até mesmo seções inteiras, desde que não haja conteúdo interativo dentro delas (por exemplo, botões ou outros links). - Fonte: Grupo de Trabalho de Tecnologia de Aplicação de Hipertexto Web
Essa é considerada uma má prática, pois torna difícil entender a intenção do usuário.

Os links devem navegar o usuário para outra parte da página da web ou para um site da web externo. Os botões devem realizar uma ação específica como o envio de um formulário.

Quando você aninha um dentro do outro, isso torna confusa a ação que você quer realizar. É por isso que é melhor não aninhar um botão dentro de um elemento de âncora.

Como estilizar um link que se pareça com um botão com CSS
Esta primeira abordagem não utiliza, de fato, um botão. Podemos estilizar uma tag de âncora para que se pareça com um botão usando o CSS.

Este é o estilo padrão do HTML para um elemento de âncora.

blue-anchor-tag
Podemos adicionar uma classe ao elemento de âncora e depois usar esse seletor de classe para estilizar o elemento.

  <a class="fcc-btn" href="https://www.freecodecamp.org/">freeCodeCamp</a>  
Se você quiser que o link abra em uma nova página, pode adicionar o atributo target="_blank", assim:

  <a target="_blank" class="fcc-btn" href="https://www.freecodecamp.org/">freeCodeCamp</a>  
Então, podemos adicionar uma cor de fundo e mudar a cor da fonte, desse modo:

.fcc-btn {
  background-color: #199319;
  color: white;
}
background-and-white-text
O próximo passo é adicionar algum preenchimento (em inglês, padding) ao redor do texto:

.fcc-btn {
  background-color: #199319;
  color: white;
  padding: 15px 25px;
}
adding-padding-1
Finalmente, podemos usar a propriedade text-decoration para remover o sublinhado do texto:

.fcc-btn {
  background-color: #199319;
  color: white;
  padding: 15px 25px;
  text-decoration: none;
}
removing-underline
Agora temos um elemento de âncora que se parece com um botão.

Também podemos tornar este "botão" um pouco mais interativo mudando a cor de fundo, dependendo do estado do link.

.fcc-btn:hover {
  background-color: #223094;
}

Poderíamos deixar o design mais intrincado, mas a ideia é apenas mostrar o básico de como estilizar um link para que se pareça um botão.

Você também poderia optar por usar uma biblioteca do CSS, como o Bootstrap.

  <a class="btn btn-primary" href="https://www.freecodecamp.org/">freeCodeCamp</a>  
bootstrap-styles
Se o seu projeto já inclui o Bootstrap, você pode usar os estilos de botões incorporados. Eu, no entanto, não importaria o Bootstrap apenas para estilizar um link.

Quais são os problemas com esta abordagem?
Há algumas discussões sobre o fato de ser uma boa prática criar links estilizados como botões. Alguns argumentarão que os links devem sempre se parecer com links e que os botões devem sempre se parecer com botões.

No livro da web chamado Resilient Web Design, Jeremy Keith afirma que

Um material não deve ser usado como substituto para outro. Caso contrário, o resultado final será enganoso.
Por que eu me dei ao trabalho de trazer à tona esse debate?

O meu objetivo não é fazer com que você escolha um lado do debate em vez do outro. Só quero que vocês estejam cientes dessa discussão em andamento.

Como usar os atributos action e formaction para fazer um botão de formulário
Como usar o atributo action
Outra alternativa seria aninhar o botão dentro de um formulário e usar o atributo action.

Exemplo de entrada:

  <form action="https://www.freecodecamp.org/">
    <input type="submit" value="freeCodeCamp">
  </form>
Exemplo de botão:

  <form action="https://www.freecodecamp.org/">
    <button type="submit">freeCodeCamp</button>
  </form>
Este seria o estilo padrão do botão.

default-button-style
Poderíamos usar os mesmos estilos anteriores, mas teríamos que adicionar o ponteiro do cursor e definir o atributo border como none, assim:

.fcc-btn {
  background-color: #199319;
  color: white;
  padding: 15px 25px;
  text-decoration: none;
  cursor: pointer;
  border: none;
}
removing-underline-1
Como utilizar o atributo formaction
Similar à abordagem anterior, podemos criar um formulário e utilizar o atributo formaction.

Exemplo de entrada:

  <form>
    <input type="submit" formaction="https://www.freecodecamp.org/" value="freeCodeCamp">
  </form>
Exemplo de botão:

  <form>
    <button type="submit" formaction="https://www.freecodecamp.org/">freeCodeCamp</button>
  </form>
Você só pode usar o atributo formaction com inputs e buttons que tenham os atributos type="image" ou type="submit".

Isso está semanticamente correto?
Embora essa pareça ser uma solução funcional, há uma questão a respeito de isso ser ou não semanticamente correto.

Estamos usando as tags de formulário, mas isso não funciona como um formulário real. O objetivo de um formulário é coletar e enviar dados do usuário.

Estamos, no entanto, usando o botão de envio para levar o usuário para outra página ou seção.

Quando se trata de semântica, essa não é uma boa prática de uso das tags de formulário.

Efeitos colaterais do uso dos atributos action e formaction
Quando você clica no botão, algo interessante acontece com o URL. O URL agora tem um ponto de interrogação ao final.

question-mark-at-end
O motivo dessa mudança é porque o formulário está usando o método GET. Você poderia mudar para o método POST, mas pode haver casos onde isso também não seja o ideal.

  <form method="POST" action="https://www.freecodecamp.org/">
    <button type="submit">freeCodeCamp</button>
  </form>
Embora essa abordagem produza uma marcação válida em HTML, ela vem com esse efeito colateral não intencional.

Como usar o evento onclick do JavaScript para fazer um botão
Nas abordagens anteriores, analisamos as soluções em HTML e em CSS. Também podemos usar o JavaScript para alcançar o mesmo resultado.

Exemplo de input:

 <form>
    <input type="button" onclick="window.location.href='https://www.freecodecamp.org/';" value="freeCodeCamp" />
 </form>
Exemplo de button:

<button onclick="window.location.href='https://www.freecodecamp.org/';">freeCodeCamp</button>  
location.href representa a localização de um URL específico. Nesse caso, o window.location.href retornará https://www.freecodecamp.org/.

Desvantagens dessa abordagem
Embora essa solução funcione, há alguns problemas potenciais a serem considerados.

Se o usuário tiver decidido desativar o JavaScript em seu navegador, claramente, essa solução não funcionará. Infelizmente, isso poderá levar a uma má experiência para o usuário.

Conclusão
O objetivo deste artigo é mostrar três maneiras diferentes de se fazer botões agirem como links.

A primeira abordagem foi estilizar um link para que se parecesse com um botão. Também analisamos no debate se é uma boa ideia mudar a aparência dos links para se parecerem com outro elemento.

A segunda abordagem utilizou formulários e os atributos action e formaction. Também aprendemos, contudo, que essa abordagem tem alguns efeitos colaterais com o URL e não é semanticamente correta.

A terceira abordagem utilizou o evento onclick do JavaScript e window.location.href. Também aprendemos, porém, que essa abordagem pode não funcionar se o usuário decidir desativar o JavaScript em seu navegador.

Como desenvolvedor, é realmente importante observar os prós e os contras de uma abordagem específica antes de incorporá-la em seu projeto.

Espero que tenham gostado deste artigo e aprendido algumas coisas na leitura.

Botões

bookmark_border
Um botão consiste em um texto ou um ícone (ou ambos) que comunica a ação que ocorre quando o usuário toca nele.


Você pode criar o botão no seu layout de três maneiras, dependendo se ele será um botão com texto, um ícone ou ambos:

Com texto, usando a classe Button:

<Button
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="@string/button_text"
    ... />
Com um ícone, usando a classe ImageButton:

<ImageButton
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:src="@drawable/button_icon"
    android:contentDescription="@string/button_icon_desc"
    ... />
Com texto e um ícone, usando a classe Button com o atributo android:drawableLeft:

<Button
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="@string/button_text"
    android:drawableLeft="@drawable/button_icon"
    ... />
As principais classes são as seguintes:

Button
ImageButton
Responder a eventos de clique
Quando o usuário clica em um botão, o objeto Button recebe um evento de clique.

Para definir o manipulador de eventos de clique de um botão, adicione o atributo android:onClick ao elemento <Button> no layout XML. O valor desse atributo precisa ser o nome do método que você quer chamar em resposta a um evento de clique. Em seguida, a Activity que hospeda o layout precisa implementar o método correspondente.

Por exemplo, veja um layout com um botão que usa android:onClick:


<?xml version="1.0" encoding="utf-8"?>
<Button xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/button_send"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="@string/button_send"
    android:onClick="sendMessage" />
Dentro da Activity que hospeda esse layout, o método a seguir processa o evento de clique:

Kotlin
Java

/** Called when the user touches the button */
fun sendMessage(view: View) {
    // Do something in response to button click
}
O método declarado no atributo android:onClick precisa ter uma assinatura exatamente conforme mostrado acima. Especificamente, o método precisa:

ser público;
retornar nulo;
definir um View como único parâmetro, que será o View que foi clicado.
Usar um OnClickListener
Também é possível declarar o manipulador de eventos de clique de forma programática, em vez de em um layout XML. Isso pode ser necessário se você instanciar o Button no momento da execução ou se precisar declarar o comportamento de clique em uma subclasse Fragment.

Para declarar o manipulador de eventos de forma programática, crie um objeto View.OnClickListener e atribua-o ao botão chamando setOnClickListener(View.OnClickListener). Exemplo:

Kotlin
Java

val button: Button = findViewById(R.id.button_send)
button.setOnClickListener {
    // Do something in response to button click
}
Estilizar seu botão
A aparência do botão (imagem de plano de fundo e fonte) pode variar de acordo com o dispositivo, porque dispositivos de fabricantes diferentes costumam ter estilos padrão diferentes para controles de entrada.

É possível controlar completamente o estilo dos controles usando um tema aplicado a todo o aplicativo. Por exemplo, para garantir que todos os dispositivos com o Android 4.0 ou versão mais recente usem o tema Holo no seu app, declare android:theme="@android:style/Theme.Holo" no elemento <application> do manifesto. Leia também a postagem do blog Holo Everywhere (link em inglês) para ver informações sobre como usar o tema Holo e ainda oferecer compatibilidade com dispositivos mais antigos.

Para personalizar botões individuais com um plano de fundo diferente, especifique o atributo android:background com um recurso drawable ou de cores. Como alternativa, você pode aplicar um estilo ao botão, que funciona de maneira semelhante aos estilos HTML, para definir várias propriedades de estilo, como plano de fundo, fonte, tamanho, entre outras. Para ver mais informações sobre como aplicar estilos, consulte Estilos e temas.

Botão sem bordas
Um design que pode ser útil é o de um botão "sem bordas". Os botões sem bordas são parecidos com botões básicos. A diferença é que eles não apresentam bordas nem plano de fundo, mas ainda mudam de aparência em estados diferentes, como quando clicados.

Para criar um botão sem bordas, aplique o estilo borderlessButtonStyle ao botão. Exemplo:


<Button
    android:id="@+id/button_send"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="@string/button_send"
    android:onClick="sendMessage"
    style="?android:attr/borderlessButtonStyle" />
Plano de fundo personalizado
Caso queira realmente redefinir a aparência do seu botão, você pode especificar um plano de fundo personalizado. No entanto, em vez de fornecer um simples bitmap ou cor, seu plano de fundo precisa ser um recurso de lista de estado, que muda de aparência dependendo do estado atual do botão.

Você pode definir a lista de estados em um arquivo XML que defina três imagens ou cores diferentes para os diferentes estados do botão.

Para criar um drawable de lista de estados para o plano de fundo do botão:

Crie três bitmaps para o plano de fundo do botão, que representem os estados padrão, pressionado e em foco.
Para garantir que suas imagens caibam em botões de vários tamanhos, crie os bitmaps como bitmaps nine-patch.

Coloque os bitmaps no diretório res/drawable/ do projeto. Cada bitmap precisa ser nomeado corretamente para refletir o estado do botão que cada um representa, como button_default.9.png, button_pressed.9.png e button_focused.9.png.
Crie um novo arquivo XML no diretório res/drawable/, dando um nome como button_custom.xml. Insira o seguinte XML:

<?xml version="1.0" encoding="utf-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:drawable="@drawable/button_pressed"
          android:state_pressed="true" />
    <item android:drawable="@drawable/button_focused"
          android:state_focused="true" />
    <item android:drawable="@drawable/button_default" />
</selector>
Isso define um único recurso desenhável, que mudará a imagem de acordo com o estado atual do botão.

O primeiro <item> define o bitmap a ser usado quando o botão for pressionado (ativado).
O segundo <item> define o bitmap a ser usado quando o botão estiver em foco, ou seja, quando ele for destacado usando o trackball ou o botão direcional.
O terceiro <item> define o bitmap a ser usado quando o botão estiver no estado padrão, não pressionado nem em foco.
Observação: a ordem dos elementos <item> é importante. Quando esse drawable é referenciado, os elementos <item> são transferidos em ordem para determinar qual é apropriado para o estado atual do botão. Como o bitmap padrão é o último, ele só é aplicado quando as condições android:state_pressed e android:state_focused são avaliadas como falsas.

Esse arquivo XML agora representa um único recurso drawable e, quando referenciado por um Button para definir o plano de fundo, a imagem exibida mudará de acordo com esses três estados.

Em seguida, basta aplicar o XML file do drawable como plano de fundo do botão:

<Button
    android:id="@+id/button_send"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="@string/button_send"
    android:onClick="sendMessage"
    android:background="@drawable/button_custom"  />
Para ver mais informações sobre essa sintaxe XML, incluindo como definir um estado de botão desativado, com o cursor do mouse sobre ele ou outros, leia sobre Drawable de lista de estados.









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

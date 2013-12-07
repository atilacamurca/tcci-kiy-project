# Introdução

A internet se torna cada vez mais popular e junto com ela as tecnologias envolvidas, ou seja,
a linguagem de marcação HTML junto com CSS, o JavaScript, protocolo HTTP. Essas tecnologias
estão saindo do browser e chegando ao desktop de todos graças a um ambiente chamado
[Node.js \cite{nodejs}](http://nodejs.org).

Através da engine V8 do Google Chrome responsável pela execução do JavaScript junto com uma API
em C para suprir o que falta para o JavaScript ser uma linguagem útil fora do browser tal como
acesso ao sistema de arquivos, um servidor HTTP, WebSockets, execução de programas externos,
etc. já é possível criar as chamadas web apps, exceto que agora sem servidores externos para
execução das tarefas.

## Node.js

O esforço do Node.js em permitir execução de códigos JavaScript fora do browser permite criar
um servidor HTTP, que pode ser usado em ambientes de produção, simples como o trecho abaixo:

~~~javascript
var http = require('http');

http.createServer(function (request, response) {
  response.writeHead(200, {'Content-Type': 'text/plain'});
  response.end('Hello World\n');
}).listen(8181);

console.log('Server running at http://127.0.0.1:8181/');
~~~

Junto com o Node.js temos um paradigma de programação muito comum em interfaces gráficas chamada
programação orientada a eventos com entrada e saída não-bloqueantes. Isso quer dizer que os
métodos tendem a retornar logo após sua chamada e notificam quando a execução foi finalizada,
da mesma forma que criar um evento de *click* usando [jQuery \cite{jquery}](http://jquery.com).

# Motivação e objetivos

Tendo toda essa tecnologia em mente surgiu o projeto **kiy**. A ideia é juntar o poder e as
facilidades da tecnologia HTML e CSS para criar aplicativos modernos e com rapidez, e todo
o poder do JavaScript com as extensões do Node.js para criar uma framework que cria
aplicativos desktop com interface web.

Imagine usar a framework
[Twitter Bootstrap \cite{bootstrap}](http://twitter.github.io/bootstrap) para criar
uma interface moderna com o poder de acessar o sistema de arquivos do seu computador para
criar, por exemplo, um gravador de CD/DVD. Ou ainda um Navegador de Arquivos, um Editor de
Texto, um Cliente de Bate-papo, uma Agenda, um Reprodutor de Áudio/Vídeos, enfim.

Seria possível criar todo um ecosistema como o [Gnome](http://gnome.org) com interfaces web
e que podem facilmente ter sincronizações com serviços on-line.

## Concepção

Para esse projeto precisamos de:

* Node.js, usado como servidor;
* um mini browser, usando webkit com python por exemplo;
* uma framework MV*, [Backbone \cite{backbone}](http://backbonejs.org/);
* jQuery ou similar para fácil iteração de eventos, requisições ajax, etc;
* Twitter Bootstrap ou similar para layout;

## Arquitetura

A arquitetura do projeto kiy é bem simples como pode ser vista na Figura \ref{img:arch}.

\begin{figure}
	\includegraphics[scale=0.55]{img/architecture.png}
	\caption{Arquitetura do kiy \label{img:arch}}
\end{figure}

## Estrutura de diretórios

Este projeto segue a linha de Single Page App ou SPA (Aplicativos em Única Página),
em que temos apenas uma página HTML contento todo o projeto. Isso parece ser um jeito
grosseiro e difícil de manter, mas algumas técnicas são utilizadas para que as SPA's
sejam uma boa opção ao criar aplicativos usando tecnologias web.

Uma grande vantagem das SPAs é que elas tendem a ser rápidas, levando em conta que depois
de carregar a primeira vez, a maioria do conteúdo não precisa ser recarregado. Mas como fazer
para que o código seja distribuído? Simplesmente usando *templates*, com jQuery,
[Swig \cite{swig}](http://paularmstrong.github.io/swig/) ou
[Jade \cite{jade}](http://jade-lang.com/).
Dessa forma o conteúdo HTML pode ser colocado em arquivos menores fazendo com que o código
fique limpo e organizado.

Em aplicativos que usam a tecnologia Node.js é comum o uso do arquivo `package.json`, onde
nele é descrito seu aplicativo, os módulos que ele depende, versões utilizadas, etc. Vejamos
um exemplo desse arquivo:

~~~
{
  "name": "hello-world",
  "scripts": {
    "start": "node app.js"
  },
  "version": "0.0.0",
  "engines": {
    "node": "v0.10.x"
  },
  "keywords": [
    "hello",
    "world",
    "appp"
  ],
  "dependencies" : {
    "express"   :  "*",
    "swig"		:  "*",
    "jquery"	:  "*"
  }
}
~~~

Com essa linha de raciocínio é possível usar ferramentas para gerenciar dependências, como
[bower \cite{bower}](http://bower.io/), [npm \cite{npm}](https://npmjs.org/),
[yeoman \cite{yeoman}](http://yeoman.io/).

\begin{figure}
	\includegraphics[scale=0.55]{img/directory-structure.png}
	\caption{Estrutura de diretórios \label{img:struct}}
\end{figure}

## Linha de comando

Para criar um novo projeto execute o comando:

~~~
kiy create appname
~~~

Depois entre no diretório do aplicativo que possui o mesmo nome definido no comando acima, ou seja,
`appname`.

~~~
cd appname
~~~

Você verá a estrutura conforme a figura \ref{img:struct}.

Para executar o aplicativo faça:

~~~
kiy run
~~~

Para gerar o aplicativo para distribuição faça:

~~~
kiy gen deb
~~~

Este comando irá gerar um arquivo com extensão `.deb` que pode ser instalado no Debian/Ubuntu.
Ou ainda podemos executar:

~~~
kiy gen [rpm|dmg|msi|exe]
~~~

e criar aplicativos que podem ser instalados no RedHat/Fedora/SuSE, MacOS, Windows,
respectivamente.

## Projetos existentes

Existem outros projetos interessantes em que essa ideia é aplicada mas apenas dois
deles utilizam Node.js:

* node-webkit - <https://github.com/rogerwang/node-webkit> muito similar ao projeto kiy,
	utiliza WebKit e Node.js escrita em C++;
* TideSDK - <http://www.tidesdk.org/> utiliza API própria escrita em C++ e faz *bindings* com
	outras linguagens;
* iBreed - <https://github.com/in-sideFX/iBreed> utiliza JavaFX;
* bowline - <https://github.com/maccman/bowline> utiliza Ruby;
* NodeOS - <http://nodeos.github.io/>;

# Cronograma

O cronograma do projeto pode ser visto na Tabela \ref{tab:crono}.

Atividade/Mês                01    02    03    04    05    06    07    08    09
--------------------------  ----  ----  ----  ----  ----  ----  ----  ----  ----
Estudo Bibliográfico         X
Modelagem da abordagem       X     X
Dissertação Preliminar             X
Implementação                            X     X     X     X
Testes e Correção                              X           X
Avaliação da Implementação                                       X
Conclusão da Dissertação                                         X
Revisão da Dissertação                                                  X
Entrega da Dissertação                                                       X

Table: Cronograma\label{tab:crono}

# Futuro da informática

Eu imagino num futuro bem próximo que internet vai estar em todos os lugares e que ao ligar um
computador ou smartphone apenas um browser irá abrir com todos os aplicativos desenvolvidos com
tecnologias web.

## O que outras pessoas acham?

* <http://worldofgnome.org/what-if-we-replace-gtkqt-with-webkit/>

Alex Diavatis em 31 de Julho de 2013 escreveu em seu blog World of Gnome:
What if we replace GTK/Qt with WebKit? (E se nós trocassemos GTK/Qt por WebKit?)

## O que outras pessoas já estão fazendo!

* <http://technical.io/>

Tessel é um microcontrolador conectado à Internet para desenvolvedores de software.

Deselvolvimento embutido é fácil como codificar para a web ou aplicativos móveis.
Ou protoripar um produto físico, e refinar a experiência com telemetria e atualização
por wi-fi.

### Instalação

~~~
$ npm install hardware -g
$ tessel shell
~~~

### Exemplo piscar led

~~~javascript
var tessel = require('tessel');
tessel.led(1).blink();
tessel.led(2).blink();
~~~

## Firefox OS

* <https://developer.mozilla.org/en-US/Firefox_OS/Platform/Gaia>

Gaia é a interface visual do Firefox OS. Tudo que aparece na tela após a inicialização
é renderizado através do Gaia, incluindo a tela de bloqueio, tela inicial, discador,
e outros aplicativos. Gaia é escrito totalmente em HTML, CSS e JavaScript. Sua interface
entre com o sistema operacional e o _hardware_ é através de padrões WEB APIs, que são
implementados pelo [Gecko](https://developer.mozilla.org/en-US/docs/Mozilla/Gecko).
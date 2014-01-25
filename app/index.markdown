---
layout: default
title: Home
---

<header class="main-header">
  <h1 class="logo">Grunt</h1>
</header>

<section class="main-content">

<article>

##Objetivo

Explicar o que é e como usar o Grunt.

</article>

<article>

##O que é?

Grunt é um automatizador de tarefas que usa Node.js, criado por <a href="https://github.com/cowboy/" target="_blank">Ben Alman</a>, com o objetivo de... automatizar tarefas (oh rly?), fazer builds de scripts, testes automatizados, etc, etc, etc...

</article>

<article>

##Instalação

Partindo do pressuposto que você já tenha o Node.js instalado em sua máquina, você pode continuar a leitura, caso não tenha instalado ainda o Node.js por qualquer motivo, lembre-se que estamos em 2014, instala logo o Node.js e você verá a quantidade de possibilidades que você está perdendo, seja por medo de usar o Terminal/Bash/PowerShell/CMD/CLI/Linha de Comando ou pelo fato de você ter passado os últimos anos numa caverna no Tuvalu.

Ok, para instalar, abra o seu Terminal (eu uso e recomendo o <a href="http://www.iterm2.com/" target="_blank">iTerm 2</a>, se você usa Windows, ~~lamento~~ recomendo usar o Git Bash, e se você usa Linux, parabéns!) e digite:

`npm install -g grunt-cli`

Talvez você tenha que executar o comando como Administrador, talvez não, enfim, feito isso, é só aguardar a instalação acabar e você terá o comando `grunt` disponível em sua linha de comando!

</article>

<article>

##Usando o Grunt

Prosseguindo, agora vamos começar a brincar com o Grunt, para isso precisamos criar 2 arquivos no root do nosso projeto, portanto, crie o arquivo `package.json` e o `Gruntfile.js` (ou `Gruntfile.cofee` se você usa <a href="http://coffeescript.org/" target="_blank">CoffeeScript</a>)

>E se você utiliza versionamento, certifique-se de colocar o diretório `node_modules` no `.gitignore`!

Anyway, o `package.json` é um arquivo que vai listar todas as dependências do projeto, já que para usar o Grunt, precisamos instalar vários plugins, você pode encontrar uma lista de plugins <a href="http://gruntjs.com/plugins" target="_blank">aqui</a> e daqui a pouco você verá como instalar plugins.

>“Todo projeto Node.js é chamado de módulo, mas o que é um módulo? O termo módulo surgiu do conceito de que a arquitetura do Node.js é modular. E todo módulo é acompanhado de um arquivo descritor, conhecido pelo nome de package.json.” - <a href="http://www.casadocodigo.com.br/products/livro-nodejs" target="_blank">Caio Ribeiro Pereira. “Aplicações web real-time com Node.js.”</a>

Aqui está um exemplo de um `package.json`:

{% highlight json %}
{
  "name": "nome-do-projeto",
  "version": "0.0.0",
  "description": "Lorem ipsum...",
  "author": {
    "name": "Lucas",
    "url": "http://agtlucas.com"
  }
}
{% endhighlight %}

É autoexplicativo...

Repare que ainda não temos nenhuma depedência em nosso `package.json`, então vamos adicionar a primeira, que é o Grunt, sim, antes instalamos o `grunt-cli`, agora precisamos do módulo do Grunt. Para isso temos 2 alternativas, de fato para qualquer plugin, a primeira é definir todas as dependências conforme o exemplo abaixo e em seguida rodar o comando `npm install`:

{% highlight json %}

{
  "name": "nome-do-projeto",
  "version": "0.0.0",
  "description": "Lorem ipsum...",
  "author": {
    "name": "Lucas",
    "url": "http://agtlucas.com"
  },
  "devDependencies": {
    "grunt": "~0.4.2",
    "foo": "~0.0.1",
    "bar": "~0.0.1"
  }
}

{% endhighlight %}

A segunda alternativa é executar direto o comando `npm install <dependência> --save-dev` (se você quiser, pode passar mais de uma dependência: `npm install <dependência> <dependência-1> <dependência-2> --save-dev`, no nosso caso, `npm install grunt --save-dev`, que economiza o teclado... e o resultado vai ser o mesmo.

Você escolhe, eu geralmente uso as duas formas, depende da situação.

Blz, agora vamos dar uma olhada no `Gruntfile.js`, que é este arquivo onde vamos configurar nossas tasks e carregar nossos plugins. Ele basicamente é composto por uma função globar com metódos para configurar, inicializar e registrar tarefas, vejamos um exemplo:

{% highlight js %}

{% endhighlight %}

</article>

<article>

##Otimizando o Gruntfile

</article>

<article>

##Plugins

</article>

<article>

##Yeoman

</article>

</section>
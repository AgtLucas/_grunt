---
layout: default
title: Home
---

<header class="main-header">
  <h1 class="logo">Grunt</h1>
  <small>Artigo criado e mantido por: <a href="https://github.com/AgtLucas" target="_blank">Lucas</a></small>
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

// ECMAScript 5' strict mode
'use strict';

// Função modular
module.exports = function(grunt) {

  // Iniciamos a configuração
  grunt.initConfig({

    // Busca o package.json
    pkg: grunt.file.readJSON('package.json');

    // Definimos uma task
    foo: {
      options: {
        bar: true
      }
    },

    // Podemos definir outras
    bar: {
      build: {
        nsa: true
      }
    }

  });

  // Carregamos as tasks
  grunt.loadNpmTasks('foo');
  grunt.loadNpmTasks('bar');

  // Registramos as tasks
  grunt.registerTask('default', ['foo']);

};
{% endhighlight %}

Repare que registramos apenas uma task, a `default`, que ao executarmos o comando `grunt` no terminal, será executada as tasks definidas, no caso `foo` e `bar`. Podemos também acessar tasks diretamente, ou seja, se executarmos o comando `grunt foo`, chamaremos a task `foo`.

Talvez este exemplo não tenha ficado claro, então vamos fazer algo útil, vamos instalar os plugins `grunt-contrib-watch` (para "assistir" os arquivos modificados e automaticamente fazer o reload no browser, poupando o trabalho do `F5` ou do `CMD + R`), `grunt-contrib-compass` (requer que você tenha Ruby instalado) e o `grunt-contrib-uglify` (para minificar os arquivos `.js`). No terminal, digite: `npm install grunt-contrib-compass grunt-contrib-uglify --save-dev`. Feito isso, vamos editar nosso `Gruntfile.js`.

{% highlight js %}

// ECMAScript 5' strict mode
'use strict';

// Função modular
module.exports = function(grunt) {

  // Iniciamos a configuração
  grunt.initConfig({

    // Busca o package.json
    pkg: grunt.file.readJSON('package.json');

    // Task: Compass
    compass: {
      dist: {
        options: {
          sassDir: 'sass',
          cssDir: 'css',
          environment: 'production'
        }
      }
    },

    // Task: Uglify
    uglify: {
      target: {
          files: {
            'build/output.min.js': ['src/input.js']
          }
        }
      }
    },

    // Task: Connect - Faz parte da task watch, cria um servidor Node
    connect: {
      options: {
        port: 9000
        hostname: 'localhost',
        livereload: 35729
      },
      livereload: {
        options: {
          open: true
        }
      }
    },

    // Task: Watch
    watch: {
      // Assiste as mudanças nos arquivos compilados pelo Compass
      compass: {
        // Todos os arquivos que terminem com a extensão .scss ou .sass
        // no diretório sass, até os que estão em outros diretórios
        // dentro do diretório sass
        files: ['sass/**/*.{.scss,sass}'],
        tasks: ['compass']
      },
      // Assiste as mudanças nos arquivos minificados pelo Uglify
      uglify: {
        // Todos os arquivos que terminem com a extensão .js no diretório js
        files: 'js/*.js',
        tasks: ['uglify']
      },
      // Mudanças nos arquivos HTML
      html: {
        files: '*.html'
      }
    }

  });

  // Carregamos as tasks
  grunt.loadNpmTasks('grunt-contrib-watch');
  grunt.loadNpmTasks('grunt-contrib-uglify');
  grunt.loadNpmTasks('grunt-contrib-compass');

  // Registramos as tasks
  grunt.registerTask('default', ['connect', 'watch']);

};

{% endhighlight %}

Acredito que tenha ficado mais fácil de entender agora.

</article>

<article>

##Otimizando o Gruntfile

Você reparou que a cada plugin que você instala, você tem que chamar ele no `Gruntfile.js`, e isso é um processo manual, o que não faz muito sentido, já que nosso objetivo é automatizar ao máximo nossas tarefas repetitivas. Mas adivinha, temos um plugin que carrega automaticamente nossos plugins, o salvador da pátria é o `load-grunt-task` criado pelo <a href="https://github.com/sindresorhus" target="_blank">Sindre Sorhus</a>. Vamos instalar ele: `npm install load-grunt-tasks --save-dev` e vamos editar nosso `Gruntfile.js`:

{% highlight js %}

// ECMAScript 5' strict mode
'use strict';

// Função modular
module.exports = function(grunt) {

  // Carregamos as tasks
  require('load-grunt-tasks')(grunt);

  // Iniciamos a configuração
  grunt.initConfig({

    // Busca o package.json
    pkg: grunt.file.readJSON('package.json');

    // Tasks...

  });

  // Registramos as tasks
  grunt.registerTask('default', ['connect', 'watch']);

};

{% endhighlight %}

Bem melhor, não?

Antes:

{% highlight js %}
...
grunt.loadNpmTasks('grunt-contrib-watch');
grunt.loadNpmTasks('grunt-contrib-uglify');
grunt.loadNpmTasks('grunt-contrib-compass');

{% endhighlight %}

Depois:

{% highlight js %}
require('load-grunt-tasks')(grunt);
{% endhighlight %}

Outra forma de otimizar nosso `Gruntfile.js`, é definir variáveis/paths dos diretórios que usamos, podemos fazer isso da seguinte forma:

{% highlight js %}
...
meta {
  srcPathSass: 'src/sass',
  srcPathJS: 'src/js',
  buildPathCSS: 'build/css',
  buildPathJS: 'build/js'
}
...
{% endhighlight %}

E nosso `Gruntfile.js` fica da seguinte forma:

{% highlight js %}

// ECMAScript 5' strict mode
'use strict';

// Função modular
module.exports = function(grunt) {

  // Carregamos as tasks
  require('load-grunt-tasks')(grunt);

  // Iniciamos a configuração
  grunt.initConfig({

    // Busca o package.json
    pkg: grunt.file.readJSON('package.json');

    // Paths
    meta {
      srcPathSass: 'src/sass/',
      srcPathJS: 'src/js/',
      buildPathCSS: 'build/css/'
    }

    // Task: Compass
    compass: {
      dist: {
        options: {
          sassDir: '<%= meta.srcPathSass %>',
          cssDir: '<%= meta.buildPathCSS %>',
          environment: 'production'
        }
      }
    },

    // Task: Uglify
    uglify: {
      target: {
          files: {
            '<%= meta.buildPathJS %>/output.min.js': ['<%= meta.srcPathJS %>/input.js']
          }
        }
      }
    },

    // Task: Connect - Faz parte da task watch, cria um servidor Node
    connect: {
      options: {
        port: 9000
        hostname: 'localhost',
        livereload: 35729
      },
      livereload: {
        options: {
          open: true
        }
      }
    },

    // Task: Watch
    watch: {
      // Assiste as mudanças nos arquivos compilados pelo Compass
      compass: {
        // Todos os arquivos que terminem com a extensão .scss ou .sass
        // no diretório sass, até os que estão em outros diretórios
        // dentro do diretório sass
        files: ['<%= meta.srcPathSass %>/**/*.{.scss,sass}'],
        tasks: ['compass']
      },
      // Assiste as mudanças nos arquivos minificados pelo Uglify
      uglify: {
        // Todos os arquivos que terminem com a extensão .js no diretório js
        files: '<%= meta.srcPathJS %>/*.js',
        tasks: ['uglify']
      },
      // Mudanças nos arquivos HTML
      html: {
        files: '*.html'
      }
    }

  });

  // Registramos as tasks
  grunt.registerTask('default', ['connect', 'watch']);

};

{% endhighlight %}

Definir essas paths é muito útil quando temos vários diretórios.

</article>

<article>

##Conclusão

Grunt é daquelas ferramentes que vicia, você usa em um projeto é quer usar em todos os outros projetos. Isso foi apenas um resumo do básico, existe muito mais a ser explorado e, um bom lugar para começar isso é o próprio site do Grunt: <a href="http://gruntjs.com" target="_blank">gruntjs.com</a>.

</article>

<article>

##Licença

**COM EXCEÇÃO DOS LINKS DE OUTROS AUTORES AQUI CITADOS**:

{% highlight bash %}

IDNC = I DO NOT CARE

USE DA FORMA QUE QUISER, POR SUA CONTA E RISCO.
FIQUE A VONTADE PARA COPIAR, REPLICAR O CONTEÚDO AQUI DESCRITO, NÃO PRECISA NEM CITAR A FONTE, SE ISSO VAI AJUDAR ALGUÉM DE ALGUMA FORMA JÁ ESTÁ VALENDO.
{% endhighlight %}

</article>

</section>
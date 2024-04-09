Univesidade Lusófona
**Programação Web**

# Ficha 6: O poder da arquitetura MVT na criação de websites

### Objetivo:
* Familiarizar-se com as camadas View e Template da arquitetura Model-View-Template (MVT). Nesta ficha não integraremos ainda a camada de modelação; tal acontecerá na ficha 7.
* Familiarizar-se com a criação de 3 websites simples, sistematizando o processo de criação de aplicações.
* Familiarizar-se em particular com criação de rotas em urls.py, de funções em views.py e de templates HTML.

### Índice:
* &alpha;. Introdução ao HTML `<>`
* A. noobsite, páginas soltas 👶
* B. pwsite, o meu primeiro website 😎
* C. website a seu gosto 😎
* &omega; Entrega 📦

# &alpha;. Introdução ao HTML `<>`

O HTML é uma linguagem de marcação para construir páginas Web (*HyperText Markup Language*). Os ficheiros HTML possuem marcadores ou etiquetas (*tags*), palavras entre parênteses angulares (`<` e `>`) que são comandos de formatação da linguagem, para estruturar e estilizar aos conteúdos. 

Por exemplo, no elemento `<p>Isto é um parágrafo.</p>`:
* `<p>` é o marcador de abertura
* `</p>` é o marcador de fecho
* `Isto é um parágrafo.` será o conteúdo afetado pelo marcador <p>, que neste caso formatará como um parágrafo separado no documento HTML.

<details>
 
 <summary><b>Clique para ver os marcadores usados nesta ficha</b></summary>

* `<h1>` = marcador que define um titulo - heading1, a fonte ficando graaande (`<h2>` um subtítulo, `<h3>` um subsubtítulo, ...)
* `<p>` = marcador que define um parágrafo
* `<ul>` = marcador que define uma lista não numerada (`<ol>` para lista numerada)
* `<li>` = marcador que define uma linha
* `<a>` = marcador de âncora para hiperlink, especificado como valor do atributo `href` 
* `<nav>` = marcador de menu de navegação, contendo hiperlinks para outras páginas
- `<html lang="pt">`: Define o início do documento HTML e especifica o idioma (neste caso, português).
- `<head>`: Define informações sobre o documento, como título, metadados e links para scripts e estilos.
- `<meta charset="UTF-8">`: Define o conjunto de caracteres (UTF-8) para garantir a correta exibição de caracteres especiais.
- `<meta name="viewport" content="width=device-width, initial-scale=1.0">`: Define como o conteúdo deve ser renderizado em dispositivos móveis.
- `<title>`: Define o título da página, exibido na barra de título do navegador.
- `<style>`: Permite incluir estilos CSS diretamente no documento HTML.
- `<body>`: Define o corpo do documento, onde todo o conteúdo visível é colocado.
- `<header>`, `<main>`, `<footer>`: São elementos semânticos (sem formatação específica que os distinga) que definem partes específicas do conteúdo da página (cabeçalho, conteúdo principal e rodapé, respectivamente).

Estes marcadores são fundamentais para criar a estrutura e o conteúdo de uma página web, permitindo que os desenvolvedores organizem e apresentem informações de forma clara e semântica.

Dentro de um marcador podem ser especificados pares de `atributo="valor"`. Os atributos modificam os resultados padrões dos elementos e os valores caracterizam essa mudança. Utilizará nesta ficha o atributo:
* `href`= atributo que define o URL da hiperligação

</details>


# A. `noobsite`, páginas soltas 🤓

Neste primeiro exercício, criará o website mais simples do mundo! Um conjunto de páginas sem HTML nem hiperlinks, apenas para se familiarizar com `urls.py` e `views.py`.

## 1. criação da aplicação ✨

No seu projeto do PythonAnyWhere, crie a aplicação `noobsite`:

```bash
python manage.py startapp noobsite
```

## 2. configuração 🔧

Na sua pasta `project`:
1. no ficheiro `project/settings.py`, adicione à lista INSTALLED_APPS a aplicação `noobsite`
1. no ficheiro `project/urls.py`:
    * importe a função `include` . 
    * na lista `urlpatterns` insira um novo `path` que encaminhe o URL `noobsite/` para `noobsite.urls`. O código será o seguinte:

```Python
# urls.py

from django.contrib import admin
from django.urls import path, include   # incluir include


urlpatterns = [
    path('admin/', admin.site.urls),
    path('noobsite/', include('noobsite.urls')),  # novo path 
]
```

## 3. views.py ⚙️

***No MVT, a camada de View lida com a lógica de negócios e a preparação dos dados. É implementada pelo ficheiro views.py, um conjunto de funções, cada uma responsável por responder ao pedido (request) de um recurso (URL), retornando o recurso pedido, um template HTML eventualmente renderizado com dados e customizado. Faz assim a interligação entre os dados e os templates (conteúdo retornado), respondendo aos pedidos encaminhados via urls.***

Crie, no ficheiro `views.py`, uma função responsável por responder com uma frase muito simples.

```Python
# noobsite/views.py

from django.http import HttpResponse

def index_view(request):
    return HttpResponse("Olá n00b, esta é a página web mais básica do mundo!")
```

Crie mais três funções diferentes a seu gosto, que retornem coisas diferentes.

## 4. urls.py ✉️

***Na arquitetura MVT do Django, existe uma camada (URLConf) relacionada com a View que é responsável pelo mapeamento de rotas para funções de view. Esta camada é implementada no ficheiro urls.py. Nela se definem padrões de URL para a aplicação, e associa-os a funçoes de view específicas.***

Na pasta noobsite, crie um novo ficheiro `urls.py` com o seguinte conteúdo:

```Python
# noobsite/urls.py

from django.urls import path
from . import views  # importamos views para poder usar as suas funções

urlpatterns = [
    path('index/', views.index_view),
]
```

***Neste caso, a rota `index/` é mapeada na função `views.index_view`, querendo dizer que, sempre que a rota é acedida num browser (`a222222.pythonanywhere.com/noobsite/index/`), a função `views.index_view` é executada. A lista `urlpatterns` encaminha (*routes*) URLs para funções em views.py. Neste caso, encaminha o URL `index/` para a função `view.index_view`.***

Adicione URLs para as restantes funções que definiu.

## 5. Ready... GO! 🏁

* ⟳ Recarregue (reload) a aplicação premindo no botão "Reload", e abra numa página a aplicação.
* teste os URL que criou ( por exemplo `http://a222222.pythonanywhere.com/noobsite/index` ), e verifique se as respectivas funções retornam o devido.

Parabéns, criou o seu primeiro website 🥳.



# B. `pwsite`, o meu primeiro website 😎

Crie agora um segunto website, mais refinado, sobre programação web. Será um conjunto de páginas HTML com hiperlinks entre si, para se familiarizar ainda mais com `urls` e `views`, e agora também com `templates HTML`.

## 1. criação da aplicação ✨

No seu projeto do PythonAnyWhere, crie uma nova aplicação `pwsite`:

```bash
python manage.py startapp pwsite
```

## 2. configuração 🔧

Na sua pasta project:
* no ficheiro `project/settings.py`, à lista INSTALLED_APPS adicione a aplicação `pwsite`
* no ficheiro `project/urls.py`, e de forma semelhante à Secção A.2, insira um novo `path` que encaminhe o URL `pwsite/` para `pwsite.urls`.

## 3. Camada de Template 🖺
***A camada de Template é responsável pela apresentação dos dados ao utilizador final. Ela define a aparência visual da página da web, utilizando marcação HTML com elementos de template Django (geralmente em linguagem de template Django, que é uma extensão do HTML com tags e filtros específicos do Django) para inserir dinamicamente dados fornecidos pela camada de View. Os templates do Django permitem que os desenvolvedores criem páginas da web dinâmicas de forma eficiente, separando a lógica de apresentação dos dados da lógica de negócios subjacente (View).***

Comecemos assim por construir conteúdos que queremos poder apresentar ao utilizador final. 

1. Na pasta `pwsite`, crie a pasta `templates`, e dentro dessa uma pasta `pwsite`.
2. Crie um ficheiro `index.html` (ficando com o caminho `/home/axxxxxx/project/pwsite/templates/pwsite/index.html`) e insira o conteúdo em baixo.
3. Crie também o ficheiro `sobre.html` e insira o conteúdo em baixo.

Alguns comentários:
* É importante ter o HTML bem indentado, para garantir visualmente que não nos esquecemos de marcadores de fecho.
* No elemento <style> podemos estilizar elementos HTML (o chamado CSS). Neste caso, `background:purple` indica que o body tem cor de fundo roxo, e `color:white` que a cor de texto branco. Mude a seu gosto estes atributos. Daqui a umas semanas aprenderá muito mais sobre esta tecnologia CSS.

#### index.html
```HTML
<!DOCTYPE html>
<html lang="pt">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Programação Web</title>
    <style>
        body {
            background: purple;
            color: white;
        }
    </style>
</head>
<body>
    <header>
        <h1>Programação Web</h1>
    </header>

    <main>
        <h2>Construindo o Futuro da Web</h2>
        <p>Neste curso, exploraremos diversas tecnologias essenciais para o desenvolvimento web moderno:</p>
        <ul>
            <li><strong>Python e Django:</strong> Utilizados para construir aplicações web robustas e escaláveis, para perfecionistas com prazos.</li>
            <li><strong>HTML, CSS e JavaScript:</strong> Essenciais para criar a estrutura, estilo e interatividade das páginas web.</li>
        </ul>
        <p>Vamos mergulhar a fundo nestas tecnologias e aprender a criar experiências incríveis na web!</p>
    </main>

    <footer>
        <p>&copy; 2024 Programação Web, Universidade Lusófona - Todos os direitos reservados.</p>
    </footer>

</body>
</html>
```

#### sobre.html


```html
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Programação Web</title>
</head>
<body>

    <header>
        <h1>Programação Web</h1>
    </header>

    <main>
      <h2>Descrição</h2>
      <p>A disciplina de Programação Web na Universidade Lusófona é oferecida aos estudantes dos cursos de Engenharia Informática e Informática de Gestão no 2º ano e segundo semestre.</p>
      <p>Neste curso, os alunos mergulham nas tecnologias e conceitos fundamentais para o desenvolvimento de aplicações web modernas e escaláveis.</p>

      <h2>Conteúdo</h2>
      <p>Os alunos aprenderão a utilizar linguagens como HTML, CSS e JavaScript para criar interfaces de usuário interativas e responsivas.</p>
      <p>Também serão introduzidos aos frameworks de desenvolvimento web, como Django, que facilitam a construção de aplicações web robustas e eficientes.</p>

      <h2>Objetivos de Aprendizagem</h2>
      <p>O principal objetivo desta disciplina é capacitar os alunos com as habilidades necessárias para projetar, desenvolver e implantar aplicações web funcionais e esteticamente atraentes.</p>
      <p>Além disso, os alunos serão incentivados a explorar as melhores práticas de desenvolvimento web, bem como a importância da acessibilidade, usabilidade e segurança na criação de websites e aplicações.</p>
    </main>

    <footer>
        <p>&copy; 2024 Programação Web, Universidade Lusófona - Todos os direitos reservados.</p>
    </footer>

</body>
</html>
```
#### interesses.html

Crie uma terceira página onde fala daquilo que tem mais gostado de aprender em PW, coisas que gostaria de aprender ou acha interessante nesta área, ou ideias de sites que possa vir a fazer.


## 4. Camada de View (implementada por views.py) ⚙️

***No MVT, a camada de View lida com a lógica de negócios e a preparação dos dados. É implementada pelo ficheiro views.py, um conjunto de funções, cada uma responsável por responder ao pedido (request) de um recurso (URL), retornando o recurso pedido, um template HTML eventualmente renderizado com dados e customizado. Faz assim a interligação entre os dados e os templates (conteúdo retornado), respondendo aos pedidos encaminhados via urls.***

No ficheiro `views.py`, crie funções que renderizem o conteúdo. Por exemplo, para retornar o ficheiro `index.html` está implementada a função `index_view` (nas funções view use o prefixo `_view`).

```Python
# pwsite/views.py

from django.shortcuts import render

def index_view(request):
    return render(request, "pwsite/index.html")
```

Inclua uma função para renderizar `sobre.html` e outra `interesses.html`. 

Experimente passar como contexto a data, e apresente-a no footer em vez do ano, recorrendo ao módulo datetime, de forma a que esta apareça na pagina home (veja os slides da aula).

## 5. urls.py ✉️

***Na arquitetura MVT do Django, existe uma camada extra, URLConf, relacionada com a View. É responsável pelo mapeamento de rotas para funções de view. Esta camada é implementada no ficheiro urls.py. Nela se definem padrões de URL para a aplicação, associados a funçoes de view específicas.***

Na pasta `/pwsite`, crie um novo ficheiro `urls.py`. Em baixo apresenta-se já configurado com a rota para index_view.

Alguns comentários:
* declaramos `app_name = 'pwsite'`, para evitar qualquer ambiguidade de URLs, quando temos multiplas aplicações num mesmo projeto. 
* A lista `urlpatterns` encaminha (*routes*) URLs para funções em views.py. Neste caso, encaminha o URL `index/` para a função `view.index_view`. Adicione URLs para as restantes funções que definiu.
* Cada rota tem um `name`. Será necessário para construir hiperlinks.

```Python
# pwsite/urls.py

from django.urls import path
from . import views  # importamos views para poder usar as suas funções

app_name = 'pwsite'

urlpatterns = [
    path('index/', views.index_view, name='index'),
]
```

## 6. hiperlinks 🔗

Uma das propriedades chave de um website é podermos navegar entre as páginas HTML através de hiperlinks. Adicione um menu de navegação com hiperlinks para cada uma das páginas, permitindo assim navegar de uma pagina para a outra. Para tal, 
* crie um marcador `<nav>` de navegação
* dentro deste crie marcadores `<a>` com hiperlinks para as três páginas.
* Insira este elemento em todas as páginas HTML, dentro do elemento `<header>`, por baixo do elemento `<h1>`.

Em baixo, está o exemplo de um elemento `<nav>` apenas com um hiperlink `<a>`.  
      
```html
<nav>
  <a href="{% url 'pwsite:index' %}">Introducao</a>
</nav>
```

Alguns detalhes:
* o atributo `href` (hipertext reference) especifica o destino do link, um URL para o qual o link aponta, e para onde será redirecionado se o utilizador clicar neste.
* `{% url 'pwsite:index' %}`é um bloco da linguagem template do Django que especifica a rota: identifica o nome da aplicação (`pwsite`, que foi definido na variável `app_name` em `pwsite/urls.py`) e identifica a respetiva rota (`index`) 



## 7. Ready... GO! 🎉 

* ⟳ Recarregue (reload) a aplicação premindo no botão "Reload", e abra numa página a aplicação.
* teste os URL que criou, e verifique se as respectivas funções retornam o devido.

Parabéns, criou o seu segundo website 🥳🥳!


# C. Crie um website a seu gosto

Crie uma aplicação a seu gosto. Relembre os passos:
1. ✨ criação da aplicação com `python manage.py startapp novaapp`
2. 🔧 configuração do ficheiro `project/settings.py` e `project/settings.py` com info da nova aplicação
3. `<>` criação da pasta `templates/novaapp`, e de um conjunto de pelo menos 3 ficheiros HTML simples, com conteúdos a seu gosto. se não tiver ideias de texto, pode usar https://www.lipsum.com/ para gerar texto em latim. o importante não é o conteudo, mas os passos do processo. Todas as páginas deverão ter um `header` e `footer` semelhante.
4.  ⚙️ definição em views.py de funções que renderizem os templates.
5. ✉️ criação do ficheiro `novaapp/urls.py` (use como base o ficheiro `project/urls.py`), definindo um `app_name`, e em urlpatterns os paths com URLs e respetivas funções em views com um `name` cada.
6. 🔗 criação de menu de navegação com hiperlinks para todas as páginas, que deverá estar presente no header de todas as páginas criadas.
7. ⟳ Recarregar (reload) a aplicação. Eventuais erros serão apresentados de forma explícita, pois está em modo debug.

Parabéns, criou o seu terceiro website 🥳🥳🥳! 

# &omega; Entrega 📦

Submeta no Moodle o link para cada uma das suas aplicações, Adicione `pwprofs` em Account\Education\teacher, para os professores poderem ajudar e verificar o código desenvolvido. 

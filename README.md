Univesidade Lusófona
**Programação Web**

# Ficha 6: O poder da arquitetura MVT na criação de websites

### Objetivo:
* Familiarizar-se com a criação de websites simples.
* Familiarizar-se com urls, views t templates HTML 
* Nesta ficha não exploraremos ainda o models.

### Índice:
* &alpha;. Introdução ao HTML `<>`
* A. noobsite, o meu primeiro website 👶
* B. pwsite 😎
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


# A. `noobsite`, o meu primeiro website 👶

Neste primeiro exercício, criará o website mais simples do mundo! Um conjunto de páginas sem HTML nem hiperlinks, para se familiarizar com `urls` e `views`.

## 1. criação da aplicação ✨

No seu projeto do PythonAnyWhere, crie a aplicação `noobsite`:

```bash
python manage.py startapp noobsite
```

## 2. configuração 🔧

Na sua pasta project:
1. no ficheiro `project/settings.py`, à lista INSTALLED_APPS adicione a aplicação `noobsite`
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

As views são funções responsáveis por responder ao pedido (request) de um recurso (URL), retornando o recurso pedido, um template HTML eventualmente renderizado com dados e customizado. Fazem assim a interligação entre os dados e os templates (conteúdo retornado), respondendo aos pedidos encaminhados via urls.

```Python
# project/views.py

from django.http import HttpResponse

def index_view(request):
    return HttpResponse("Olá n00b, esta é a página web mais básica do mundo!")
```

Crie mais três funções diferentes a seu gosto, que retornem coisas diferentes.

## 4. urls.py ✉️

Na pasta noobsite, crie um novo ficheiro `urls.py` com o seguinte conteúdo:

```Python
# noobsite/urls.py

from django.urls import path
from . import views  # importamos views para poder usar as suas funções

urlpatterns = [
    path('index/', views.index_view),
]
```

A lista urlpatterns encaminha (*routes*) URLs para funções em views.py. Neste caso, encaminha o URL `index/` para a função `view.index_view`. Adicione URLs para as restantes funções que definiu.

## 5. Ready... GO! 🏁

* Recarregue (reload) a aplicação premindo no botão "Reload", e abra numa página a aplicação.
* teste os URL que criou ( por exemplo `http://a222222.pythonanywhere.com/noobsite/index` ), e verifique se as respectivas funções retornam o devido.

Parabéns, criou o seu primeiro website 🥳.



# B. `pwsite`, agora sim 😎

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

## 3. templates HTML 🖺

Designa-se de template um ficheiro HTML retornado ao browser por uma função view específica, eventualmente renderizado com conteúdos. Começamos assim por construir os conteúdos que teremos para retornar a um cliente. 

Na pasta `pwsite`, crie a pasta `templates`, e dentro dessa uma pasta `pwsite`. Crie um ficheiro `index.html` (ficando com o caminho `/home/axxxxxx/project/pwsite/templates/pwsite/index.html`) e insira o conteúdo em baixo.

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
Apesar de não ser obrigatório, é importante ter o HTML bem indentado, para garantir visualmente que não nos esquecemos de marcadores de fecho.

Conforme falado na aula, no elemento <style> podemos estilizar elementos HTML. Neste caso, `background:purple` indica que o body tem cor de fundo roxo, e `color:white` que a cor de texto branco. Mude a seu gosto para as outras páginas. 

#### sobre.html
crie também o ficheiro `sobre.html`

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


## 4. views.py ⚙️

No ficheiro views, crie funções que renderizem o conteúdo. Para index.html será

```Python
# pwsite/views.py

from django.shortcuts import render

def index_view(request):
    return render(request, "pwsite/index.html")
```

Inclua uma função para renderizar sobre.html e interesses.html. Adicione a cada rota um valor para `name`. Será necessário para construir hiperlinks.

Experimente passar como contexto a data, e apresente-a no footer em vez do ano, recorrendo ao módulo datetime, de forma a que esta apareça na pagina home (veja os slides da aula).

## 5. urls.py ✉️

Na pasta noobsite, crie um novo ficheiro `urls.py` com o seguinte conteúdo:

```Python
# pwsite/urls.py

from django.urls import path
from . import views  # importamos views para poder usar as suas funções

app_name = 'pwsite'

urlpatterns = [
    path('index/', views.index_view, name='index'),
]
```

A lista urlpatterns encaminha (*routes*) URLs para funções em views.py. Neste caso, encaminha o URL `index/` para a função `view.index_view`. Adicione URLs para as restantes funções que definiu.

Definimos `app_name` para especificar o nome da aplicação, a ser usado nos hiperlinks.

## 6. hiperlinks 🔗

Uma das propriedades chave de um website é podermos navegar entre as páginas HTML através de hiperlinks. Vamos adicionar um menu de navegação com hiperlinks em cada uma das páginas. Será um marcador <nav> com vários marcadores <a>, um por hiperlink. Constroi-se especificando o valor de `name` que foi dado em `urls.py` à rota. `{% url 'index' %}`é um bloco da linguagem template do Django. Falaremos mais em detalhe na proxima aula.

```html
<nav>
  <a href="{% url 'index' %}">Introducao</a>
</nav>
```

Crie hiperlinks para as restantes duas páginas. Copie este elemento em todas as páginas, dentro do elemento `header`, por baixo do elemento `<h1>`.


## 7. Ready... GO! 🎉 

* Recarregue (reload) a aplicação premindo no botão "Reload", e abra numa página a aplicação.
* teste os URL que criou, e verifique se as respectivas funções retornam o devido.

# &omega; Entrega 📦

Submeta no Moodle o link para cada uma das suas aplicações, Adicione `pwprofs` em Account\Education\teacher, para os professores poderem ajudar e verificar o código desenvolvido. 

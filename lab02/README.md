# Lab02 - Data Flow & Mensagens

---

## Tarefa sobre catálogo de componentes

No diretório [s02catalog em santanche/component2learn](https://github.com/santanche/component2learn/blob/master/labs/02-data-flow_messages/notebooks/data-flow/s02catalog) está o notebook `components-01-catalog.ipynb` que apresenta o catálogo de componentes e o modo de conectá-los (visto pela perspectiva blackbox - externa) para montar uma composição. 

Ele apresenta seis tarefas que devem ser resolvidas. A entrega desse lab será formada pelo notebook `components-01-catalog.ipynb` com as seis tarefas resolvidas.

### Arquivo do Projeto

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/FernandoMorais/unicamp-engsoft-2020-inf331/master?filepath=lab02%2Fnotebook%2Fdata-flow%2Fs02catalog%2Fcomponents-01-catalog.ipynb)

- [notebook/data-flow/s02catalog/components-01-catalog.ipynb](notebook/data-flow/s02catalog/components-01-catalog.ipynb)

---

## Tarefa Web Components 1

Crie quatro botões com rótulos `Mundo`, `Brasil P`, `Brasil E` e `Bahia` que, ao serem clicados, publiquem notícias nos seguintes tópicos (conteúdo a sua escolha):
* `noticia/mundo/politica`
* `noticia/brasil/politica`
* `noticia/brasil/esporte`
* `noticia/bahia/esporte`

O segundo nível do tópico indica a região da notícia e o terceiro o assunto. Associe a cada tópico o texto de uma mensagem de sua criação.

Crie três personagens (`doctor`, `nurse` e `patient`) usando o `<dcc-lively-talk>`. Cada um deles deve mostrar seletivamente (em seu balão) notícias publicadas pelos botões, conforme os seguintes critérios:
* `doctor` - mostra notícias sobre política (independentemente de região);
* `nurse` - mostra notícias cuja região é o Brasil (independentemente do assunto);
* `patient` - mostra todas as notícias.

### Composição de Componentes Web

_Para visualizar os componentes utilize o ambiente [DCC Playground](https://santanche.github.io/component2learn/labs/02-data-flow_messages/notebooks/messages/dccs/playground/)._

~~~html
<dcc-trigger
    id="mundo" label="Mundo"
    action="noticia/mundo/politica"
    value="<p><b>Multidão protesta em Beirute; premiê cogita antecipar eleições</b><br/>Milhares de pessoas saíram às ruas de Beirute neste sábado (08/08/2020) para protestar contra o governo e o sistema político vigente no Líbano, acusados de serem os responsáveis pela explosão que devastou a zona portuária da cidade e deixou pelo menos 154 mortos.<br/><a href='https://www.terra.com.br/noticias/mundo/multidao-protesta-em-beirute-premie-cogita-antecipar-eleicoes,d3776042d84bc62b93d6fe283fa041e2d2d4y9v8.html' target='blank'>Veja mais...</a></p>">
</dcc-trigger>

<dcc-trigger 
    id="brasil_p" label="Brasil P" 
    action="noticia/brasil/politica"
    value="<p><b>Bolsonaro: não pretendo participar de eleições no 1º turno</b><br/>O presidente Jair Bolsonaro disse neste sábado, 08/08/2020, em sua conta oficial no Facebook, que não pretende se envolver na disputa em primeiro turno das eleições municipais. &quot;Não pretendo participar das eleições municipais no 1º turno&quot;, afirmou. Na publicação, o presidente disse que esse assunto foi pauta no café da manhã com o diretor do Paraná Pesquisas, Murilo Hidalgo.<br/><a href='https://www.terra.com.br/noticias/brasil/politica/bolsonaro-nao-pretendo-participar-de-eleicoes-no-1-turno,845e4559f57bba590e3b01ff39caa811q4h28d2x.html' target='blank'>Veja mais...</a></p>">
</dcc-trigger>

<dcc-trigger 
    id="brasil_e" label="Brasil E" 
    action="noticia/brasil/esporte"
    value="<p><b>Decisão do Paulista acontece em dia que Brasil chega a 100 mil mortos por Covid e Andres Sanchez lamenta</b><br/>O presidente do Corinthians, Andres Sanchez, lamentou em uma postagem publicada no twitter, que a final do Campeonato Paulista acontece, por coincidência, com o dia em que o Brasil chegou a triste marca de 100 mil mortos pela Covid-19.<br/><a href='https://www.terra.com.br/esportes/lance/decisao-do-paulista-acontece-em-dia-que-brasil-chega-a-100-mil-mortos-por-covid-e-andres-sanchez-lamenta,b6703bc05455dd38e59af3d72cbffd1af7j76hd8.html' target='blank'>Veja mais...</a></p>">
</dcc-trigger>

<dcc-trigger 
    id="bahia" label="Bahia" 
    action="noticia/bahia/esporte"
    value="<p><b>Com um a mais, Bahia para na defesa do Atlético-BA na ida da decisão do estadual</b><br/>Ninguém conseguiu encaminhar vantagem para o segundo jogo da decisão do Campeonato Baiano. Jogando no Estádio de Pituaçu, o mandante Atlético de Alagoinhas, mesmo tendo um jogador a menos, resistiu a pressão do Bahia e colaborou bastante para o resultado de 0 a 0 que deixa tudo &quot;em aberto&quot; para o confronto do próximo sábado 08/08/2020 às 16h30.<br/><a href='https://www.terra.com.br/esportes/lance/com-um-a-mais-bahia-para-na-defesa-do-atletico-ba-na-ida-da-decisao-do-estadual,7d6467f64e0f80dd489b0d8a7e217138nsxrnnln.html' target='blank'>Veja mais...</a></p>">
</dcc-trigger>

<dcc-lively-talk 
    id="doctor"
    character="doctor"
    speech="<i>Notícias de Política no Brasil e no Mundo:</i>">
  <subscribe-dcc topic="noticia/+/politica"></subscribe-dcc>
</dcc-lively-talk>

<dcc-lively-talk 
    id="nurse"
    character="nurse"
    speech="<i>Notícias do Brasil:</i>">
  <subscribe-dcc topic="noticia/brasil/+"></subscribe-dcc>
  <subscribe-dcc topic="noticia/bahia/esporte"></subscribe-dcc>
</dcc-lively-talk>

<dcc-lively-talk 
    id="patient"
    character="patient"
    speech="<i>Todas as Notícias do Brasil e do Mundo:</i>">
  <subscribe-dcc topic="noticia/#"></subscribe-dcc>
</dcc-lively-talk>
~~~

---

## Tarefa Web Components 2

Crie dois componentes RSS usando o `<dcc-rss>` que assinem os canais:
  * canal 1 (ciência): https://www.wired.com/category/science/feed
  * canal 2 (design): https://www.wired.com/category/design/feed

Crie um agregador de mensagens usando o `<dcc-aggregator>` para notícias de ciência.

Crie três personagens (`doctor`, `nurse` e `patient`) usando o `<dcc-lively-talk>`. Cada um deles deve mostrar seletivamente (em seu balão) RSSs ou agregados, conforme os seguintes critérios:
* `doctor` - mostra notícias agregadas de ciências;
* `nurse` - mostra notícias de ciências;
* `patient` - mostra notícias de design.

### Composição de Componentes Web

_Para visualizar os componentes utilize o ambiente [DCC Playground](https://santanche.github.io/component2learn/labs/02-data-flow_messages/notebooks/messages/dccs/playground/)._

~~~html
<dcc-trigger label="Next Item" action="next/rss">
</dcc-trigger>

<dcc-rss source="https://www.wired.com/category/science/feed" publish="rss/science">
  <subscribe-dcc topic="next/rss" role="step"></subscribe-dcc>
</dcc-rss>

<dcc-rss source="https://www.wired.com/category/design/feed" publish="rss/design">
  <subscribe-dcc topic="next/rss" role="step"></subscribe-dcc>
</dcc-rss>

<dcc-aggregator publish="aggregate/science" quantity="5">
  <subscribe-dcc topic="rss/science"></subscribe-dcc>
</dcc-aggregator>

<dcc-lively-talk 
    id="doctor"
    character="doctor"
    speech="<i>Notícias de Ciência:</i>">
  <subscribe-dcc topic="aggregate/science"></subscribe-dcc>
</dcc-lively-talk>

<dcc-lively-talk 
    id="nurse"
    character="nurse"
    speech="<i>Notícia de Ciência:</i>">
  <subscribe-dcc topic="rss/science"></subscribe-dcc>
</dcc-lively-talk>

<dcc-lively-talk 
    id="patient"
    character="patient"
    speech="<i>Notícia de Design:</i>">
  <subscribe-dcc topic="rss/design"></subscribe-dcc>
</dcc-lively-talk>
~~~
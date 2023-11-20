## Lab08 - Soluções em bancos de grafos com análise de rede


## Equipe: VIRUS


## Subgrupo: A  (BOYS)

- Lucas Gabriel Monteiro Da Costa - 183967 
- Pietro Grazzioli Golfeto - 223694 
- Vitor Rodrigues Zanata da Silva - 231718

## Questões a serem analisadas:

Pergunta 1: 

Quais os crop groups cujos ingredientes são mais usados nas receitas? Análise de centralidade. 

Implementação 1:

Itera sobre os ingredientes de cada receita e soma o contador no respectivo crop group do ingrediente. Com isso, descobre-se os crop groups mais utilizados nas receitas, ao computar seu grau da forma descrita.


Pergunta 2: 

Quais são os ingredientes mais usados em conjunto (presentes nas mesmas receitas)? Isso define uma comunidade dos ingredientes.

Implementação 2:

Baseado no algoritmo de Girvan e Newman, que assume que nós de alta centralidade são pontes entre as comunidades, conseguimos partir o grafo em comunidades suficientemente pequenas ao removermos os nós mais centrais e, assim, completar a nossa análise.


Pergunta 3: 

Que receitas possuem o maior número relativo de ingredientes compartilhados? O quão comum ela é? É uma centralidade baseada no grau.

Implementação 3:

Seleciona o peso da aresta entre receitas, que mostra o número de ingredientes em comum (apenas quando esse peso for maior que um threshold para evitar relações não significativas). Divide esse peso pelo número de ingredientes da receita, obtendo um valor normal entre 0 e 1 (X) que significa o quão relacionadas essas receitas são. Fazendo isso para todas as suas receitas relacionadas, tire a média de X e multiplique pelo número de receitas em comum (grau Y do nó). O seu resultado será o coeficiente Z de quão comum e relacionada ela é. Ao selecionarmos as receitas de maiores coeficientes Z, podemos responder à análise.

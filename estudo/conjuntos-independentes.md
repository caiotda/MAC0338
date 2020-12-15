### Conjuntos independentes de um grafo

**Motivação**: dado um tabuleiro de xadrez com n rainhas, **existe uma configuração de posição das rainhas que permite que nenhuma delas se ataque**?

Essa pergunta pode ser respondida ao estudarmos o conjunto independente de um grafo.

**Definição**: um conjunto independente de um grafo é um conjunto de vertices S tal que não não exista aresta conectando diretamente nenhum vertice de S. Ou seja, não há vertice adjacente em S.

Um conjunto independente é máximo se não existe outro conjunto independente contendo mais vértices. Logo:

**Problema do conjunto independente maximo**: S é um conjunto independente maximo de um grafo G se não existe outro conjunto independente X tal que |X| > |S|.

Computacionalmente, não existe algoritmo mais eficiente do que exponencial para **Devolver** o conjunto independente maximo de um grafo. No entanto, existem alternativas mais eficientes para determinar a **existência** de tal conjunto.

O problema das rainhas pode ser resolvido verificando se existe um conjunto independente de tamanho n. Note que, para cada posição de rainha, podemos conectar com esse vértice de posição toda posição que a rainha pode pular. Se existe um conjunto independente, existe um conjunto de posições que não se intersectam, ou seja, as rainhas não se cruzarão.
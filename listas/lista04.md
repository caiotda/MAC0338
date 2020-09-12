# Lista 4

1)

Seja C(n) o número de execuções, no pior caso, da atribuição A[i+1] := A[i] na [linha 5](https://edisciplinas.usp.br/mod/quiz/attempt.php?attempt=2909578&cmid=3141471#line5) de ORDENAÇÃO-POR-INSERÇÃO.

1. O consumo de tempo do algoritmo é proporcional a C(n)? Por que?
2. Quanto vale C(n) no pior caso? Justifique.

***

2)

Dê uma solução da instância (1, ¾, 0) do problema da equação inteira do segundo grau. Justifique. (No editor de texto, use formato TEXT.)



R.: A instância do problema não é valida. Pela definição do problema da equação inteira do segundo grau: "Dados números [inteiros](https://www.ime.usp.br/~pf/analise_de_algoritmos/aulas/dictionary.html#integer) a, b e c, encontrar um número inteiro x tal que  ax² +  bx +  c = 0." b não é inteiro.

***

3)

Qual o consumo de tempo do algoritmo ORDENAÇÃO-POR-INSERÇÃO no melhor caso? Justifique.



No melhor caso o vetor de entrada de tamanho n já está ordenado, então o insertion sort simplesmente  itera o vetor. Assim, assintoticamente, o tempo de execução é igual a n.

***

4) 

"O algoritmo A consome pelo menos Ο(n²) unidades de tempo." Essa afirmação faz sentido? Justifique.



Não. Não faz sentido falar que o algoritmo consome **pelo menos** O(n^2) unidades de tempo, tendo em vista que a notação serve para delimitar superiormente o consumo de unidades de tempo.


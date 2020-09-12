# Lista 4

1)

Seja C(n) o número de execuções, no pior caso, da atribuição A[i+1] := A[i] na [linha 5](https://edisciplinas.usp.br/mod/quiz/attempt.php?attempt=2909578&cmid=3141471#line5) de ORDENAÇÃO-POR-INSERÇÃO.

1. O consumo de tempo do algoritmo é proporcional a C(n)? Por que?
2. Quanto vale C(n) no pior caso? Justifique.



1. Não. No melhor caso (vetor de entrada já está ordenado) a linha 5 não é  executada. Neste caso, a afirmação implicaria que o o consumo de tempo  do algoritmo, mesmo que no melhor caso, é proporcional a n(n-1)/2, o que é falso.

2. No pior caso, a linha 5 é executada 1 + 2 + ... n-1 vezes, resultando em n(n-1)/2 vezes

***

2)

Dê uma solução da instância (1, ¾, 0) do problema da equação inteira do segundo grau. Justifique. (No editor de texto, use formato TEXT.)



R.: A instância do problema não é valida. Pela definição do problema da equação inteira do segundo grau: "Dados números [inteiros](https://www.ime.usp.br/~pf/analise_de_algoritmos/aulas/dictionary.html#integer) a, b e c, encontrar um número inteiro x tal que  ax² +  bx +  c = 0." b não é inteiro.

***

3)

Qual o consumo de tempo do algoritmo ORDENAÇÃO-POR-INSERÇÃO no melhor caso? Justifique.



No melhor caso o vetor de entrada de tamanho n já está ordenado, então o insertion sort simplesmente  itera o vetor. Assim, vale que o tempo do algoritmo está tanto em  Omega(n) quanto O(n) no melhor caso, logo, está em Theta(n).

***

4) 

"O algoritmo A consome pelo menos Ο(n²) unidades de tempo." Essa afirmação faz sentido? Justifique.



Não. Não faz sentido falar que o algoritmo consome **pelo menos** O(n^2) unidades de tempo, tendo em vista que a notação serve para delimitar superiormente o consumo de unidades de tempo.


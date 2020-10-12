# Lista 09

***

1) 

Faça um rastreamento da aplicação do algoritmo  QUICKSORT (sem aleatorização) ao vetor [6  5  4  3  2  1].  Imite o  exemplo C da página *Quicksort*.

[ 6 5 4 3 2 1]

1  [ 5 4 3 2 6]

1 [ 5 4 3 2 ] 6

1 2 [ 4 3 5] 6

1 2 [4 3] 5 6

1 2 3 [4] 5 6

1 2 3 4 5 6

***

2)

Seja A[p .. r] uma permutação de 1 .. n. Submeta A[p .. r] ao QUICKSORT (sem aleatorização) e conte o número total de comparações entre elementos do vetor (linha 4 de DIVIDE). Faça isso para n = 1, 2, 3 e para cada permutação de 1 .. n. Também faça isso para n = 4 e as permutações [1 3 4 2], [2 1 4 3], [3 4 2 1] e [4 3 2 1].

Construa uma tabela para apresentar os resultados. Sua tabela deve ter três colunas:  na coluna 1 coloque as permutações 1 .. n; na coluna 2 coloque o estado do vetor depois da  primeira aplicação de DIVIDE ao vetor da coluna 1; na coluna 3 coloque uma expressão da forma  `a+b+c=d`, sendo `a` o número de comparações  da primeira aplicação de DIVIDE, sendo `b` o número total de comparações que  QUICKSORT  executa ao processar o vetor A[ p.. q−1]; sendo `c` o número total de comparações que  QUICKSORT  executa  ao processar o vetor A[q+1..r); e sendo `d` o valor da soma `a`+`b`+`c`. (É claro que todas as referências a comparações  devem ser entendidas como comparações entre elementos do vetor.) (Dica:  Para calcular `b` e `c`, use as tabelas de n−1, n−2, etc.)

Compare os resultados com a previsão teórica.

```


permutações | estado após primeiro divide | expressão
----------- |-----------------------------|---------------
[1]         | [1]                         | 0 + 0 + 0 = 0
----------------------------------------------------------
[1 2]       | [1] 2                       | 1 + 0 + 0 = 1
----------------------------------------------------------
[2 1]       | 1 [2]                       | 1 + 0 + 0 = 1
----------------------------------------------------------
[1 2 3]     | [1 2] 3                     | 2 + 1 + 0 = 3
----------------------------------------------------------
[1 3 2]     | [1] 2 [3]                   | 2 + 0 + 0 = 2
----------------------------------------------------------
[2 3 1]     | 1 [3 2]                     | 2 + 0 + 1 = 3
----------------------------------------------------------
[2 1 3]     | [2 1] 3                     | 2 + 1 + 0 = 3
----------------------------------------------------------
[3 2 1]     | 1 [2 3]                     | 2 + 0 + 1 = 3
----------------------------------------------------------
[3 1 2]     | [1] 2 [3]                   | 2 + 0 + 0 = 2
----------------------------------------------------------
[1 3 4 2]   | [1] 2 [4 3]                 | 3 + 0 + 1 = 4
----------------------------------------------------------
[2 1 4 3]   | [2 1] 3 [4]                 | 3 + 1 + 0 = 4
----------------------------------------------------------
[3 4 2 1]   | 1 [4 2 3]                   | 3 + 0 + 2 = 5
----------------------------------------------------------
[4 3 2 1]   | 1 [3 2 4]                   | 3 + 0 + 3 = 6
----------------------------------------------------------

```



Pela previsão teórica, o Quicksort tem um desempenho médio de Theta n log n. Isto é, espera-se que, se, por exemplo, dobrarmos o tamanho de um vetor, o seu número de comparações aumenta  um pouco mais do que duas vezes.  No entanto, nota-se que se dobrarmos o tamanho do vetor (por exemplo, de n = 2 para n = 4), o número de comparações pode aumentar em até 5 vezes. Isso provavelmente se deve às constantes escondidas na notação assintótica Theta, que naturalmente é mais fiel aos resultados experimentais para n assintoticamente grandes.
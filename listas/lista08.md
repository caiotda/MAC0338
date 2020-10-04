# Lista 08

***

1) Calcule o número médio de execuções da linha 4 de  Máximo no caso n = 3. (imite o [exemplo A](https://edisciplinas.usp.br/mod/assign/hiring.html#example-A) da página *Análise probabilística e algoritmos aleatorizados*.) Compare com  o valor previsto pela teoria. Parte 2: Calcule o número de execuções da linha 4  em cinco diferentes permutações de 1..5.

Vamos anotar abaixo todas permutações e o número de vezes que a linha 4 é executada para cada permutação:



1,2,3 --- 3
1,3,2 --- 2
2,1,3 --- 2
2,3,1 --- 2
3,2,1 --- 1
3,1,2 --- 1

O que dá uma média de 11/6 execuções. Seja x o número de execuções da linha 4. A previsão teórica é que esse número é a série harmônica x = 	1/1 + 1/2 + 1/3 + ... 1/n. Note que como n = 3, temos que x = 1/1 + 1/2 + 1/3 = 11/6. Ou seja, o valor calculado é exatamente o valor previsto pela teoria.

Parte 2:

1,2,3,4,5 --- 5

1,3,2,4,5 --- 4

1,4,5,3,2 --- 3

1,5,4,3,2 --- 2

5,1,2,3,4 --- 1



***

2) Escreva  um algoritmo recursivo que receba dois vetores  A[1 .. n] e B[1 .. n] e decida se existe um índice i tal que A[i] = B[i]. (Devolva 1 se tal índice existe e devolva 0 em caso contrário.)

Use formato TEXT para digitar sua resposta.

```
busca_auxiliar(A, B, i, j)
1. se i < 0 ou j < 0
2.   devolva 0
3. se A[i] = A[j]
4.  devolva 1
5. a:= busca_auxiliar(A, B, i-1, j)
6. b:= busca_auxiliar(A, B, i, j-1)
7. devolva (a+b)/2 // garante que o valor retornado está em [0, 1]

busca(A, B)
1. devolva busca_auxiliar(A, B, n, n)
```



***

3) Suponha que todos os elementos do vetor A[p .. r] são iguais entre si. Quantas vezes a [linha 4](https://edisciplinas.usp.br/mod/assign/quick.html#lineS4) do algoritmo Divide é executada? Qual o valor do índice que o algoritmo devolve? Parte 2: Qual o valor do índice que Divide devolve quando o vetor é decrescente?

Use formato TEXT para digitar sua resposta.

A linha 4 é executada r - p vezes. O índice devolvido é r.

Quando o vetor é decrescente, o valor retornado é p.
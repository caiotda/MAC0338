# Lista 08

***

1) Calcule o número médio de execuções da linha 4 de  Máximo no caso n = 3. (imite o [exemplo A](https://edisciplinas.usp.br/mod/assign/hiring.html#example-A) da página *Análise probabilística e algoritmos aleatorizados*.) Compare com  o valor previsto pela teoria. Parte 2: Calcule o número de execuções da linha 4  em cinco diferentes permutações de 1..5.

Vamos anotar abaixo todas as permutações de 1..3 com o número correspondente de execuções da linha 4 do algoritmo 'Máximo':



1,2,3 --- 3
1,3,2 --- 2
2,1,3 --- 2
2,3,1 --- 2
3,2,1 --- 1
3,1,2 --- 1

O que resulta em uma média de 11/6 execuções da linha 4. Seja x o número de execuções da linha 4. O valor previsto pela teoria para x é a série harmônica x = 1/1 + 1/2 + 1/3 + ... 1/n. Note que como n = 3, temos que x = 1/1 + 1/2 + 1/3 = 11/6. Ou seja, o valor calculado é exatamente o valor previsto pela teoria.

Parte 2: Abaixo, algumas permutações de 1..5 com o número correspondente de execuções da linha 4 do algoritmo 'Máximo'.

1,2,3,4,5 --- 5

1,3,2,4,5 --- 4

1,4,5,3,2 --- 3

1,5,4,3,2 --- 2

5,1,2,3,4 --- 1

***

2) Escreva  um algoritmo recursivo que receba dois vetores  A[1 .. n] e B[1 .. n] e decida se existe um índice i tal que A[i] = B[i]. (Devolva 1 se tal índice existe e devolva 0 em caso contrário.)

Use formato TEXT para digitar sua resposta.

```
busca(A, B)
1. devolva busca_auxiliar(A, B, n)

busca_auxiliar(A, B, i)
1. se i = 0
2.     devolva 0
3. se A[i] = B[i]
4.     devolva 1
5. devolva busca_auxiliar(A, B, i-1)
```



***

3) Suponha que todos os elementos do vetor A[p .. r] são iguais entre si. Quantas vezes a [linha 4](https://edisciplinas.usp.br/mod/assign/quick.html#lineS4) do algoritmo Divide é executada? Qual o valor do índice que o algoritmo devolve? Parte 2: Qual o valor do índice que Divide devolve quando o vetor é decrescente?

Use formato TEXT para digitar sua resposta.

A linha 4 é executada r - p vezes. O valor do índice devolvido pelo algoritmo é r.

Parte2: Quando o vetor é decrescente, o valor do índice retornado é p.
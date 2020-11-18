## Lista 13

1. [2 pts] Considere a recorrência T(n) = 3 +  2 T(n − 1) para n ≥ 1. O valor inicial é T(0) = 3. Qual a solução da recorrência? Prove sua resposta por indução.

   A solução da recorrência é T(n) = 6*2^n - 3.

   

   Prova por indução em n: Se n = 0, a igualdade vale:

   

   T(0) = 3 = 6 - 3 = 6*2^0 - 3.

   

   Agora tome n >= 1 e suponha como hipótese de indução que:

   T(n-1) = 6 * 2^{n-1} - 3

   2*T(n-1) = 6 * 2 * 2^{n-1} - 6

   2*T(n-1) + 3 = 6 * 2^n - 3; mas T(n) = 2*T(n-1) + 3, logo:

   T(n) = 6 * 2^n - 3.

   

   Está provado por indução em n que T(n) = 6 * 2^n - 3.

   

   

   ***

2. [2 pts] Prove a estrutura recursiva do [problema da mochila booleana](https://www.ime.usp.br/~pf/analise_de_algoritmos/aulas/mochila-bool.html#the-problem). Veja a descrição da estrutura na página *Mochila booleana*.



Primeiro, vamos enunciar a propriedade da estrutura recursiva do problema da mochila Booleana. Seja X uma mochila ótima para a instância (p, v, n, c) para o problema da mochila Booleana. Se n não pertence a X, então X é solução da instância (p, v, n-1, c). Do contrário, X - {n} é solução da insância (p, v, n-1, c- p[n]). 



Parte1: Suponha que X é uma solução ótima para (p, v, n, c) e que n não pertence a X. Vamos provar que isso implica que X é solução de (p, v, n-1, c).

Como a capacidade das duas instancias é a mesma, segue naturalmente que X é uma mochila para a instância (p, v, n-1, c). Vamos mostrar agora que X é mochila otima para essa instancia. Seja V(X) o valor da solução ótima de (p, v, n, c) e v' o valor da solução ótima para (p, v, n-1, c). Como 'n' não pertence a X, vale que V(X) = v'. Como a mochila X apresenta valor ótimo para a instancia , então segue que X é solução ótima para (p, v, n-1, c).

Parte 2: Se n pertence a X, então X - {n} é solução da insância (p, v, n-1, c- p[n]). 



Primeiro, vamos mostrar que X - {n} é uma mochila para a instancia (p, v, n-1, c - p[n]).  

v(X) <= c

v(X) - p[n] <= c - p[n]

v(X - {n}) <= c - p[n]

Agora vamos mostrar por contradição que X - {n} é a mochila ótima da instância (p, v, n-1, c - p[n]).

Suponha que H != X - {n}é uma mochila qualquer da instância. Então para toda mochila H vale que:

v(H) > v(x - {n})

v(H) + p[n] > v(X - {n}) + p[n]

v(H u {n}) > v(x). Mas isso contradiz a hipotese de que X é solução ótima. 

Então vale que v(H) <= v(X - {n}) para toda mochila  H. Assim, X - {n} é mochila ótima da instância.

***

3. [2 pts] Escreva um algoritmo de programação dinâmica Mochila-Prog-Din para o problema da mochila booleana. O seu algoritmo deve preencher a tabela de programação dinâmica (basta adaptar o código do [correspondente algoritmo para o problema subset sum](https://www.ime.usp.br/~pf/analise_de_algoritmos/aulas/mochila-subsetsum.html#Subset-Sum-Prog-Din)) e em seguida usar a tabela para calcular  o vetor característico de uma solução do problema.



```
monta-tabela-mochila (p, v, n, c)
1 para i crescendo de 0 até n
2 	t[i, 0] := 1
3 para j crescendo de 1 até c
4 	t[0, j] := 0
5 	para i crescendo de 1 até n
6		 val := t[i − 1, j]
7 		 se p[i] <= j
8 				val := max(val ,v[i] + t[i − 1, j − p[i]])
9 	     t[i, j] := val
10 devolva t

devolve-solucao(p, n, c)
1.  t := monta-tabela-mochila(p, v, n, c)
2.  se t[n, c] > 0 
3.      j := c
4.      para i := n decrescendo até 1 
5.          se t[i − 1, j] > 0
6.              x[i] := 0
7.        senão x[i] := 1
8.          j := j − p[i]
9.      devolva x[1 .. n]
```



***

4. [2 pts] Mostre que o [problema subset sum](https://www.ime.usp.br/~pf/analise_de_algoritmos/aulas/mochila-subsetsum.html#the-problem)  (veja a página *Subset sum*) é um caso particular —  ou seja, uma coleção de [instâncias](https://www.ime.usp.br/~pf/analise_de_algoritmos/aulas/instance.html#instance) — do problema da mochila booleana. Como um algoritmo para o problema da mochila booleana pode ser usado para resolver o problema subset sum?

O problema subset sum é um caso particular do problema da mochila booleana no qual v[i] = 1,  para todo objeto i. Podemos adaptar o algoritmo monta-tabela-mochila levemente para resolver o problema:

```
monta-tabela-mochila-adaptado-para-subsetsum (p, v, n, c)
1 para i crescendo de 0 até n
2 	t[i, 0] := 1
3 para j crescendo de 1 até c
4 	t[0, j] := 0
5 	para i crescendo de 1 até n
6		 val := t[i − 1, j]
7 		 se p[i] <= j
8 				val := max(val ,v[i] + t[i − 1, j − p[i]])
9 	     t[i, j] := min(val, 1)
10 devolva t[n, c]
```

As diferenças são na linha 9 e 10: na linha 9, garantimos que o valor armazenado em cada posição da tabela é 0 ou 1. Na linha 10, devolvemos 0 ou 1, discriminando se existe subsequencia de soma maxima com n elementos e soma maxima c.
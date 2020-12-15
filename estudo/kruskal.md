### Algoritmo de Kruskal e MSTs

O algoritmo de Kruskal é utilizado para encontrar a **MST de peso mínimo de um grafo**. , onde MST  = Minimum Spanning Tree (arvore geradora mínima)



Suponha que cada aresta uv de um grafo tem um peso p[uv]. p é um vetor de pesos. O peso de um subgrafo qualquer T é a soma dos pesos de todas arestas de T e será denotado por p(T).



Portanto, uma MST é uma árvore geradora do grafo para a qual o peso é mínimo. O problema da MST então é, dado um grafo G com peso nas arestas, encontrar uma MST de G. Note que o problema só tem solução se G for conexo.

**O algoritmo de Kruskal**

Um algoritmo iterativo foi descoberto nos anos 50 para resolver esse problema.

Começamos com uma floresta geradora F de G. A cada iteração, o algoritmo faz uma escolha gulosa, adicionando a F uma aresta de G. **Escolhemos sempre uma aresta de peso mínimo dentre as externas à floresta**.

Uma aresta "a" é externa a F se:

1. Não pertence a F
2. O grafo F + a é uma floresta. (ou seja, não tem circuitos.)

Inicialmente, a floresta F não tem arestas. No fim da execução do algoritmo, G não tem arestas externas a F.

**Prova de correção do algoritmo**

A prova de correção do algoritmo de Kruskal se baseia no seguinte invariante: F sempre faz parte de alguma MST de G. Se esse invariante for provado, o algoritmo está correto

O invariante é trivialmente correto na primeira iteração, onde F = {}; Tome 'a' uma aresta escolhida pelo algoritmo. Seja M uma MST de G. Se a pertence a M, acabou. Suponha que 'a' não pertence a M. Então Vale que M + a possui um ciclo. Tome b uma aresta externa a F e membro deste ciclo. Como b não foi escolhida pelo algoritmo, vale que P(b) >= P(a). Tome M - b + a; Se P(b) > P(a), então P(M- b + a) < P(M), o que é um absurdo. Então vale que P(b) = P(a) e M - b + a é uma MST. Assim, 'a' pertence a uma MST e a prova acabou.



**O Algoritmo**

```
MST-Kruskal (G, n, m, p)
1 arestas := Sort-Edges (G, m, p)
2 X := { }
3 Initialize ()
4 para i := 1 até m
5 	uv := arestas[i]
6 	r := Find (u)
7 	s := Find (v)
8 	se r ≠ s
9 		X := X ∪ { uv }
10 		Union (r, s)
11 devolva X
```

Esse algoritmo tem um tempo de execução de O(m + lg n);
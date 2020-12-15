### Lista 14

1) Considere o algoritmo [Componentes](https://www.ime.usp.br/~pf/analise_de_algoritmos/aulas/lista-exr-14.html#Componentes) com as implementações Initialize-3, Find-3  e Union-3 de Initialize, Find e Union respectivamente. Submeta o grafo da figura ao algoritmo tomando as arestas na ordem `ba dc db fe hg hf hd ac eg bf`. (Execute o código de Union-3 *exatamente*.) Dê o estado dos vetores `chefe`  e `alt` no fim da execução do algoritmo. (Escreva esses dois vetores num formato semelhante ao da página Union-find.)

```
a———b———f———e
│   │   │   │
c———d———h———g
```

Vou deixar aqui cada implementação necessaria:

```
Find-3 (v)
1 enquanto chefe[v] ≠ v
2 	v := chefe[v]
3 devolva v
```

```
Union-3 (r, s)  ▷ union-by-rank; r ≠ s
1 se alt[r] > alt[s]
2     chefe[s] := r
3 senão chefe[r] := s
4      se alt[r] = alt[s]
5          alt[s] := alt[s] + 1
```

```
INITIALIZE-3()
1. para cada vertice v
2. 	   dir[v] := v
3. 	   alt[v] := 0
```

``` 
Componentes (G, n)
1 c := n
2 Initialize ( )
3 para cada aresta uv de G
4 	r := Find (u)
5 	s := Find (v)
6 	se r ≠ s
7 		Union (r, s)
8 		c := c − 1
9 devolva c
```

Pai: [b, d, d, h, f, h, h, h]

alt: [0, 1, 0, 2, 0, 1, 0, 3]

***

2) Execute o algoritmo [MST-Kruskal](https://www.ime.usp.br/~pf/analise_de_algoritmos/aulas/MST-kruskal.html#MST-Kruskal) sobre o grafo não-dirigido definido pela  matriz de pesos abaixo, com - representando "∞". Sua resposta deve dar o peso de uma MST  e a lista das arestas da MST, na ordem em que essa lista foi obtida pelo algoritmo.

```
    1  2  3  4  5  6  7  8
  
1   -  3  -  4  5  -  -  -
2   3  -  9  -  6  -  -  -
3   -  9  -  -  8  2  -  -
4   4  -  -  -  6  -  6  7
5   5  6  8  6  -  9  -  8
6   -  -  2  -  9  -  -  -
7   -  -  -  6  -  -  -  8
8   -  -  -  7  8  -  8  -
```

***

3) Encontre um conjunto independente máximo no grafo da dama 5-por-5.  Repita o exercício para o grafo da dama 8-por-8. Dê suas respostas numa figura do tipo da que está abaixo.

```
   ----------------
   |  |  |  |  |  |
   ----------------
   |  |  |  |  |  |
   ----------------
   |  |  |  |  |  |
   ----------------
   |  |  |  |  |  |
   ----------------
   |  |  |  |  |  |
   ----------------
```
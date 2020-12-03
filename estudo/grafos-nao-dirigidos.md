### Grafos não dirigidos

**o que é um grafo?**

Um grafo é um objeto formado por dois conjuntos: vértices e arestas (vertices e edges). Os vertices são "bolinhas" que normalmente armazenam alguma informação - como números - e as arestas são conexões entre essas bolinhas. Computacionalmente, representamos as arestas como um **par não ordenado** de vértices. Ou seja, usamos um par que identifica quais vertices essa aresta conecta. Note que falamos de um par **não ordenado**. Isto significa que, nesse caso, uma aresta que conecta a com b e uma aresta que conecta b com a é exatamente a mesma coisa.

Grafos que apresentam arestas como pares não ordenados são conhecidos como **grafos não dirigidos**. A ideia de ordenação de vertices na definição de arestas dá naturalmente uma ideia de direção na aresta. É uma aresta que parte de a e termina em b, não apenas conecta mas aponta. Como no nosso caso o grafo não é dirigido, as arestas apenas conectam.

**Mais definições**

Um vértice v é adjacente ao vertice u se o par uv é aresta. Também dizemos que os dois vértices são **vizinhos**.

Dados vértices u e v de um grafo, existe, **no maximo**, uma aresta uv. Nosso grafo não tem arestas paralelas. Nossos grafos também não tem loops, já que as pontas das arestas são distintas.

***Representação computacional**

Um grafo pode ser representado computacionalmente como uma **matriz de adjacências**. Para cada par (u,v ) vale que na matriz de ajacencias M:

* M[u,v] = 1 se uv é aresta
* M[u,v] = 0 do contrario.

Note que M é uma matriz booleana, tem diagonal nula (não temos loops) e é simetrica, ja que nosso grafo não é dirigido.

### Subgrafos

Podemos denotar um grafo com um conjunto V de vértices e A de arestas simplesmente como (V, A). Se chamarmos o grafo de G, dizemos então que seus vertices são definidos por V(G) e suas arestas por A(G).



Um grafo H é subgrafo de G se V(H) $\subseteq$ V(G) e A(H) $\subseteq$ A(G) .

Se V(H) = V(G), dizemos que o subgrafo H é gerador de G.

### Passeios e caminhos

Um passeio é uma **sequencia** de vértices de um grafo.
$$
(v_0, v_1, \dots, v_{k-1}, v_k)
$$
Dizemos que o passeio começa em v0 e termina em vk. Cada aresta da forma $v_iv_{i+1}$ é uma aresta do passeio.

Um **caminho** é um passeio sem repetição de arestas. Um caminho é **simpĺes** se não existe repetição de vértices.

Dizemos que um vértice s está  ao **alcance** de um vertice r se existe pelo menos um caminho que comece em s e termine em r.

### Grafos e componetes conexas

Dizemos que um grafo é conexto se **cada um dos seus vértices esta ao alcance se um dos demais**.

Uma **componente conexa** é um subgrafo conexo **maximal** de G.

### Circuitos

Um circuito é um **caminho fechado**, ou seja, o vértice de início é também o vértice de fim. Um circuito é simples se for um circuito onde apenas o primeiro vertice repete.

Note que, por ser um **caminho**, não podemos repetir arestas, mas podemos repetir vertices.

O que define um circuito é o seu conjunto de vertices e arestas, então o inverso de um circuito é "igual" ao circuito original. Note que a noção de circuito inverso existe apenas em grafos não dirigidos (não há garantia da existencia do circuito contrario num grafo dirigido).

### Florestas e árvores

Uma **floresta** é um grafo sem circuitos. Uma **árvore** é uma floresta **conexa**, ou seja, é um grafo sem circuitos e conexo.



Note que uma árvore **sempre** é uma floresta, já que um grafo conexo pode ser um grafo sem circuitos. Mas nem sempre um grafo sem circuitos naturalmente é convexo. Podemos simplesmente agrupar duas arvores (sem fazer arestas entre elas ) e isso constitui uma floresta, mas não existe aresta entre as duas arvores, então o conjunto não é conexo.



Propriedade de árvore: pra qualquer dois vertices r e s, existe **um único** caminho entre eles (já que naturalmente uma arvore não tem circuitos porque florestas não tem circuitos.)

Uma árvore é **geradora** de um grafo se ela for o subgrafo gerador deste grafo. Ou seja, possui todos os vertices do grafo.

Ou seja, é um grafo conexo, sem circuitos e que possui todos os vertices do outro grafo.

Vamos enunciar agora uma propriedade util para provar a corretude do algoritmod e **kruskal**, que será abordado a seguir.



Tome uma arvore geradora T de um grafo G.  Para qualquer T, vamos denotar T + e como o grafo gerado por adicionar uma aresta "e" qualquer de G. Da mesma maneira, vamos denotar T - t como o grafo gerado quando uma aresta t de T é removida.

**propriedade insere-remove**: Seja T uma árvore geradora de um grafo não dirigido G. Pra qualquer aresta e de G que não esteja em T, o grafo T + e apresenta apenas um circuito. Para qualquer aresta t nesse circuito, vale que T + e - t é uma arvore geradora de G.
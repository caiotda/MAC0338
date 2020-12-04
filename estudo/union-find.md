### Union find

Nessa sessão, vamos estudar como calcular o número de componentes de um grafo. Para tanto, vamos utilizar uma estrutura de dados conhecida como **union-find**. 

Para calcular o número de componentes de um grafo, precisamos descobrir **quando** um vértice pertence a uma componente. Para tanto, é conveniente definir um nome, ou um representante, para cada componente.

Digamos que temos uma coleção de componentes. Para calcular o número de componentes, podemos iterar pelas arestas uv de G e verificar **qual o representante** de cada componente. Se forem representantes diferentes, achamos uma componente. Podemos então **unir** as duas componentes e continuar nossa busca. Se iniciarmos o número de componentes como o número de vértices, a cada iteração podemos diminuir esse número. Ao fim, teriamos o número de componentes do gráfico.



A estrutura de dados abstrata Union find apresenta exatamente essas duas operaçãos:

* **FIND**: dado um vértice v, devolve o representante da coleção de v
* **UNION**: dados representantes r e s de duas coleções distintas, faz a função das coleções e designa r ou s como o representante da coleção resultante.

### Implementações das operações de union e find

Naturalmente, precisamos de alguma implementação computacional para as duas operações de forma que podemos utilizar a ADD.

**Primeira implementação: find rapido, union lento**

Nessa primeira implementaão, armazenamos os representantes num vetor indexado pelos vértices do grafo. Note que isso torna o find O(1):

``` 
FIND-1(v)
1. devolva dir[v]
```

E o union $\Omega(n)$:

```
Union-1 (r, s)  ▷ r ≠ s
1 para cada vértice v
2 	se dir[v] = r
3 		dir[v] := s
```

Naturalmente existe também uma etapa de criação do vetor de diretores/representantes:

``` 
INITIALIZE-1()
1. para cada vertice v
2. 	   dir[v] := v
```

**Segunda implementação: find lento, union rapido**

Ao invés de armazenarmos o representante da componente que o vértice faz parte, vamos adotar a ideia de **superior**: o representante da componente é o seu proprio superior. Pense numa estrutura hierarquica, essa é a ideia dessa implementação.

Os chefes ficam armazenados num vetor de chefes:

```
INITIALIZE-1()
1. para cada vertice v
2. 	   dir[v] := v
```

O find naturalmente torna-se mais lento, já que temos que percorrer toda a hierarquia:

```
Find-2 (v)
1 enquanto chefe[v] ≠ v
2 	v := chefe[v]
3 devolva v
```

O find é tão lento quanto tão grande for a profundidade de um chefe (também chamamos o chefe de **folha**, já que é o único vértice sem chefe). A profundidade é o comprimento do **único caminho** que leva de uma folha e termina em um vertice qualquer v. Aqui caminho se refero a uma sequencia de vértices na forma (u, chefe[u], chefe[chefe[u]], ...);

Como esse caminho pode ser tão grande quanto n-1, o find é lento.

Já o union, fica extremamente rapido:

```
UNION-2(r, s)
1.	chefe[r] := s
```

**Union by rank: ambos rapidos**

Pra evitar o problema de criar uma hierarquia linear (ou seja, a altura do diretor é algo na casa de n), vamos adotar uma heuristica: **ao unir duas categorias, tornar como diretor o diretor da maior componente**.

![](/home/caio/Documentos/BCC/atual/MAC0338/estudo/heuristica.png)

Note como esse grafo é mais balanceado. Ao evitarmos uma estrutura linear, o find fica mais rapido e limitado pela profundidade dessa arvore, que, sabemos é O(lgn)

Para implementar essa heuristica, precisamos ter em mãos a informação de qual a altura de cada nó. Usando a informaçao da altura, podemos definir quem representa a coleção numa eventual união:

```
Union-3 (r, s)  ▷ union-by-rank; r ≠ s
1 se alt[r] > alt[s]
2     chefe[s] := r
3 senão chefe[r] := s
4      se alt[r] = alt[s]
5          alt[s] := alt[s] + 1 
```

No processo de inicialização, devemos também inicializar o vetor de alturas:

```
INITIALIZE-3()
1. para cada vertice v
2. 	   dir[v] := v
3. 	   alt[v] := 0
```

O find fica inalterado. Mas note que ganhamos no desempenho!

Vale que depois de cada execução de union-3, a altura de um vertice v é limitado por:
$$
alt[v] \leq lg \ n(v)
$$
onde n(v) é o número de vertices que pertencem à mesma coleção que v.

Uma consequência natural disso é que a altura de qualquer diretor é no maximo lg n. Naturalmente, isso implica que o FIND é O(lg n) e UNION é O(1)

**Quarta implementação: path compression**.

Nessa nova implementação, sempre que rodarmos o find, vamos **encurtar a distancia** entre qualquer vertice e seu representante. O que isso faz é remover os intermediarios até o chefe:

```
Find-4 (v)  ▷ path-compression
1 se v ≠ chefe[v]
2 	chefe[v] := Find-4 (chefe[v])
3 devolva chefe[v]
```

Mantemos as outras implementações.



O resultado disso é que qualquer implementação do union find passa a ser **O(log\* n)**. Log * é uma função que diz quantas vezes devemos aplicar log num numero para ele ser reduzido a 1. O log * de todas estrelas do universo é algo em torno de 7.

Na pratica? Isso torna o consumo **amortizado** do union find O(1) basicamente.



Falamos que é amortizado porque naturalmente algumas execuções do union e do find vão demorar mais do que isso. Mas sempre que rolar um find, qualquer operação fica muito mais barata. Então no frigir dos ovos, fica mais rapido sim. Essa é a melhor implementação pro union find: **find** com path compression e **union** com rank.
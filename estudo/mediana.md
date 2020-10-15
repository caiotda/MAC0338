# Problema da mediana e do i-ésimo menor elemento

***

### Tabela de conteúdos

1. Introdução
2. Solução ingênua (linearítmica)
3. Solução intermediária: algoritmo da seleção
   2. Análise de desempenho
4. Solução definitiva: algoritmo da seleção aleatoriezado

***

### Introdução

O problema: dado um conjunto de inteiros (isto é, uma coleção de números sem repetições) o **posto** de um elemento é a **quantidade de elementos que é menor que o elemento**:  $\{s \in S : s \leq x\}$. Assim, o elemento de posto 1, por exemplo, possui 1 elemento menor que ele. O elemento de posto 0 possui 0 elementos menor que ele (ou seja, é o menor elemento). Analogamente, o elemento x de posto |S| (ou seja, a cardinalidade - tamanho -  do conjunto) é maior que todos elementos do conjunto.

Assim, podemos definir o **i-ésimo menor elemento** como o elemento de posto i.

A mediana de um conjunto possui posto igual a $\lfloor \frac{|S| + 1}{2}\rfloor$. 

Vamos representar nossos conjuntos como vetores onde os elementos são distintos dois a dois. Com isso, podemos definir dois problemas:

**Problema da mediana**: Dado um vetor A[p..r] com elementos distintos dois a dois, encontrar a mediana de A.

**Problema da mediana generalizada**: Dado um vetor A[p..r] com elementos distintos dois a dois, encontrar o i-ésimo menor elemento de A.]

Note como o problema da mediana é um caso específico do segundo problema.

### Uma solução ingênua

Uma primeira solução - muito simples e intuitiva - seria simplesmente ordenar o vetor e então escolher o iésimo menor elemento: pelo nosso conhecimento em algoritmos de ordenação, a etapa de ordenação seria O(n log n) e a etapa de seleção seria O(1) - se A está ordenado, o i-ésimo menor elemento de A é A[i]. Isso nos dá uma solução de tempo **linearítmico**. Iremos mostrar a seguir uma solução mais elaborada que pode nos devolver o i-ésimo menor elemento em **tempo linear**. Primeiro, mostraremos uma solução um pouco menos poderosa, na qual apenas o melhor caso é linear, e o pior caso é quadrático. Em seguida, melhoraremos essa primeira solução para ela ser **linear no caso médio**.

### O algoritmo da seleção

Uma outra solução além da solução ingênua é o algoritmo da **seleção**: ele funciona a base da rotina de particionamento do quicksort. A idéia central do algoritmo recursivo é selecionar o elemento de posto i do vetor. Isso é feito dividindo o vetor em duas porções,por meio da rotina divide do quicksort. Suponha que o divide retorna um índice "q". Pela natureza do divide, sabemos três coisas:

1. Todos elementos menores que A[q] estão à sua esquerda - logo, todos elementos **com posto menor que q** estão à sua esquerda
2. Todos elementos maiores que A[q] estão à sua direita, logo, todos elementos com **posto maior que q** estão à sua direita.
3. A[q] tem posto q, ou seja, é o q-ésimo menor elemento de A.

Com isso, conseguimos fazer uma busca em A pelo i-ésimo menor elemento. Fazemos isso em três momentos:

Primeiro, dividimos o vetor em duas porções. Então, descobrimos quantos elementos temos em A[p...q], vamos chamar esse valor de K. Se dermos sorte de O vetor da esquerda ter exatamente i elementos, achamos o i-ésimo menor elemento. Do contrário, sabemos aonde procurar: se i < k, temos que olhar o vetor da esquerda e procurar pelo iésimo menor elemento. Do contrario, temos que procurar no vetor da direita pelo i-k-esimo menor eleemnto (subtraimos k porque não vamos considerar os elementos da esquerda). O algoritmo é:

```
selecao(A, p, r, i)
1. se p == r
2. 	devolva A[r]
3. q = divide(A, p, r)
4. k = q - p + 1
5. se k = i
6.  devolva A[k]
7. se i < k
8. 	devolva selecao(A, p, q-1, i)
9. devolva selecao(A,q+1, r, i-k)
```

**Análise de desempenho**:

Assim como fizemos com o quicksort, vamos medir o número de comparações que o divide faz em um array de tamanho n. Sabemos que esse número é n-1.Sabemos que no pior caso, a recorrência do divide pode ser ser descrita como:
$$
T(n) = T(n-1) + n-1
$$
Onde n = r-p+1. É fácil de verificar que essa recorrência é $T(n) = \Theta(n^2)$. Ou seja, o seleciona é quadratico no pior caso, o que é pior que nosso algoritmo de ordenar e pinçar.





No melhor caso, podemos imaginar que o `divide` divide o vetor em exatamente n/2 elementos. Ou seja:
$$
M(n) = M(\lfloor\frac{n-1}{2}\rfloor) + n-1
$$
Podemos resolver uma recorrência similar (supondo n-1 multiplo de 2) e obter que, no melhor caso, M(n) = $\Theta(n)$.

### Solução definitiva: um algoritmo aleatoriezado



Para nos livrarmos desse possível caso ruim quadrático, convém-se aleatoriezar o seleção:

```
selecao-rand(A, p, r, i)
1. se p == r
2. 	devolva A[r]
3. q = divide-rand(A, p, r)
4. k = q - p + 1
5. se k = i
6.  devolva A[k]
7. se i < k
8. 	devolva selecao-rand(A, p, q-1, i)
9. devolva selecao-rand(A,q+1, r, i-k)
```

A única coisa diferente é que usamos um pivô aleatório no divide. O pior caso acontece só quando o pivô selecionado em A[p..r] é o maior elemento do vetor. Espera-se que, ao selecionarmos um pivô qualquer, o pior caso aconteça menos. O tempo esperado de execução acaba sendo $\Omicron(n)$.
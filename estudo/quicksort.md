# Quicksort

Topicos:

* Introdução
* o problema da particionamento
* O quicksort
* Desempenħø do quicksort
  * Melhor caso
  * Pior caso
  * Sobre o tempo de execução vs mergesort

***

Até agora vimos dois algoritmos de ordenação: ordenação por inserção e o mergesort. O insertion sort, apesar de ser muito intuitivo é lento: no caso médio, é quadrático. O mergesort por sua vez é no caso médio linearitmico, mas consome memória extra. Vamos ver agora outro algoritmo de divisão e conquista que também é linearítimico mas é mais rapido e não precisa de memória auxiliar: **o quicksort**.

### O problema do particionamento

Da mesma forma que o mergesort se apoia quase que completamente numa rotina auxiliar (a rotina de merge), o quicksort se apoia quase que completamente na rotina de **particionamento**. Dado um item qualquer de um vetor  A[p..r] - por convenção vamos escolher A[r] - chamado de **pivô**, queremos manipular o vetor A de forma que **todos elementos menores que o pivô sejam posicionados a sua esquerda, e todos elementos maiores sejam posicionados à sua direita**. Em outras palavras, queremos uma permutação de A de forma que :
$$
A[p..j] \leq A[j] < A[j+1..r]
$$
Se todos elementos menores que o pivô ficam a sua esquerda e todos elementos ficam a sua direita, vale que essa rotina **posiciona o pivô na sua posição correta no vetor caso ele fosse ordenado**: por exemplo, se rodarmos um mergesort depois de colocarmos o pivô na sua posição correta, ele estará no mesmo lugar ao fim da ordenação.



Abaixo, um pseudocódigo descrevendo o particionamento de um vetor A[p..r]:

```c
particiona(a, p, r):
1. x:= A[r] // pivo												theta(1)
2. i := p-1														theta(1)
3. para j := p até r - 1:										theta(n)
4. 	se A[j] <= x:												Theta(n)
5.		i := i + 1												O(n)
6.		troque A[i] com A[j]									O(n)
7. troque A[i+1] com A[r] // Garante que o pivô está em i+1		theta(1)
8. Devolva i+1 // Devolve posição do pivô						theta(1)
```

Note como a variável i guarda o elemento mais a direita dos elementos menores que o pivô. A variável j percorre todo o vetor, enquanto que x guarda o pivô.



No loop da linha 3 temos 3 invariantes:

1. A[r] = x
2. i < j
3. A[p..i] <= x < A[i+1..j-1]

Note como isso vale até o final do algoritmo e é útil para mostrar que ele funciona.

É fácil ver que o consumo de tempo do algoritmo é Theta(n). Uma forma interessante de analisar o tempo de execução do algoritmo é olhar o número de comparações na linha 4. Esse número é, no máximo n - 1, o que corrobora nossa visão de que, pelo menos no pior caso, esse algoritmo é linear.

### Quicksort

Como mencionamos acima, o quicksort é um algoritmo de divisão e conquista, assim como o mergesort. No entanto, ao contrário do mergesort, sua fase de conquista é trivial, enquanto que a fase de divisão (particionamento) é complicada - lembrando que no mergesort a divisão é feita pelas chamadas recursivas enquanto que a conquista é feita usando a rotina de merge. Abaixo, o pseudocódigo co quicksort:

```c
quicksort(A, p, r):
1. se p<= r:
2. q := particiona(A, p, r)
3. quicksort(A, p, q-1)
4. quicksort(A, q+1, r)
```

Como vale que p <= q <= r e nunca incluimos q nas chamadas recursivas, enetão nota-se que o tamanho das instâncias diminui.

### Desempenho do quicksort

Sabemos que o desempenho do particiona é Theta n, mas o desempenho das chamadas recursivas do quicksort em si vão depender do tamanho das duas subinstâncias: Faz sentido pensar que se sempre quebrarmos um vetor em duas porções seguindo uma proporção 90% 10% entre os dois subvetores, vai ser muito mais lento do que dividir o vetor na metade (a divisão de trabalho é mais justa). Para tanto, vamos separar a analise em pior caso e melhor caso, e posteriormente analisaremos o caso médio.

### Desempenho no pior caso

Seguindo essa idéia de divisão desbalanceada de trabalho, o pior caso possível é pegar uma instância de tamanho n e quebrar em uma instância de tamanho n-1 e outra vazia: Note que isso ocorre quando o pivô já está na sua posição ideal e o mergesort não cria instâncias de tamanho 1 (se q = r, ele faz uma chamada recursiva para quicksort(a, r+1, r), o que é previnido de ser rodado pelo caso base da recursãõ).

Assim, vamos analisar a recorrência no pior caso: Seja $T_*(n)$ o desempenho no pior caso:
$$
T_*(n) = T_*(n-1) + n-1
$$
Lembrando que $n-1$ é o número de comparações na linha 4 do particiona. Tomamos aqui $T_*(0) = 0$. Vamos desenrolar a recorrência:
$$
T_*(n) = T_*(n-1) + n-1
\\
T_*(n) = T_*(n-2) + n-2 + n-1
\\
T_*(n) = T_*(n-3) + n-3 + n-2 + n-1
\\
\vdots
\\
T_*(n) = 0 + 1 + 2 + ... n-1
\\
T_*(n) = \frac{n(n-1)}{2}
\\
\therefore \\
T_*(n) = \Theta(n^2)
$$
Assim, o quicksort é quadrático no pior caso!

### Análise de melhor caso

Se o pior caso ocorre quando a divisão é injusta, faz sentido pensar que o melhor caso ocorre quando a divisão é justa. Para tanto, vamos analisar o caso no qual o pivô divide o vetor A em dois vetores de mesmo tamanho. Assim, seja $T^*(n)$ o tempo de execução do quicksort no melhor caso:
$$
T^*(n) = T^*(\lceil \frac{1}{2}(n-1)\rceil) +  T^*(\lfloor \frac{1}{2}(n-1)\rfloor) + n - 1
$$
Claramente é bem difícil desenrolar essa recorrência em algo útil, já que n é um natural, não necessariamente multiplo de 2. Para tanto, vamos desenrolar uma recorrência parecida:
$$
S(n)  =2\times S(\frac{n}{2}) + n
$$
Para n = 2^0, 2^1, 2^2, ... 2^k...

Vamos começar a desenrolar a recorrência:
$$
S(n)  =2\times S(\frac{n}{2}) + n
\\
S(n)  =2\times 2\times S(\frac{n}{4}) + n + 2\frac{n}{2}
\\
S(n)  =4\times S(\frac{n}{4}) + n + n
\\
S(n) = 8\times S(\frac{n}{8}) + 3n
\\
\vdots
\\
S(2^k) = 2^k S(\frac{n}{2^k}) + kn
$$
Se tomarmos $k = lg_2(n)$, temos:
$$
S(n) = nS(1) + n lg(n)
\\
S(1) = 1, logo\\
S(n) = n + nlg(n)
\\
\therefore \\
S(n) = \Theta(n lg(n)
$$
Parece que n lg n é um bom chute para T*(n). Vamos provar por indução que isso funciona:

Vamos provar que T*(n) <= n lg(N) para todo n > 1. Para n = 1, é trivial:
$$
T*(1) = 0 <= 1* lg(1)
$$
Agora tome n > 1 e suponha que vale para argumentos de T* menores ou iguais a 1;


$$
T^*(n) = T^*(\lceil \frac{1}{2}(n-1)\rceil) +  T^*(\lfloor \frac{1}{2}(n-1)\rfloor) + n - 1
\\
= T*(\lfloor\frac{n}{2}\rfloor) + T*(\lceil\frac{n}{2}\rceil) + n-1
\\
\leq \lceil\frac{n}{2}\rceil lg(\lceil\frac{n}{2}\rceil) + (\lceil\frac{n}{2}\rceil - 1) * lg(\lceil\frac{n}{2}\rceil - 1)  + n -1
\\
< \frac{n}{2}lg(\frac{n}{2}) + \frac{n}{2}lg(\frac{n}{2}) + n-1
\\
= nlg(\frac{n}{2}) + n - 1
\\
= Nlgn - n + n - 1 < N lg n
$$
É fácil de mostrar que vale o mesmo para Omega, mas não provaremos aqui já que a prova é bem similar.



Assim, fica provado que o quicksort é $\Theta$(n lg(n) no melhor caso.

***

Nesse momento é interessante fazer a reflexão: se o quicksort é quadrático no pior caso, por que usamos ele e não o mergesort. Por três razões:

1. O quicksort não cria memória extra. Imagine se temos que ordenar milhões de itens: para usarmos o mergesort, seria necessário alocar o dobro de memória que no quicksort
2. O melhor caso do quicksort é mais rapido que o melhor caso do mergesort
3. O pior caso do quicksort é raro: só ocorre se o vetor já está ordenado. Se usarmos uma rotina que aleatoriza a escolha do pivô, podemos evitar o pior caso (claro que ainda pode ocorrer, mas a probabilidade é tão baixa que vale o risco)
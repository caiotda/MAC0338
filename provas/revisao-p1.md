## Revisão pré-prova 1 de MAC0338

Conteúdo: 

* Prova por Indução
* Notação assintótica
* Tempo de execução, problemas e instâncias
* Ordenação por inserção
* Recursão
* Resolução de recorrências
* Divisão e conquista
* mergesort
* karatsuba
* quicksort
* Análise aleatoriezada (*)
* Problema do iésimo elemento

***

### Prova por indução

Como provamos por indução? 

Pense na indução como uma sequência de dominós caindo: existe um primeiro dominó que cai, e sempre existe um sucessor. A prova por indução consiste em fazer uma prova para uma base (o primeiro dominó) e, sabendo que vale para um caso base, mostrar que, se um dominó qualquer está caindo, o próximo também vai cair. Em termos mais matemáticos, para fazer uma prova por indução temos que:

1. Provar para um caso base (normalmente n = 0, ou n = 1)
2. Assumir que vale para um caso qualquer (n-1), e provar para o sucessor (n)

Quando usamos uma variável "n" para provar por indução, dizemos que estamos provando por indução em n.

Erros comuns ao se provar por indução:

1. "vamos provar por indução em n, onde n é um número real" ERRADO! Precisamos ter um sucessor claro, e o conjunto dos reais não possui a propriedade dos sucessores bem definida (para quaisqueres dois reais, existem infinitos numeros reais entre eles). O que fazemos normalmente é provar nos naturais.
2. Não especificar o caso base: "Vamos provar por indução em n, onde n é um natural". Isso é capricho do PF, mas ele sempre pede para especificarmos a base no enunciado do problema: "Vamos provar por indução em n, onde n> 1 pertence aos naturais"

Exemplo de prova por indução:

```
Prove o seguinte fato por indução: Para todo número natural não-nulo n tem-se 1² + 2² + 3² + ⋅⋅⋅ + n² ≤ n³.

Queremos provar que 1² + 2² +... n² <= n³; vale para n >= 1, onde n é um natural.

Note que a expressão vale para n = 1: 1² <= 1³.

Agora vamos tomar como hipótese de indução que 1² + 2² +...(n-1)² <= 1³ + 2³ + ... (n-1)³ vale e vamos provar que vale para n > 1


1² + 2² +... (n1)² <= (n1)³; Somando n em ambos lados

1² + 2² +... (n+1)² + n^2= (n+1)³ +n²;

1² + 2² +... n² <= n³ -3n² +3n + n² - 1 <= n³ -3n² +3n +n²; portanto

1² + 2² +... n² <= n³ -2n² +3n-1 <= n³ -n*(2n-3); como n > 1 e n pertence aos naturais não nulos, vale que 2n-3 > 0 para todo n natural maior que 1, logo

1² + 2² +... n² <= n³ -2n² +3n-1 <= n³ -n*(2n-3) <= n³; assim:

1² + 2² +... n² <= n³

Tendo provado a base e o passo da indução, fica provado por indução que a afirmação vale para todo n natural não nulo.

```

Outro:

```
 É verdade que n < 2n? Use indução.



Vamos provar que n < 2^n por indução, para n>=0.

Base da indução:
Para n=0 => 0 < 1.
Para n=1 => 1 < 2^1.
Para n=2 => 2 < 4.

Passo da indução: n > 2.
Hipótese de indução: n-1 < 2^(n-1).
Temos:
2(n-1) < 2(2^(n-1))
2n-2 < 2^n

Como n > 2 => 2n > 2 + n => 2n-2 > n, temos:

n < 2n -2 < 2^n
n < 2^n.


Para n < 0, sabemos que 2^n > 0, então n < 2^n também vale
```



Aqui a solução foi mais direta ao ponto, já indicando qual a base e qual o passo. Dá pra fazer assim também.

***

### Notação assintótica

A análise assintótica se preocupa com a comparação **assintótica** entre funções (ou seja, para n sufienciemente grandes). A notação assintótica é usada para **comparar o crescimento de funções** - o que é diferente de compararmos derivadas, por exemplo. Para tanto, normalmente usamos funções **assintoticamente não negativas** (ou seja, tomamos n grande o bastante para considerarmos apenas valores positios de f e g). Dependendo do resultado da comparação entre duas funções, usamos uma das **3 notações assintóticas**. Usamos:

1. $f = \Omicron(g(n))$ quando assintoticamente f é limitado **superiormente** por g
2. $f = \Omega(g(n))$ quando assintoticamente f é limitado **inferiormente** por g
3. $f = \Theta(g(n))$ quando assintoticamente f é **igual** a g.

Vamos agora passar pela definição formal de cada notação:

**Notação big o**:

Dizemos que f é big o g quando:

"Se existem constantes c e n0 tal que $f(n) \leq c g(n)$ para n > n0, então vale que $f = \Omicron(g(n))$ ". Note que podem existir **inúmeros** pares c, n0. Para provar que f é $\Omicron(g(n))$, basta acharmos um par. Quando dizemos que estamos analisando as funções para n suficientesmente grandes, estamos nos referindo a n > n0.

**Notação omega**

Dizemos que f é omega g quando:

"Se existem constantes c e n0 tal que $f(n) \leq c g(n)$  para n > n0, então vale que $f = \Omega(g(n))$".

**Notação Theta**

Dizemos que f é theta g quando

"Se existem constantes c1, c2 e n0 tal que $c1*g(n) \leq f(n) \leq c2*g(n)$ para n > n0, dizemos que $f = \Theta(g(n))$". Alternativamente, podemos definir a notação theta como:

"Se $f = \Omicron(g(n))$ e $f = \Omega(g(n))$ então $f = \Theta(g(n))$ ".



**Erros comuns**:

* Definir c em função de n. Esses dois números devem ser fixos e independentes um do outro
* Afirmar que para todo n suficientemente grande existe um c. O correto é afirmar que existem c e n0 e, para n suficientemente grande, vale qualquer relação entre f e g.



***

### Tempo de execução, instâncias e problemas

Quando estamos resolvendo um problema computacional, frequentemente lidamos com noções de **melhor caso** e **pior caso**. Associados a esses conceitos, existem algumas frases como "O algoritmo do insertion sort apresenta melhor caso quando o vetor já está ordenado" ou "o quicksort apresenta seu pior caso quando o vetor já está ordenado". Mas o quê isso significa? 
Para cada problema computacional, associamos **instâncias**, que são simplesmente exemplos do problema

* Para o problema da ordenação, o vetor A = [1,2,3,4,5] é uma instância

Algoritmos computacionais recebem instâncias e devolvem possíveis soluções (ou avisam que não existe solução para a dada instância). O algoritmo leva **tempo** até resolver o problema. Esse tempo de execução, geralmente, é associado à notação assintótica. Dizemos que um algoritmo leva  tempo **quadrático** se a sua ordem de crescimento é O(n^2), por exemplo.

O **melhor caso** de um algoritmo é o conjunto de instâncias que geralmente resultam em um menor tempo de execução do algoritmo. O insertion sort apresenta menor tempo de execução (O(n)) se o vetor já estiver ordenado. Então toda instância de A[1...n] onde  A[1] <= A[2] <= ... A[n] apresentará o melhor caso.

Analogamente para o **pior caso**, onde estamos interessados em instâncias nas quais o tempo de execução é maior.



**Nota sobre notação assintótica**: Como a notação O(.) tem cara de "menor igual que", não tem sentido afirmar que um algoritmo é O(.) no **pior caso**, já que isso é reduntante. Ao invés disso, podemos dizer que o algoritmo é $\Theta(.)$ no pior caso. Dizer que uma função é O(.) no **melhor caso** não é redundante.

Similarmente ao caso de $\Omega(.)$. Essa notação tem cara de "maior igual que", então é redundante afirmar que o um algoritmo é $\Omega(.)$ no **melhor caso**. Dizer que um algoritmo é $\Omega(.)$ no **pior caso** não é redundante.

***

### Insertion sort

Algoritmo de ordenação bem ingênuo. 

Idéia central: Iterar um vetor A[1..n] mantendo sempre dois subvetores:

1. A[i..j]: Contendo os itens já ordenados de A
2. A[j...n]: Contendo os itens não ordenados em A

O que fazemos é, para cada elemento em A[j...n], procuramos aonde inseri-lo em A[i...j]. Esse processo é basicamente iterar A[i...j] até encontrar um elemento menor que o escolhido. Nesse momento, insiro em A[i...j].



Algoritmo: 

```
INSERTION-SORT(A)
1. for j = 2 to A.length:								n
2. 	chave = A[j]										n-1
3.	# Insira A[j] na sequencia já ordenada A[1..j-1]
4.	i = j - 1											n-1
5. 	while i > 0 and A[i] > chave:						2 + 3 + ... n-1
6.		A[i+1] = A[i] 									1+2+...n-1	
7.		i = i -1 										1+2+...n-1
8.	A[i+1] = chave 										n-1
```

Melhor caso: A já está ordenado -> nunca entra no laço da linha 5

* Desempenho no melhor caso: $\Theta(n)$.

Pior caso: Vetor inversamente ordenado: sempre entra no laço da linha 5

* Desempenho no pior caso: $\Theta(n^2)$

Essa análise foi feita somando quantas vezes cada linha é executada (no melhor caso, as linhas 6 e 7 não são executadas).

**Invariante**: o vetor A[1..j-1] está ordenado.

Para mostrar a validade do invariante precisamos mostrar que vale a inicialização, a manutenção e a finalização.

### Algoritmos recursivos e recorrências

Um algoritmo é recursivo se ele **reduz o tamanho das suas instancias** e sabe **obter solução de uma instância a partir de subinstâncias**. Para fazer a análise de desempenho de um algoritmo recursivo vamos fazer uso de **recorrências**: 

Uma recorrência é um artifício matemático de definir uma função em cima dela mesma. Tome o algoritmo recursivo de calcular a soma de um vetor:

```
Soma(A, n)
1. se n = 1
2.  devolva A[1]
3. devolva A[n] + soma(A, n-1)
```

Seja T(n) o tempo de execução desse algoritmo para uma instância de tamanho n. Podemos descrever o tempo de execução como
$$
T(n) = T(n-1) + 1
$$
E podemos definir T(1) = 1.

Para **escrevermos** a recorrência, basta olharmos para a cara do algoritmo recursivo e entender:

1. Como o algoritmo quebra uma instância de tamanho n
2. Como o algoritmo combina a solução dessas instâncias.

Para **resolvermos** uma recorrência, precisamos chutar. O passo a passo é:

1. Desenrolamos a recorrência (literalmente vamos abrindo a recorrência até abrir uma fórmula longa e explícita do tempo de execução)
   1. Se for muito difícil de desenrolar a recorrência, podemos desenrolar uma recorrência parecida e torcer pra que, no passo 2 e 3, o resultado seja válido.
2. Chutamos uma fórmula fechada
3. Provamos a validade da fórmula fechada

Exemplo:
$$
T(n) = T(\lfloor\frac{n-1}{2}\rfloor) + T(\lceil\frac{n-1}{2}\rceil) + n
$$
É bem difícil supor uma solução pra isso, já que o tamanho das instâncias - se tomarmos n inteiro - acaba ficando fracionario. Uma solução seria supor n-1 multiplo de 2, dai teriamos:
$$
T'(n) = 2*T'(\frac{n-1}{2}) + n
$$
Agora sim poderíamos desenrolar essa recorrência, chutar uma fórmula fechada e tentar provar que ela vale para T(n).

### Mergesort

* Algoritmo linearitmico para ordenaçã

* Divisão e conquista

* Tempo de execução: theta (nlog n)

* Consome memoria adicional

* Recorrencia:
  $$
  T(n) = T(\lceil \frac{n}{2}\rceil) + T(\lfloor \frac{n}{2}\rfloor) + 6n + 7
  $$

* Estratégia pra resolver a recorrência (e outras recorrências parecidas):
  * Suponha que n é potência de 2 e resolva a recorrência similar. Prove por indução que o resultado obtido serve para resolver T(n)

### Algoritmo de karatsuba

* Algoritmo de divisão e conquista
* Multiplicação de dois numeros
* Ótimo pra numeros enormes
* n^lg3

Idéia: pegar o produto de 2 números u*v, ambos números de n algarismos, e reescrever os dois como:

* u = p*10^m + q, onde m = teto(n/2) e p é a metade mais significativa de u e q é o resto
* v = r*10^m + s. r é a metade mais significativa de v e s é o resto.

Então a multiplicação seria
$$
u*v = (10^m p + q) * (10^m r + s)
$$
Eventualmente chegamos em 
$$
= 10^\frac{n}{2} * (qr+ ps) +10^n*pr + qs
$$
Mas se fizermos
$$
y = (p+q)*(r+s)
\\
\therefore
\\
qr + ps = y - pr - qs
$$


Teríamos
$$
u*v = 10^\frac{n}{2}(y - pr - qs) +qs + 10^n*pr
$$
Assim a gente quebra um problema de tamanho n em 2 de tamanho n/2 e um de tamanho n/2, constituindo divisão e conquista.
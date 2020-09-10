# Aula 03

## Ordenação por inserção

***

Problema: Rearranjar um vetor A[1..n] em ordem crescente.

Toda instância tem solução?

## Insertion sort

Suponha que temos esse vetor:

 ... 11 33 22 -44 55

Suponha que o vetor já está resolvido antes do item "33". O que temos que fazer, nesse momento, seria, por exemplo, inserir o 22 na posição certa, isto é, entre o 11 e o 33:

... 11 22 33 -44 55

Essa é a idéia por trás do **insertion sort**: a cada iteração, inserimos um elemento na sua posição correta:

```
insertion_sort(A, n)
	para j:= 2 até n
	x := A[j]
	i := j - 1
	enquanto i > 0 e A[i] > x
		A[i+1] := A[i]
		i := i + 1
	A[i+1] := x
```

Note que o laço interno simplesmente desloca todos elementos para a direita de modo que encontramos um lugar para incluir o elemento em questão.

### Análise do algoritmo

Análise 1: correção

Invariante: Fato lógico que vale a cada iteração do algoritmo. Mais do que isso, no início de cada iteração.

* No nosso caso, Todo elemento em A com índice i tal que i < j está ordenado.

Prova:

 Trivial quando j = 2.

Suponha que vale no começo de uma iteração genérica. Vamos provar que vale na iteração seguinte. Como inserimos j+1 na posição correta no subvetor [1...j], então segue naturalmente que [1...j+1] está ordenado



Análise 2: desempenho



O tempo de execução depende de n: T(n)

Uma forma simples da análise do algoritmo é somar quantas vezes cada linha é executada:

```
insertion_sort(A, n)
	para j:= 2 até n				n
	x := A[j]						n-1
	i := j - 1						n-1
	enquanto i > 0 e A[i] > x		2+3+...+n
		A[i+1] := A[i]				1+2+...n-1
		i := i + 1					1+2+...n-1
	A[i+1] := x						n-1
```

Note que a linha 1 é executada 1 vez a amis que a linha 2 pois temos uma execução da linha 1 quando j = n, mas quando isso vale, a linha 2 não é executada.



Supondo que cada linha demora uma unidade de tempo para ser executada, se somarmos todos tempos temos:
$$
T(n) = \frac{3}{2}n^2 + \frac{7}{2}n - 4
$$
Uma informação importante é que essas constantes pouco importam e derivam da nossa hipótese de que cada linha demora 1 unidade de tempo.

Podemos concluir facilmente que:
$$
T(n) \in \Theta(n^2)
$$
Uma forma mais grosseira de resolver seria fazer a analise assintotica de cada linha  e somar o resultado:

```
insertion_sort(A, n)
	para j:= 2 até n				Theta(n)
	x := A[j]						Theta n
	i := j - 1						Theta n
	enquanto i > 0 e A[i] > x		Theta n ^2
		A[i+1] := A[i]				Theta n^2
		i := i + 1					Theta n^2
	A[i+1] := x						Theta n
```

Note que estamos pensando no pior caso, então todas execuções são theta. Se analisarmos o caso geral, o laço da linha 5, por exemplo seria O n^2 e não Theta.



Se somarmos os Thetas, teriamos simplesmente $\Theta(n^2)$.
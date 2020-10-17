# Divisão e conquista

***

### O que é?



**Divisão e conquista** é uma técnica de projeto que consiste em:

1. Dividir uma instância de um problema em instâncias menores (fase da **divisão**)
2. Resolver instâncias menores (**conquista**, feita usando recursão)
3. Combinar as soluções menores e obter a solução do problema original

Se tanto a fase de divisão e conquista forem rápidas, o algoritmo é eficiente.

Como os algoritmos de DC usam recursões, para analisarmos seu tempo de execução, vamos usar recorrências.

Alguns famosos problemas que usam DC:

* Busca binária
* Algoritmo de Kuratsaba
* Mergesort
* Quicksort

***

## Mergesort

Para entender como funciona um algoritmo de divisão e conquista e como fazer uma analise de desempenho dessa classe de algoritmos, vamos estudar o mergesort.

### O problema da ordenação

Relembrando o problema da ordenação, que é: Dado um vetor `A[1...N]`, queremos uma **permutação** de A tal que:
$$
A[1] \leq A[2] \leq A[3] \leq ... \leq A[n]
$$
Para estudarmos o mergesort, vamos simplesmente redefinir nosso problema tomado um vetor `A[p...r`], e queremos uma permutação que satisfaça:
$$
A[p] \leq A[p+1] \leq \dots \leq A[r]
$$
O que o mergesort é **dividir** o vetor orignial em porções menores, recursivamente ordenar esses subvetores e **intercalar** esses vetores ja ordenados (fase da conquista). Em código:

```python
MERGESORT(A, p, r):
1.    se p < r:
2.       q := piso((p+r)/2)
3.        MERGESORT(A, p, q)
4.        MERGESORT(A, q+1, r)
5.        INTERCALA(A, p, q, r)        
```

Note a divisão e conquista: quebramos o vetor `A[p...r]` no meio, então ordenamos recursivamente cada metade e cada metade, por sua vez, quebra suas metades e as ordena recursivamente, dai em diante até que p == r, ou seja, o elemento tem 1 elemento apenas e está trivialmente ordenado.

Depois de quebrarmos nosso vetor em pedacinhos de 1 unidade e ordenados, chamaos a função `INTERCALA` que faz o trabalho sujo de tomar dois vetores ordenados `A[p...q]` e `A[q+1...r]` e retorna um terceiro vetor `A[p...r]` que contém todos elementos dos dois vetores e está ordenado.

Note, também, que a terminação do algoritmo está garantida na linha 2: como q < r, necessariamente, o algoritmo irá atingir a base da recursão.



### Intercala

A função intercala recebe um vetor A e tres inteiros, delimitando as duas regiões que ele deve intercalar. É importante ressaltar que o intercala consome **memória adicional** ja que usa um vetor auxiliar para manipular as posições dos itens no vetor A:

```python
INTERCALA(A, p, q, r):
   para i:= p até q
    	B[i] := A[i]
   para j := q+1 até r
   	 	B[r+q+1-j] = := A[j]
   i := p
   j := r
   para k := p até r
    	se B[i] <= B[j]
        	A[k] := B[i]
            i := i + 1
        senão A[k] := B[j]
            j := j - 1
```

Um ponto interessante é essa cópia invertida da segunda metade do vetor: ao assumir que cada metade está ordenada, colocamos o maior elemento no inicio do segundo subvetor. Então mesmo que os dois subvetores ja estejam ordenados entre si, nunca vai ocorrer um caso que  I > j .
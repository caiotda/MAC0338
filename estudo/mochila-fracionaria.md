## Mochila fracionária

Imagine que temos a nossa disposição um conjunto de objetos. Cada objeto possui valores e pesos. Quero colocar colocar itens na minha mochila (que possui uma capacidade máxima) de forma a **maximizar** o valor armazenado. Diferentemente do problema da mochila **Booleana**, agora podemos selecionar **frações** - entre 0 e 1 - de itens.

Esse é o problema da mochila fracionária. Semelhante ao problema da mochila booleana, ele apresenta **solução gulosa**, sendo assim um problema muito mais fácil de entendimento e com um algoritmo mais rapido.

### Formalizações

Temos vetores x[1..n], p[1..n], v[1...n] onde x é a quantidade de cada item que foi selecionado, p é o vetor de cada objeto e v é o vetor do valor de cada objeto. Denotaremos o peso armazenado pelo **produto escalar** x.p. Dizemos que x é racional se todos os seus itens forem numeros naturais. Da mesma maneira, diremos que x é natural se todos os seus itens forem naturais. 

PROBLEMA DA MOCHILA FRACIONÁRIA: Dados vetores **naturais** p[1...n], e v[1...n] e um número natural c, encontrar um vetor **Racional** x[1...n] que maximize x.v sob as condições x.p <= c e 0 <= x[i] <= 1 para todo i.



Diremos que c é a capacidade da instância. Dizemos que X é uma mochila fracionaria se x.p <= c, ou seja, x é candidato a solução.

### Um algoritmo guloso

A **estratégia gulosa** dessa implementação é ordenar nosso objetos em ordem decrescente de  **valor por peso**. Vamos **SEMPRE** escolher os itens enquanto eles couberem na mochila. Quando não couber, pegamos a fração que cabe. Assim, nosso objetos ficam ordenados nessa ordem:
$$
\frac{v_n}{p_n} \geq \frac{v_{n-1}}{p_{n-1}} \geq \dots \frac{v_1}{p_1}
$$
A implementação é :

```
Mochila-Fracionária (p, v, n, c)
1 para j := n decrescendo até 1
2 	se p[j] ≤ c
3 		x[j] := 1
4 		c := c − p[j]
5 	senão x[j] := c / p[j]
6 		c := 0
7 devolva x
```

Note que o algoritmo abocanha o objeto de maior valor específico dentre todos os objetos, e não se arrepende dessa decisão. No momento que um item não cabe na mochila, pega o maximo que couber. Depois disso, a mochila estará cheio. Surpreendentemente, esse algoritmo devolve a mochila de maximo valor.
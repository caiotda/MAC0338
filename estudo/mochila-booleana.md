## Mochila Booleana

Problema: Dada uma quantidade de itens, cada item tem um peso e um valor associado, e uma mochila com uma certa capacidade "c" de kg. Se quero armazenar itens na minha mochila, **qual a combinação de itens que maximiza o valor da minha mochila sem exceder a capacidade dela?**. Chamamos o problema de **booleana** porque quando nos deparamos com um item, temos apenas duas opções: pega-lo, ou não. Posteriormente, vamos estudar o problema da mochila **fracionária**, no qual há a possibilidade de pegar frações de um item.

Formalização: 

* Diremos que 1,2,...,n são **objetos** do problema ("o objeto 1 tem peso x e valor y")

* Fizemos que p[1...n] descreve o peso de cada objeto

* Assim como v[1...n] descreve o valor de cada objeto

* Vamos denotar p(x) como
  $$
  p(x) = \sum_{i \in X} p[i]
  $$
  E vamos denotar v(x) como
  $$
  v(x) = \sum_{i \in X} v[i]
  $$
  Onde x é um conjunto.

* Uma mochila é um conjunto X com capacidade c. Dizemos que a mochila X tem capacidade c se 

$$
 \sum_{i \in X} p[i] \leq c
$$

Agora, vamos enunciar o problema da mochila booleana formalmente:

Dados vetores p[1..n] e v[1..n] naturais (>= 0) e um natural c, queremos encontrar um subconjunto X do intervalo 1...n que **maximize** v(x) sob a restrição p(x) $\leq$ c.

Note que o problema da mochila é um caso geral do problema de subset sum. No subset sum, somavamos pesos para obter exatamente um valor. Aqui, queremos maximizar o valor de um conjunto de numeros mas não ultrapassando a capacidade da mochila.

### Subestrutura ótima

Qualquer solução de uma instancia da mochila booleana é composta por solupes de suas subinstancias.

Suponha que X (uma mochila) é solução da instancia (p, v, n , c). Se n $\notin$ X, então X é solução de (p, v, n-1, c). Agora, se n pertence a X, então X- {n} é solução de (p, v, n-1, c - p[n]). Com isso, temos desenhado uma estrutura recursiva para um algoritmo que resolve o problema da mochila booleana.

### Uma abordagem dinâmica

Se implementarmos a estrutura recursiva acima, chegariamos num algoritmo recursivo muito ineficiente: assim como no problema do subset sum, o problema exploraria todos 2^n subconjuntos, ou seja, uma solução força bruta. 



Para evitar essa ineficiencia, vamos propor uma solução que utiliza **programação dinamica**. Vamos montar uma tabela t onde t[i, j] denota o **valor** de uma solução da instancia (p, v, i, j). 

Para todo i, vale que t[i, 0] = 0. Para todo j, vale que t[0, j] = 0. Com isso, podemos escrever o cerno do algoritmo como:

```
			t[i - 1, j] 							se p[i] > j
t[i, j] = 
			max(t[i-1, j], v[i] + t[i-1, j - p[i]]) do contrario
```

Isso resume o pensamento: se o item cabe na mochila, eu pego (ja que o valor é sempre não negativo). Se não couber, não pego. Aqui vale uma explicação detalhada do uso do operador de maximo. Como tanto t[i-1, j] e t[i-1, j - p[i]] são possiveis soluções da instancia t[i, j] - supondo que p[i] <= j- pode ser que v[i] = 0. Nesse caso, devemos escolher a subinstancia mais vantajosa, de forma que maximizamos o valor de t[i, j].Um algoritmo que resolve o problema em tempo $\Theta(nc)$ é :

```
Mochila-Bool-Prog-Din (p, v, n, c)
1 para i crescendo de 0 até n
2 	t[i, 0] := 1
3 para j crescendo de 1 até c
4 	t[0, j] := 0
5 	para i crescendo de 1 até n
6		 val := t[i − 1, j]
7 		 se p[i] <= j
8 				val := max(val ,v[i] + t[i − 1, j − p[i]])
9 	     t[i, j] := val
10 devolva t[n, c]
```

Note a similaridade com o algoritmo do subset sum (eu inclusive copiei o algoritmo e so mudei algumas linhas. É extremamente similar).
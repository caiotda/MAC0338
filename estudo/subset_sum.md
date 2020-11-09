## Soma de sub conjuntos

Problema: Dado uma sequência de números p =  $\{p_1, p_2, p_3, \dots, p_n\}$ de n elementos e um alvo c, verificar se existe um subconjunto de a "s" tal que:
$$
\sum_{i\in p}i = c
$$
Note que toda instância do problema possui uma solução: ela pode ser 0 (chamaremos isso de "não") ou 1(chamaremos isso de "sim").

Vamos chamar cada valor de p como "pesos"

### Uma estrutura recursiva

O problema possui uma estrutura recursiva (e por consequência uma subestrutura ótima) óbvia. Uma instancia de tamanho n e alvo c só possui solução "sim" se e só se a instancia n-1 e alvo c possui solução (obviamente existe solução, ja que eu poderia só ignorar o n-esimo elemento e teria uma solução).

Além disso, uma instancia de tamanho n e alvo c só possui solução "sim" se a instancia n-1, c-p[n] possuir. Se isso for verdade, então certamente existe um subset que soma c-p[n]. Se eu incluir o n-esimo elemento, eu teria exatamente c - p[n] + p[n] = c e portanto uma solução para a instancia n,c.

Em outras palavras, uma instancia (n, c)  do problema tem solução "sim" se as instancias

(p, n-1, c) e (p, n-1, n-p[n])

Possuirem solução. Com isso, temos uma regra recursiva muito clara de como montarmos um algoritmo recursivo.

### Um algoritmo recursivo

```python
SUBSET-SUM-R(p, n, c)
1. se n = 0
2.	se c = 0
3.		devolva 1 #"Sim"
4.	devolva 0 #"não"
5. b:= SUBSET-SUM-R(P, N-1, C)
6. se b= 0 e p[n] <= c #checagem pra ver se o c resultane é positivo
7.		b:= SUBSET-SUM-R(p, n-1, c-p[n])
8. devolva b
```

Quanto tempo esse algoritmo consome? Denotando por T(n) o consumo no pior caso e se cada instrução consuma 1 unidade de tempo, T(n) satisfaz a recorrência: 
$$
T(n) = 3  + T(n-1) + T(n-1)
$$
Note como separamos os dois T(n-1). Isso acontece porque, mesmo trabalhando com o mesmo n, as duas instancias podem diferir quando ao alvo "c" almejado (devido a linha 7). Então apesar disso ter cheiro de linear, temos um problema ai porque o mesmo subproblema é resolvido muitas vezes. Dado o conjunto que contem todas as combinações possiveis entre pesos e alvos, o nosso algoritmo visita todas essas combinações. Como o numero de subconjuntos de um conjunto de tamanho n é 2^n, e o algoritmo refaz muita conta nesse caminho, esse algoritmo é **Exponencial**. (isso me cheirou meio a migué, mas ok).

### Uma solução dinamica

Uma Alternativa em programação dinâmica é criar uma tabela de valores booleanos onde as linhas são tamanhos de instancias n e as colunas são alvos. Assim, b[i, j] denota a solução da instância de tamanho i e alvo j.

Podemos fazer o uso dessa mesma maxima:



(p, n-1, c) e (p, n-1, n-p[n])



Mas traduzindo em termos de programação dinamica:

``` 
		t[i-1, j], se p[i] > j

t[i,j] = 

		t[i-1, j] OU t[i-1, j - p[i]] se p[i] <= j


```

O algoritmo é o seguinte:

```
Subset-Sum-Prog-Din (p, n, c)
1 para i crescendo de 0 até n
2 	t[i, 0] := 1
3 para j crescendo de 1 até c
4 	t[0, j] := 0
5 	para i crescendo de 1 até n
6		 b := t[i − 1, j]
7 		 se b = 0 e p[i] ≤ j
8 				b := t[i − 1, j − p[i]]
9 	     t[i, j] := b
10 devolva t[n, c]
```

A gente tem que criar uma coluna de indice 0 pra não dar xabu quando fazer t[i-1, j] quando i = 1.



O desempenho claramente é Theta(n * c). Aqui surge uma discussão interessante que vai ser retomada quando começarmos a falar de complexidade, algoritmos polinomiais na entrada e P = NP. Note que se mantivermos o VALOR de c, mas mudarmos seu TAMANHO (por exemplo, c = 1kb e mudar 1000 bytes, é o mesmo VALOR mas o tamanho da entrada é diferente). Uma definição que nos alerta melhor à influencia do tamanho da entrada é dizer que:
$$
\Theta(n * 10^{log c})
$$
O algoritmo é exponencial em relação ao tamanho da entrada mas quadratico em relação ao valor dos inputs.
## Algoritmos guloso

Um algoritmo guloso (ou **Greedy**) é um algoritmo que faz uso de uma estratégia peculiar de modelagem de algoritmos: no algoritmo guloso, partimos de uma solução **pequena** e vamos para instâncias maiores e acabamos resolvendo o problema. Mas como isso se difere de **programação dinâmica**? Bem, um algoritmo guloso faz uma certa escolha a cada passo que traz **benefícios imediatos, mas não necessariamente de longo prazo**. Com isso, não pesamos se a escolha vai trazer beneficios ou maleficios, e também não voltamos atrás da nossa escolha. Naturalmente, existem poucos problemas que admitem esse tipo de escolha com um resultado positivo. Assim, a cada passo, escolhemos a decisão mais **gulosa** e nunca nos arrependemos da escolha. Os problemas que admitem essa **escolha gulosa** podem ser resolvidos por **algoritmos gulosos**. Estes, geralmente são:

* Muito **rápidos**
* Muito **intuitivos**
* Muito **difíceis de serem provados**.

Ao contrário de programação dinâmica, que **explora todas as soluções dentro do espaço de soluções** (claro, de uma maneira eficiente), o algoritmo guloso explora de uma forma muito mais simples, tomando uma escolha gulosa por vez. 

Vamos ver a seguir um exemplo de problema resolvido por um algoritmo guloso

### O problema do pendrive

Digamos que eu tenha um pendrive com capacidade de c megabytes. No meu computador, possuo n arquivos, cada um com tamanho $t_i$ em megabytes. Quero **armazenar o máximo de arquivos no meu pendrive**.

Ex.: Se tenho um pendrive de 1000mb e a seguinte lista de tamanhos de arquivos:

```
files = [10mb, 20mb, 900mb, 30mb, 40mb,100mb, 200mb, 600mb]
```

Existem algumas maneiras de lotar o pendrive, por exemplo tomando um arquivo de 900mb e outro de 100mb. Mas se quisermos colocar o máximo de arquivos possível, podemos pensar em por exemplo tomar 10mb, 20mb, 30mb, 40mb, 100mb, 200mb, 600mb. Totalizando 1000mb.



Uma possível solução: tome todas as permutações de itens cuja soma dá a capacidade do pendrive. Tome a permutação com mais comprimento (Note como aqui navegamos **todo** o espaço de soluções e escolhemos a maior)

Uma solução **gulosa**: Sempre escolha o arquivo de menor tamanho que ainda não foi gravado no pendrive. Parece fazer sentido, é muito mais rápido do que montar todas permutações (note, exploramos apenas uma **parcela** do espaço de soluções) e talvez seja mais difícil de provar. Um algoritmo guloso que resolve esse problema é implementado a seguir:

```
pendrive(t, n, c)
1. i := 1
2. enquanto i <= n e t[i] <= c 
3.  c := c - t[i]
4.  i := i + 1
5. devolva {1...i-1}
```

Nosso algoritmo recebe um vetor de tamanhos (ordenado crescentemente), a quantidade de arquivos e a capacidade do pendrive.

Vamos provar agora que esse algoritmo funciona.

### Prova de corretude do algoritmo do pendrive

Primeiro, vamos fazer uma observação importante sobre as soluções do algoritmo do pendrive: toda solução X do problema é um **segmento inicial** de 1..n, ou seja:

```
				Alguma solução X tem forma {1...k}, k <= n
```

Além disso, vamos tomar outra definição importante: dizemos que um elemento é o **topo** de um conjunto se ele for o maior elemento desse conjunto.

Agora escolha uma solução X com o menor topo possível (lembre-se que o importante para nossa solução é que a soma dos pesos de cada arquivo deve ser menor ou igual à capacidade do pendrive, e deve ser a maior sequencia possivel). Ou seja, de todas soluções possíveis para o problema, vamos tomar aquela que tem o menor topo entre todas soluções. 

Mais do que isso, vamos dizer que esse piso é exatamente k. Vamos mostrar que X = {1....k}.



Prova:

Vamos supor inicialmente que X != {1...k}. Tome $h \in \{1...k\} - X$ . Como k é topo, então vale que $ h \leq k$. Assim, se somarmos os pesos:
$$
\sum_{i \in X}ti - tk + th\leq \sum_{i \in X}ti
$$
Assim, o conjunto $X \cup \{h\} - \{k\}$ cabe no pendrive e tem exatamente o mesmo tamanho que X, ou seja, esse conjunto é uma solução. Mas como h < k, isso contratiz o fato de que X possui o menor topo possível. Assim, por contradição, vale que X = {1..k}



Alternativamente, podemos supor que X != {1...k}. Com isso, temos duas alternativas:

1. X = {1...k...p}, p >= k. Isso contradiz o fato de que X é a maior solução possível.
2. X = {1...h}, h <= k. Isso contradiz o fato de que X possui o menor topo possível.

Com isso, a única saída razoável é tomar X = {1...k}.
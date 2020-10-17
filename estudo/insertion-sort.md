# Ordenação por inserção

***

Nessa seção vamos introduzir, analisar e provar a corretude do algoritmo de ordenação por inserção

### Insertion sort

input: uma sequência de n números ($a_1, a_2, \dots,a_n$).

Output: uma permutação ordenada da sequencia original.

O Insertion sort é um algoritmo eficiente para ordenar uma pequena sequencia de elementos. Para mostrarmos o insertion sort, vamos imaginar que você possui uma sequência de cartas de baralho na sua mão e deseja ordena-las. Você tem a sequência virada para baixo na sua direita e sua mão esquerda vazia. Para cada carta removida do monte, você move para a mão esquerda. Para inserir na posição correta, vamos comparar com cada carta ja inserida na sua mão esquerda. Note que **a todo momento, a sua mão esquerda contém um subconjunto do baralho que está ordenado**.

A idéia do insertion sort é olhar na mão esquerda e:

1. Se a carta sendo olhada é maior que a carta em questão, desloca ela um pouquinho pra direita
2. Se você achar uma carta menor que a carta que voce quer inserir, você achou o lugar correto dela

Então a idéia é ir abrindo espaço na sua mão esquerda para inserir a carta na posição correta. Ao fim dessa operação, sua mão esquerda está ordenada. Falando em codigo:

```python
INSERTION-SORT(A)
1. for j = 2 to A.length:
2. 	chave = A[j]
3.	# Insira A[j] na sequencia já ordenada A[1..j-1]
4.	i = j - 1
5. 	while i > 0 and A[i] > chave:
6.		A[i+1] = A[i] #Abre espaço pra inserção
7.		i = i -1 #olha o elemento anterior
8.	A[i+1] = chave #Ou achei um elemento menor, ou cheguei ao inicio do vetor e chave é o menor elemento do vetor
```

Note como usamos 2 "ponteiros": j, para indicar a carta atual, e i para percorrer todas cartas na minha mão esquerda (Seguindo a analogia do baralho)

Para ajudar a entender por que o algoritmo está correto, vamos demonstrar o **invariante do loop**

### Invariantes

Para mostrar que um invariante vale, devemos mostrar 3 propriedades dele:

1. Inicialização: a propriedade vale antes da primeira iteração do laço
2. Manutenção: Se for verdadeiro antes de uma interação qualquer do loop, ele permanece verdadeiro na próxima interação
3. Terminação: o invariante é valido ao fim da execução do loop

O invariante para a ordenação por inserção é que **a cada iteração, o subvetor A[1...j-1] está ordenado**. Vamos mostrar essas 3 propriedades para demonstrar que o invariante está correto:

1. Trivial. Na primeira iteração (j = 2), A[1...j-1] = A[1]; assim, está trivialmente ordenado
2. Numa iteração j-1 qualquer, vale que A[1...j-1] está ordenado. A idéia do insertion sort é inserir A[j] na posição correta dentro de A[1...j-1]. O algoritmo o faz movendo cada elemento em A[1....j-1] maior que A[j] para a posição sequencial até um ponto que o elemento é A[j] é inserido (suponha que seja inserido numa posição i tal que 1 <= i < j. Nesse momento, vale que A[1....i-1] está ordenado, A[i+1...j] está ordenado. Como A[i] é trivialmente ordenado, o vetor resultante A[1...i....j] está ordenado.
3. Ao fim do loop, vale que j = n + 1. Pelo invariante, vale que o subarray A[1...j-1] está ordenado. Mas A[1...j-1] = A[1...n], logo, o vetor está ordenado. Concluímos, portanto, que o algoritmo está correto.

### Analisando o algoritmo

Para fazermos a anlálise do nosso algoritmo, vamos assumir que a iésima linha do nosso algoritmo toma um tempo $c_i$ constante. Como vamos analisar tudo em notação assintótica, o valor dessa constante é desprezível. Podemos, então, assumir que cada instrução toma um tempo arbitrário 1. Abaixo, vamos mostrar o algoritmo junto de quantas vezes cada linha é executada:



```python
INSERTION-SORT(A)
1. for j = 2 to A.length:								n
2. 	chave = A[j]										n-1
3.	# Insira A[j] na sequencia já ordenada A[1..j-1]
4.	i = j - 1											n-1
5. 	while i > 0 and A[i] > chave:				2 + 3 + ... n-1
6.		A[i+1] = A[i] 							1+2+...n-1	
7.		i = i -1 								1+2+...n-1
8.	A[i+1] = chave 								n-1
```

Note que a linha 5 é executada j vezes por n iterações. Assim, na primeira iteração do loop da linha 1, a linha 5 é executada 2 vezes, então 3 vezes e assim em diante.


Para verificarmos qual a ordem assintótica do algoritmo, podemos simplesmente somar os tempos de execução de cada linha:
$$
T(n) = \frac{3}{2}n^2 + \frac{7}{2}n - 4
$$
É fácil deduzir dai que $T(n) = \Omicron(n^2)$.

### Melhor caso x caso médio x pior caso

É muito comum quando analisarmos um algoritmo discutirmos o tempo de execução no melhor caso, pior caso e caso médio.

O melhor caso, para o insertion sort, é tomar um vetor já ordenado. Nesse caso, ele simplesmente iria percorrer o vetor: nunca entraríamos no laço da linha 5

O pior caso seria um vetor ordenado inversamente, que é essencialmente o que foi mostrado no exemplo ali em cima.

O caso médio exige um pouco mais de cuidado ao analisarmos estatisticamente a esperança de um item estar em certa posição do vetor (veremos isso em **análise probabilística**). Geralmente ele é tão ruim quanto o pior caso.



O insertion sort, no geral, é $\Omicron(n^2)$ e $\Omega(n)$. No pior caso, é $\Theta(n^2)$ enquanto que no melhor caso é $\Theta(n)$. Note a sutileza: Quando estamos no pior ou melhor caso, temos uma notação assintotica mais poderosa para determinar o tempo de execução do algoritmo, já que, no pior caso - por exemplo - o insertion sort tem um tempo de execução limitado superior e inferiormente por uma quadrática.




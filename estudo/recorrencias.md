# Recorrências

***

Quando estamos analisando algoritmos iterativos, é muito simples entender o tempo de execução de um algoritmo porque as **instruções são explícitas**: explicitamos ao computador tudo que ele deve fazer, e simplesmente contamos quantas vezes cada instrução é realizada.



O problema com algoritmos recursivos é que não temos intruções tão explicitas e simplesmente dizemos ao computador como quebrar um problema em subproblemas e como derivar uma solução disso, assim, não funciona mais contar quantas vezes uma linha é executada



Para tanto,  vamos utilizar o artifício das **recorrências**, que nada mais são do que uma expressão que dá o valor de uma função em um dado ponto em função dos pontos anteriores:
$$
f(n) = f(n-1) + 3n +2
$$
Note a similaridade com um algoritmo recursivo. Tome o algoritmo recursivo de calcular uma recursão: é razoável afirmar que o tempo de execução para resolver uma instância de tamanho n é o tempo para resolver uma instância de tamanho n + n (seria o tamanho da multiplicação resultante).



Mas não é nada util dizermos que o tempo de execução de um algoritmo T(n) é "O(t(n-1) + 15)", isso não é informação valiosa! Então oq ue fazemos é **resolver** uma recorrência: processo matemático que consiste de achar uma fórmula fechada que dá o valor direto de uma recorrÊncia em função do seu argumento n.



Para resolver a recorrência vamos fazer duas coisas:

1. Desenrolar a recorrência e ver o que sai. Com isso, vamos tentar encontrar um padrão e com isso encontrar uma fórmula fechada.
2. Definir o valor de F(0)

P.s.: Estamos trabalhando no domínio dos naturais. Então n = 0, 1, 2....

### Exemplo 1

$$
F(n) = F(n-1) + n + 1
$$

1. Desenrolar a recorrência:

2. $$
   F(n) = F(n-1) + n + 1
   \\
   = F(n-2) + n + 2
   \\
   = F(n−3) + (n−2) + (n−1) + n + 3 
   \\
   \vdots\vdots
   = F(0) + 1 + 2 + ... n- 2 + n - 1  + n + n
   $$

Assim, se F(0) = 1, então vale que
$$
F(n) = \frac{n^2 + 3n + 2}{2}
$$
E poderíamos tranquilamente afirmar que o algoritmo descrito por essa recorrência é quadratico.

***

Mas nada garante que essa fórmula está correta né? Basicamente eu fiz um chute de f(0), supus um padrão mas como ter certeza que está correto: Podemos verificar por indução.

Com isso, temos 3 passos na hora de resolver uma recorrência:

1. Abra a recorrência
2. Chute um valor de f(0). Obtenha uma formula para f(n)
3. Verifique se ela está correta

A verificação é feita da seguinte maneira: 

suponha que estamos trabalhando a recorrência:
$$
f(n) = f(n-1) + 3n + 2
$$
E digamos que eu adotei f(1) = 1  e chutei uma aproximação muito boa:
$$
f(n) = \frac{3n^2}{2} + \frac{7}{2}n - 4
$$
O que vamos é verificar por indução que:
$$
f(n) = \frac{3n^2}{2} + \frac{7}{2}n - 4 = f(n-1) + 3n + 2
$$
Pra n = 1 é facil verificar:
$$
f(1) = \frac{3}{2} + \frac{7}{2} - 4 = 1 = f(1)
$$
Vamos dar o passo da indução:
$$
f(n) = f(n-1) + 3n + 2
\\
H.I...
\\
f(n) = \frac{(n-1)^2}{3}n + \frac{7}{2}(n-1) - 4 + 3n + 2
\\
= 	(3n² − 6n + 3 + 7n − 7 − 8 + 6n + 4)/2
\\
= (3n² + 7n − 8)/2
\\ =  	3n²/2 + 7n/2 − 4 , 
$$
Pronto, provamos que nosso chuteé uma fórmula fechada para a recorrência.

### Exemplo 2

Vamos considerar a recorrência
$$
F(n) = F(\frac{n}{2}) + 3
$$
Lembrando que estamos trabalhando no domínio dos naturais. Assim, note que não faz sentido tomarmos n = 3, n = 5... Assim, vamos trabalhar aqui num sub conjunto dos naturais: os naturais multiplos de 2. Assim, $n \in \{2^0, 2 ^1, ...\}$

Então podemos reescrever nossa recorrência como:
$$
f(2^k) = f(2^{k-1}) + 3
$$
Para k  = 1, 2, 3,....

Vamos tomar F(1) = 5, por exemplo. Vamos desenrolar a recorrência:
$$
F(2^k) = F(2^{k-1}) + 3
\\
\ = F(2^{k-2}) + 3*2
\\
\ = F(2^{k-3}) + 3x3
\\
\vdots
\\
= F(2^0) + 3k
\\
= 5 + 3k
$$
Como $ k = lgn$, temos:

$$F(n) = 5 + 3 lg n$$. Note que se tivessemos escolhi outro f(0) o resultado seria outra. Na verdade, para F(0) = i, teríamos:
$$
F(n) = i + 3lg (n)
$$


Assim, poderíamos tranquilamente afirmar que o tempo de execução do algoritmo descrito pela recorrência é O(lgn).

Exercício: mostrar que a recorrência vale por indução.

### Exemplo 3

Seja T uma recorrência e T(0) = 1:
$$
T(n) = 2*T(\lfloor \frac{n}{2} \rfloor) + 7n + 2
$$

# Lista 03

Conteúdo: notação assintótica

***

1) 

```

É verdade. A prova será dividida em três momentos 

de acordo com o valor de n:

a. n <= 0

b. 0 < n < 1

c. n >=1

a) Para n <= 0 é trivial. Vale que 2^n > 0 para todo n 

então n < 2^n vale

b) Vamos provar por absurdo. 
Primeiramente, vamos assumir que a negativa da 

afirmação, ou seja, n >= 2^n vale.

Podemos aplicar o log dos dois lados da inequação e

obter lg n >= n, o que é um absurdo. 

Assim, fica provado por absurdo que  n < 2^n vale
nesse intervalo


c) Vamos provar a afirmação neste intervalo por

indução em k.


Base: k = 1: 

K < 2^ k
1 < 2^1; O que é um fato


Passo da indução:
 Vamos assumir que a afirmação vale para 

k - 1 < 2^{k-1} (hipótese de indução), e  vamos provar 

que a afirmação vale para um k qualquer, onde k > 1



k - 1 < 2^{k-1};

k - 1 + 1 < 2^{k-1} + 1;

Como k > 1, vale que 2^{k-1} > 1, logo:


k < 2^{k - 1} + 1 < 2^{k - 1} + 2^{k - 1}

k < 2* 2^{k - 1}

k < 2^k

Como a afirmação vale para um k qualquer maior que 1,

fica provado por indução que a afirmação vale para todo

n > 1.


Juntando a), b) e c), provamos que a afirmação vale

para todo n real




```





***

2) Fica bem dizer que "f(n) está em Ο(n²) com c = 10 e n0 = 100"? Como reformular isso?

a) não

b) depende de f
c) sim
justifique

```
Não. Tal afirmação implica que c e n0 são únicos,
sendo que na verdade existem inúmeros pares c e n0
que satisfazem a afirmação: 

"f(n) está em O(n^2) se existe c positivo tal que f(n) > c*n^2 
vale para todo n >n0"

Uma forma de reformular a frase seria:

"f(n) está em O(n^2) se existe c positivo tal que
f(n) > c*n^2 vale para todo n >n0.
Particularmente, vale que f(n) > 10*n^2, n > 100"
```

***

3) É verdade que n²/100 = Ο(n)? Justifique. (No editor de texto, use a opção "pré-formatado" e fonte monoespaçada. Você pode digitar "n^2" no lugar de "n²" e "n^{k+1}" no lugar de "nk+1".)

a) não

b) sim

c) depende de c e $n_0$.

Justifique

```
Vamos mostrar que é um absurdo afirmar que existe 
uma constante c > 0 e n > n0 tal que n^2/100 < cn

Primeiramente, podemos reescrever a equação como

n^2/100 - cn < 0;
n* (n/100 - c) < 0;
Mas como as funções são assintoticamente não-negativas
então n > 0, assim:

n/100 - c < 0; Logo

n < 100c;  

Como c é fixo e n é variável, é um absurdo afirmar que
essa desigualdade é verdadeira 
(para qualquer constante c escolhida, irá 
existir um n tal que n >= 100c).

Assim, não vale que n^2/100 = O(n).



```

***

4)É verdade que 10n2 + 200n + 500/n = Ο(n2)? Justifique. (No editor de texto, use a opção "pré-formatado" e fonte monoespaçada. Você pode digitar "n^2" no lugar de "n²" e "n^{k+1}" no lugar de "nk+1".)

a) não

b) depende de c e n0

c) sim

Justifique

```

Ambas funções devem ser assintoticamente não negativas

, então vamos tomar n > 501. Assim, temos:


10n^2 + 200n + 500/n < 10n^2 + 200n;

Como n > 501, temos que

10n^2 + 200n + 500/n < 10n^2 + 200n < 10n^2 + 200n^2;

Ou seja

10n^2 + 200n + 500/n < 210n^2

Como existe c tal que 

10n^2 + 200n + 500/c < c*n^2 vale para todo n > n0,

 então segue que 10n2 + 200n + 500/n = Ο(n2)



```



5) É verdade que 2^{n+1} = Ο(2^n)? Justifique. (No editor de texto, use formato TEXT. Digite "2^n" no lugar de "2n" e "n^{k+1}" no lugar de "nk+1".)

a) depende de n

b) não

c) sim

Justsifique



```

É um fato que 2^{n+1} < 2^{n+2}; Particularmente,
isso é verdadeiro com n > 0. Logo:
2^{n+1} < 2^2*2^n;
2^{n+1} < 4*2^n

Assim, existe c tal que 2^{n+1} < c*2^n para todo n>n_0,
consequentemente, vale que 2^{n+1} = O(2^n)
```





6) É verdade que ⌈lg n⌉ = Ο(lg n)? Justifique (você pode digitar "teto(x)" no lugar de "⌈x⌉").

a) depende de n

b) sim

c) não

Justifique



```

 Vamos assumir que a afirmação do enunciado é 

verdadeira e provar por  absurdo que ela não vale.


Pela definição da função teto e pela afirmação do 
enunciado, podemos afirmar que:

lg n <= teto(lg n) < c* lg n,

para algum c > 0 e n suficientemente grande.

Logo, podemos escrever:

lg n < c * lg n [1]

lg n ( 1 - c) < 0; M

as como lg n > 0 para todo n, então vale que c < 1.


Mas se [1] vale, não há n que satisfaça [1] se 
0 < c < 1.

Assim, fica provado por absurdo que a afirmação

não vale.



```



***

7) É verdade que 2n² − 20 n − 50 = Ω(2n). Justifique.

a) não

b) sim

c) depende de c e n_0



Sim.



Tome n > 1. Assim, podemos afirmar que

2n² − 20 n − 50 > 2n² > 2n

Assim, como existe c positivo tal que 2n² − 20 n − 50 >> c*2n vale para todo n > n0, então segue que 2n² − 20 n − 50 = Ω(2n)

***

8)"Dizemos que f está em Ο(g) se para todo n suficientemente grande existe c positivo tal que f(n) ≤ c g(n)." Justifique.

a) verdadeiro

b) falso

Falso.

```
O erro é afirmar que para todo n grande existe c: 
isso pode abrir brecha para a interpretação de que 
para todo n existe um c diferente, quando 
na verdade o c é único para todo n > n0.

O mais correto seria dizer 
que "Se existe c positivo tal que f(n) < c g(n) 
para n suficientemente grande, então f(n) = O(g(n))".

Note como nessa definição fixamos c para todo n.


```


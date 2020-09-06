# Lista 03

Conteúdo: notação assintótica

***

1) É verdade que $n < 2^n$?Use indução. Justifique

É verdade. A prova será dividida em três momentos:

a. n <= 0

b. 0 < n < 1

c. n >=1

a) Para n <= 0 é trivial. Vale que 2^n > 0 para todo n então n < 2^n vale
b) Vamos provar por absurdo. Primeiramente, vamos assumir que a negativa da afirmação, ou seja, n >= 2^n vale. Podemos aplicar o log dos dois lados e obter lg n >= n, o que é um absurdo. Assim, fica provado por absurdo que  n < 2^n nesse intervalo
c) Vamos provar esse trecho por indução em k. 
Base: k = 1: K < 2^ k -> 1 < 2^1; O que é um fato

Passo: Vamos assumir que a afirmação vale para k - 1 < 2^{k-1}, onde k > 1.

Somando 1 aos dois lados da desigualdade:

k < 2^{k - 1} + 1

Como k > 1, vale que 2^{k-1} >= 1, logo

k < 2^{k - 1} + 1 < 2^{k - 1} + 2^{k - 1}

k < 2^{k - 1}*2

k < 2^k

***

2) Fica bem dizer que "f(n) está em Ο(n²) com c = 10 e n0 = 100"? Como reformular isso?

a) não

b) depende de f
c) sim
justifique

***

3) É verdade que n²/100 = Ο(n)? Justifique. (No editor de texto, use a opção "pré-formatado" e fonte monoespaçada. Você pode digitar "n^2" no lugar de "n²" e "n^{k+1}" no lugar de "nk+1".)

a) não

b) sim

c) depende de c e $n_0$.

Justifique



Não.

Vamos mostrar que é um absurdo afirmar que existe uma constante c > 0 e n > n0 tal que n^2/100 < cn

Ambas funções devem ser assintoticamente não negativas, então devemos tomar n > 0, logo, podemos reescrever a equação como

n^2/100 - cn < 0
n* (n/100 - c) < 0; mas n > 0, então vale que

n/100 - c < 0; Logo

n < 100c;  Como c é fixo e n é variável, é um absurdo afirmar que essa desigualdade é verdadeira (para qualquer constante c escolhida, irá existir um n tal que n >= 100c).



Assim, não vale que n^2/100 = O(n).

***

4)É verdade que 10n2 + 200n + 500/n = Ο(n2)? Justifique. (No editor de texto, use a opção "pré-formatado" e fonte monoespaçada. Você pode digitar "n^2" no lugar de "n²" e "n^{k+1}" no lugar de "nk+1".)

a) não

b) depende de c e n0

c) sim

Justifique



Sim. Ambas funções devem ser assintoticamente não negativas, então vamos tomar n > 0.

Tomando n0 = 501, temos:

10n^2 + 200n + 500/n < 10n^2 + 200n; Como n > n0, portanto, n > 501, temos que

10n^2 + 200n + 500/n < 10n^2 + 200n < 10n^2 + 200n^2; Ou seja

10n^2 + 200n + 500/n < 210n^2

Assim, a afirmação vale para n0 = 501 e c = 210.

***

5) É verdade que 2n+1 = Ο(2n)? Justifique. (No editor de texto, use formato TEXT. Digite "2^n" no lugar de "2n" e "n^{k+1}" no lugar de "nk+1".)

a) depende de n

b) não

c) sim

Justsifique

Sim. Tomando n0 = 1/2, temos:
2n + 1 < 2n + 2n; portanto

2n + 1 < 2* 2n



Assim, 2n+1 está em O(2n) com n0 = 1/2 e c = 2.

***

6) É verdade que ⌈lg n⌉ = Ο(lg n)? Justifique (você pode digitar "teto(x)" no lugar de "⌈x⌉").

a) depende de n

b) sim

c) não

Justifique



Nao. Vamos assumir que a afirmação do enunciado é verdadeira e provar por absurdo que ela não vale.Pela definiçao de teto e pela afirmação do enunciado, podemos afirmar que:

lg n <= teto(lg n) <= c* lg n, para algum c > 0 e n suficientemente grande. Logo, podemos escrever

lg n <= c * lg n (1)

lg n ( 1 - c) <= 0; Mas como lg n > 0 para todo n, então vale que

c <= 1.

Mas se (1) vale, não há n que satisfaça (1) se 0 < c <= 1.

Assim, fica provado por absurdo que a afirmação não vale.

***

7) É verdade que 2n² − 20 n − 50 = Ω(2n). Justifique.

a) não

b) sim

c) depende de c e n_0

***

8)"Dizemos que f está em Ο(g) se para todo n suficientemente grande existe c positivo tal que f(n) ≤ c g(n)." Justifique.

a) verdadeiro

b) falso
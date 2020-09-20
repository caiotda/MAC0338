# Lista 06

***

1) Considere a recorrência 
$$
F(n) = 2F(\frac{n}{2}) + n
$$
Com n = 2^1, 2^2, ....; Dê uma fórmula fechada para a recorrência, com F(1) = 0. Prove por indução que sua solução está correta

F(n) = F(2^k)

F(2^k) = 2*F(2^{k-1}) + 2^k

F(2^k) = 2* [	2*F(2^{k-2}) + 2^{k-1}	]   + 2^k

F(2^k) = 2^2 * F(2^{k-2})  + 2*2^k

F(2^k) = 2* [	2^2*F(2^{k-3}) + 2^{k-2}	]   + 2 * 2^k

F(2^k) = 2^3 * F(2^{k-3})  + 3*2^k

...

F(2^k) = 2^k * F(1) + k * 2^k; F(1) = 0, logo

F(2^k) = k*2^k; Tomando 2^k = n, temos

F(n) = n* lg(n);



Agora vamos provar a validade do nosso "chute" por indução em k. Queremos provar por indução que n * lg(n) = F(n), ou, 2^k * k  = F(2^k).

Base: k = 0

2^0 * 0 = 0
F(2^0) = F(1) = 0

Assim, vale para a base

Passo: assumir que vale para k-1

F(2^k) = 2*F(2^{k-1}) + 2^k; 

Aplicando a hipótese de indução:

F(2^k) = 2 * 2^{k-1}*(k-1) + 2^k

F(2^k) = 2^ k * (k-1 + 1)

F(2^k) = 2^k * k



Está confirmado, por indução, a validade do chute.



***

2) Considere a recorrência  T(n) = 2 T(⌊n/2⌋) + 7n + 2 para n natural positivo. Adote T(1) = 1. Prove que T(n) ≤  8n lg n para todo n ≥ 5.

 Parte 2: Tente usar a mesma técnica para provar que T(n) ≤  7n lg n para todo n ≥ 100, supondo (base da indução) que a desigualdade vale para n = 100, 101, … , 199. 

**Parte 1:**

Vamos provar por indução que a desigualdade T(n) <= 8 n lg (n) vale.

Base:

T(2) = 2*T(1) + 7 + 2 = 11 <= 8 *2 * lg(2) = 16
T(3) = 2* T(1) + 21 + 2 = 25 < = 24* lg(3); lg(3) > 1, então a desigualdade vale.

T(4) = 2* T(2) + 7 * 4 + 2 = 62 <= 8 * 4 * 2 = 64


Vamos tomar como hipótese de indução que a desigualdade acima vale para piso(n/2). Isto é, T(piso(n/2)) <= 8*(n/2) * log(n/2). Logo:

T(n) = 2* T(piso (n/2)) + 7n + 2

T(n) <= 2 *  8*(n/2) * log(n/2) + 7n + 2

T(n) <=  8*n *( log(n) - 1) + 7n + 2

T(n) <= 8nlogn - 8n + 7n + 2

T(n) <= 8nlogn - n + 2

Como n >= 5, temos

T(n) <= 8 * n log(n)



**Parte 2:**

Supondo que a hipótese vale no intervalo de naturais [100,199], podemos tomar como hipótese que T(piso (n/2) ) <= 7 * (n/2) * lg(n/2). Logo:

T(n) = 2* T(piso (n/2)) + 7n + 2

T(n) <= 2 *  7*(n/2) * log(n/2) + 7n + 2

T(n) <=  7*n *( log(n) - 1) + 7n + 2

T(n) <= 7nlogn +  2



Portanto, não vale que T(N) <= 7 * n * log(n)

***



3) Mostre que o consumo de tempo do Mergesort está em Ω(n lg n). (É claro que você deve mostrar isso a partir da recorrência que dá  o consumo de tempo do algoritmo.)



Vamos provar por indução que T(n) >= 1*nlg n. Vamos tomar T(1) = 1.

Base: Tome n =2 e n = 3:

T(2) = T(1) + T(1) + 6*2 + 7 = 21 >= 1 * 1 * 1 = 1 * n * lg (n)

T(3) = T(piso(3/2)) + T(teto(3/2)) + 3 * 6 + 2

T(3) = T(1) + T(2) + 3 * 6 + 2

T(3) = 1 + 21 + 18 + 2 = 42 >= 1 * 3 * 2 >=1 * 3 *  lg (3) = 1 * n lg (n)

Passo:

Vamos tomar como hipotese de indução que a desigualdade vale para T(teto(n/2)) e T(piso(n/2)). Assim:

T(n) = piso(n/2) + teto(n/2) + 6n + 7

T(n) >= 1 * piso (n/2) * lg(piso(n/2)) + 1 * teto(n/2) * lg( teto(n/2) ) + 6n + 7 

,>= 1*lg(piso(n/2)) * [  piso(n/2) + teto(n/2) ] + 6n + 7  

,>= 1*lg(piso(n/2)) * piso(n) + 6n + 7  

,>= 1*lg(piso(n/2)) * (n-1) + 6n + 7 ; Como piso(n/2) >= n/4 para n>= 3, temos:

,>= 1*lg(n/4) * (n-1)+ 6n + 7  

= (lg(n) - 2) * (n-1)+ 6n + 7  

= n*lg(n) - lg(n) -2n + 2 + 6n + 7

= n*lg(n) - lg(n) + 4n + 9

, >= n* lg(n)

Assim, como existe c tal que T(n) >= c * n lg(n) para n >= 1, está provado que T(n) é Omega(n lg (n))

Prova auxiliar [*] :

 Vamos provar que piso(n/2) >= n/4. Como n é inteiro, temos dois casos: n par, ou n ímpar:
 se n for par:

 n/2 >= n/4; Verdadeiro para todo n > 0
 se n for ímpar
 piso(n/2) = (n-1)/2, logo

 (n-1)/2 >= n/4

 n-1 >= n/2; Verdadeiro para n>= 2
# Lista 07

***

1) 

Escreva um algoritmo recursivo que multiplique um número natural u por um número natural v com no máximo n dígitos cada. O algoritmo deve ser baseado na fórmula  u × v = p × r × 10^n + (p × s + q × r) × 10^{n/2} + q × s . Você pode supor que n é potência de 2.

Parte 2: Escreva a recorrência que dá o consumo de tempo do algoritmo.

```
algoritmo(u, v, n)
1. se n <= 1
2. 		devolva u * v
3. m := n/2
4. p := piso(u/10^m)
5. q := u * mod10^m
6. r := piso(v/10^m)
7. s := v * mod10^m
8. pr := algoritmo(p, r, m)
9. qs := algoritmo (q, s, m)
10.ps := algoritmo(p, s, m)
11.pq := algoritmo(p, q, m)
11. uv := pr * 10^2m + 10^m * (ps + qr) + qs
12.devolva uv
```

Vamos denotar o tempo de execução de uma instância de tamanho n como T(n). É razoável supor que as linhas 1-7 consomem em torno de n unidades de tempo. as linhas 7-11 cada consomem T(n/2) unidades de tempo. Assim:

T(n) = 4*T(n/2) + n

***

2) Calcule T(4), … , T(8) a partir da  recorrência T(n) =  2 T(⌈n/2⌉) +  T(⌈n/2⌉ +1) + n supondo T(2) = 2 e T(3) = 3.

T(4) = 2*T(2) + T(3) + 4

T(4) = 2*2 + 3 + 4
T(4) = 11



T(5) = 2*T(3) + T(4) + 5

T(5) = 2*3 + 11 + 5

T(5) = 22



T(6) = 2*T(3) + T(4) + 6

T(6) = 2*3 + 11 + 6

T(6) = 23



T(7) = 2*T(4) + T(5) + 7

T(7)  = 2* 11 + 22 + 7

T(7) = 44 + 7

T(7) = 51



T(8) = 2 * T(4) + T(5) + 8

T(8) = 2*11 + 22 + 8

T(8) = 52 

***

3)

Suponha que o algoritmo de Karatsuba leva 1 minuto para multiplicar dois números de n dígitos cada. Quanto tempo levará para multiplicar dois números de 10n dígitos cada?

Parte 2: Faça uma estimativa análoga para o algoritmo de  multiplicação usual.



Seja T(n) o tempo de execução em minutos do algoritmo de Karatsuba para uma entrada de tamanho n. Sabemos que, assintoticamente, T(n) possui a mesma taxa de crescimento que n^lg3. Assim:



T(n) = 1 minuto = n^lg3

T(10*n) = (10 * n )^lg 3 = 10^lg3 * n ^lg 3 = 10 ^lg 3 * T(n)

Portanto

T(10 * n) = 10 ^lg 3 * 1 minuto (aproximadamente 38 minutos)

Portanto, se aumentarmos o número de digitos dos dois números por um fator de 10, o algoritmo de Karatsuba demora 38 minutos para calcular o produto.

Agora seja G(n) o tempo de execução em minutos do algoritmo usual de multiplicação de dois inteiros. Sabemos que, assintoticamente, G(n) possui a mesma taxa de crescimento que n^2. Assim:

G(n) = 1 minuto = n^2
T(10*n) = (10 * n) ^2 = 100 * n^2 = 100 * G(n) = 100 * 1 minuto
T(10*n) = 100 minutos



Portanto, se aumentarmos o número de digitos dos dois números por um fator de 10, o algoritmo usual de multiplicação demora 100 minutos para calcular o produto.

***

4) Seja S a função definida assim: S(1) = 1 e S(n) = 3 S(n/2) + n  para n = 2, 4, 8, 16, … ,  2i, … Prove, por indução em n, que S(n) = 3 nlg 3 − 2n.

Parte 2: Prove  que S(n) = Ο(nlg 3).

Parte 3: Prove  que S(n) = Ω(nlg 3).



Vamos provar que S(n) = 3 * n ^lg3 - 2n por indução em n. Primeiro, vamos provar que vale para a base ( n = 2)



S(2) = 3 * S(1) + 2 = 3 * 1 + 2 = 5 = 9 - 4 = 3 * 3^lg(2) - 4 = 3 * 2^lg3 - 2*2.

O que prova para a base.



Agora vamos provar para n>=4, tomando como hipótese de indução que S(n/2) = 3*(n/2) ^lg 3 - 2 * (n/2). Partindo da hipótese de indução, temos:



S(n/2) = 3*(n/2) ^lg 3 - 2 * (n/2)

S(n/2) = 3 *( n^lg3/ 2 ^lg 3) - n

S(n/2) = 3 *( n^lg3/ 3 ^lg 2) - n

S(n/2) = 3 * n^lg3/ 3  - n

S(n/2) = n^lg3  - n;

Multiplicando os dois lados da equação por 3:

3* S(n/2) = 3 * n^lg3  -3 * n;

Agora somando n aos dois lados da equação:

3* S(n/2) + n = 3 * n^lg3  -2 * n; 

Mas T(n) = 3* S(n/2) + n , logo

T(n) =  3 * n^lg3  -2 * n;


Está provado por indução que T(n) =  3 * n^lg3  -2 * n;

Agora vamos provar que T(n) = O(n^lg3)

T(n) =  3 * n^lg3  -2 * n;

Note que, para n>=2, vale que

T(n) =  3 * n^lg3  -2 * n; <= 3 * n^lg3

Assim, como existe c tal que T(n) <= c*n^lg3 vale para todo n > n0, então segue que T(n) = O(n^lg3).



Agora vamos provar que T(n) = Omega(n^lg3)

T(n) =  3 * n^lg3  -2 * n;

Note que para n >= 2 vale que

T(n) =  3 * n^lg3  -2 * n >= T(n) =  3 * n^lg3  -2*n^lg3

T(n) >= 1* n^lg3



Portanto, como existe c tal que T(n) >= c*n^lg3 vale para todo n > n0, então segue que T(n) = Omega(n^lg3).
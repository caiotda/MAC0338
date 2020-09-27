# Lista 07

***

1) 

Escreva um algoritmo recursivo que multiplique um número natural u por um número natural v com no máximo n dígitos cada. O algoritmo deve ser baseado na fórmula  u × v = p × r × 10^n + (p × s + q × r) × 10^{n/2} + q × s . Você pode supor que n é potência de 2.

Parte 2: Escreva a recorrência que dá o consumo de tempo do algoritmo.

***

2) Calcule T(4), … , T(8) a partir da  recorrência T(n) =  2 T(⌈n/2⌉) +  T(⌈n/2⌉ +1) + n supondo T(2) = 2 e T(3) = 3.



***

3)

Suponha que o algoritmo de Karatsuba leva 1 minuto para multiplicar dois números de n dígitos cada. Quanto tempo levará para multiplicar dois números de 10n dígitos cada?

Parte 2: Faça uma estimativa análoga para o algoritmo de  multiplicação usual.

***

4) Seja S a função definida assim: S(1) = 1 e S(n) = 3 S(n/2) + n  para n = 2, 4, 8, 16, … ,  2i, … Prove, por indução em n, que S(n) = 3 nlg 3 − 2n.

Parte 2: Prove  que S(n) = Ο(nlg 3).

Parte 3: Prove  que S(n) = Ω(nlg 3).
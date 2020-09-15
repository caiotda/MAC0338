# Lista 05

***

1) Para todo número natural positivo n, o número $11^n-6$ é divisível por 5. Prove essa afirmação por indução matemática.

Base: n = 1

11^1 - 6 = 5; 5 é divisível por 5

Passo da indução. Vamos assumir que vale para n-1 e provar para n

Por hipótese de indução, vale que 11^{n-1} - 6 é divisível por 5. Assim, vale que 
11^{n-1} - 6 + 10*(11^{n-1} - 6) é divisível por 5, já que 10 é divisível por 5. Portanto, teríamos:

11^{n} - 66, ou
11^{n} - 66 + 60, mas 60 é divisível por 5. Então se 
11^{n} - 66 é divisível por 5, consequentemente

11^{n} - 6 é divisível por 5.

Está provado por indução que a expressão é divisível por 5 para todo natural positivo n.

***

2) Escreve um algoritmo recursivo que receba um número natural positivo n e devolva o quociente de 11^n - 6 por 5.

```
devolve-quociente(n)
1.    devolva calcula-funcao(n)/5

calcula-funcao(n)
1. se n = 1
2.    devolva 5
3. senão devolva 11*calcula-função(n-1) + 60
```


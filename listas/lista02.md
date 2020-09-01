# Lista 02, análise de algoritmos



1) Qual das afirmações está mais correta?

a) O candidato será eleito se obtiver metade dos votos válidos mais um

b) O candidato estará eleito se obtiver mais da metade dos votos válidos



2) É verdade que, para todo inteiro positivo n, ⌈lg n⌉ é o menor inteiro k tal que n ≤ $2^k$ ? Justifique (você pode digitar "2^k" no lugar de "2k" e "teto(x)" no lugar de "⌈x⌉").



r.: 



n <= 2^k; aplicando lg nos dois lados da inequação:

lg(n) <= k; O menor inteiro positivo k que satisfaz a inequação, pela definição de teto, é teto(lg(n))





3) É verdade que 
$$
\lfloor lg(n) \rfloor \geq lg(n-1)
$$
?

R.: Falso. Tome n = 4:

piso(lg(4)) >= lg(3) -> 2 >= lg(3), portanto, 2^2 >= 3, o que é falso.



6) Quanto vale k no fim do procedimento?

```
k := 0
para i := 1 até n
  para j:= i até n
    k := k + 1
```



O número de execuções da linha 4 (n_exec) na i-ésima iteração da linha 2 é n+1 - i . Assim, podemos n_exec como:

n_exec = soma de i = 1 até n do termo n+1 - 1

portanto

n_exec = n + (n-1) + (n-2) + ... 1;



O que é uma soma de uma progressão aritmética de n termos. Assim, podemos calcular n_exec como:

n_exec = n*(a_1 + a_n) / 2

Onde a_1 = n - primeiro termo da sequência - e a_n = 1 - n-ésimo termo da sequência.

n_exec = n*(n + 1)/2
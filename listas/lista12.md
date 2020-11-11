### Lista 12

1. O algoritmo SUBSET-SUM-PROG-DIN preenche a tabela t por colunas (a primeira coluna, depois a segunda, etc.). Escreva uma variante do algoritmo que preencha a tabela por linhas.

   ```
   
   Subset-Sum-Prog-Din (p, n, c)
   1 para j crescendo de 0 até c
   2   t[0, j] := 0
   3. t[0, 0] = 1
   4 para i crescendo de 1 até n
   5   t[i, 0] := 1
   6   para j crescendo de 1 até c
   7     b := t[i − 1, j]
   8     se b = 0 e p[i] ≤ j
   9       b := t[i − 1, j − p[i]]
   10     t[i, j] := b
   11 devolva t[n, c] 
   ```

   

***

2. Seja t[0 .. n, 0 .. c] a tabela construída por SUBSET-SUM-PROG-DIN. Escreva um algoritmo que use t para calcular um conjunto X tal que  p(X) = c. O seu algoritmo deve devolver o vetor característico de X ou nada se tal X não existe.

```
recupera-conjunto(p, t, n ,c)
1. se t[n, c] == 1
2.   j := c
3.   X = {}
4.   enquanto j >= 0
5.     encontrou := 0
6.     i := 0
7.     enquanto i <= n e encontrou = 0
8.       se t[i, j] = 1
9.         X := X U {i}
10.        j :=j - p[i]
11.        encontrou := 1
12.		 i := i + 1
13.     se encontrou = 0
14.       j := j - 1
15.  devolva X
```


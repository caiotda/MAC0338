### Lista 10



2) Calcula uma SSC máxima de (32, 19, 32, 17, 31, 43, 30, 29, 54, 16, 28, 52, 15, 41, 65, 14, 50).

32, 43, 51, 65
19, 32, 43, 54, 65

17, 31, 43, 54, 65

31, 43, 54, 65
16, 28, 52, 65





3) O que há de errado com o código:

```
 MaxDC (A, p, r)
    1  se p = r
    2      devolve A[p]
    3  q := ⌈(p+r)/2⌉
    4  x := MaxDC (A, p, q)
    5  y := MaxDC (A, q+1, r)
    6  se x > y
    7      devolva x
    8  devolva y

```

O problema é que o algoritmo não diminui o tamanho das instâncias corretamente, como é esperado de um algoritmo de divisão e conquista. Tome A = [1, 2], p = 1 e r = 2. Com isso, q = 2. Portanto, q = r, logo, o subproblema gerado na linha 4 tem o mesmo tamanho que a instância geradora. Resulta em um loop.
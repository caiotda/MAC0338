## Lista 11



2) Escreva uma variante do algoritmo  SCD-Max-Gula supondo que os intervalos são dados em order crescente *de inícios*.  
 Parte 2: Enuncie a versão apropriada da  propriedade da escolha gulosa. 
 Parte 3: Enuncie a versão apropriada da  propriedade da subestrutura ótima.


Parte 1:

``` 
SCD-Max(A, B, p, r)
1.  X := {r}
2.  k := r
3.  para m := r - 1 até p
4.      se B[m] <= A[k]  
5.          X := X u {m}
6.          k := m 
7.  devolva X

```

Parte 2: Todo intervalo de início máximo pertence a alguma SCD máxima

Parte 3: Seja m um intervalo de início máximo e X uma SCD máxima. Vale que se m pertence a X, então X - {m} é uma SCD máxima de todos os intervalos anteriores a m.
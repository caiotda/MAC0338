## Problema dos intervalos disjuntos

O problema dos intervalos disjuntos foca em **encaixar o máximo número de intervalos disjuntos em sequência**. Vamos tomar dois intervalos: i e j. Vamos denotar o início de um intervalo k por a[k] e o seu fim por b[k]. Dois intervalos são disjuntos se b[i] $\leq$ a[j]. Podemos ler isso como **o intervalo i termina antes do intervalo j começar**.

Por exemplo, um admnistrador de centro de convenções com um conjunto de eventos quer encaixar **o máximo de eventos em sequência e cada evento deve ser disjunto um do outro**.

### Formalizações e definições

Vamos tomar dois vetores a[p...r] e b[p..r] denominando inicios e fins de intervalos. Obviamente queremos eventos que terminam depois que começam, então vale para todo p <= i <= r que a[i] <= b[i]. Chamamos a e b de **coleção de intervalos**.

Além disso, vamos dizer que {p, p+1, ... r} é uma **coleção de intervalos**.

Vamos dizer que um intervalo i é **anterior** a um intervalo k se b[i] < a[k]. Um intervalo i é **sucessor** a um intervalo k se a[k] < b[i]. 

Dois intervalos são **disjuntos** se um é anterior ao outro.

Uma **coleção de intervalos** {p...r} é **disjunta** se **todos seus intervalos são disjuntos dois a dois**.

Uma subcoleção disjunta X é **máxima** se não existe subcoleção Y tal que |Y| > |X|.

Por fim, podemos definir o problema da **subcoleção disjunta maxima (SCD máxima):

**SCD Máxima: encontrar uma subcoleção disjunta máxima de uma coleção de intervalos a[p..r], b[p...r]**.



### Um algoritmo guloso

Esse problema admite um algoritmo guloso como solução. Esse algortimo toma a seguinte **escolha gulosa**: sempre escolha um intervalo de término mínimo e remova todos intervalos que não são posteriores ao intervalo escolhido.

Com isso é óbvio que o algoritmo produz uma SCD (isso vêm como consequencia natural de só escolhermos intervalos posteriores ao intervalo com término mínimo). O que nos resta provar é se essa SCD é máxima.

Para provar esse fato, precisamos provar duas propriedades gulosas do algoritmo:

1. A propriedade da escolha gulosa: Todo intervalo de término mínimo pertence a alguma SCD máxima

   PROVA: Seja m um intervalo mínimo de alguma SCD e seja X uma SCD maxima. Se m pertence a X, acabou. Vamos supor então que $m \notin X$ se seja q um intervalo mínimo em X. Como m pertence a alguam SCD e tem término mínimo, observe que m é **anterior** a q. Como m é anterior a q, note que m é anterior a todo intervalo em X. Assim, $X - q \cup m $ é uma SCD. Ademais, tem exatamente o mesmo tamanho original que X, então é uma SCD máxima. Observe que essa coleção apresenta m. Então está provado que todo intervalo de término mínimo pertence a **alguma** SCD máxima.

   

2. Propriedade da subestrutura ótima: Seja m um intervalo de término mínimo e X uma SCD máxima. Vale que se m $\in$ X, então X - {m} é uma SCD máxima de todos intervalos posteriores a m.

   PROVA:

   Tome Y uma SCD máxima qualquer para a coleção de intervalos posteriores a m. Sabemos que X é SCD máxima, então vale que | Y | <= | X |. Mais do que isso,  temos que | Y + {m} | <= |X|, logo, | Y | <= |X - {m}|

   O que prova que qualquer SCD sucessora de m é menor que X - {m}. Logo, X - {m} é a SCD maxima nessa coleção de intervalos.

Assim, está provado tanto a escolha gulosa quanto a propriedade da subestrutura ótima. Dessa forma, fica provado que nossa escolha gulosa vale e, além disso, se resolvermos um subproblema podemos usar essa solução para problemas maiores.

A seguir, uma implementação para o problema dos intervalos disjuntos:

```python
SCD-Max(A, B, p, r)
1. X := {p}
2. k := p
3. para m := p + 1 até r
4. 		se A[m] > B[k]  
5.      	X := X u {m}
6.			k := m 
7. devolva X
```

Na linha 4, encontramos um intervalo k que possui término mínimo. Assim, na linha 5 adicionamos o intervalo m na solução por ser o primeiro sucessor a k. Atualizamos k na linha 6 e rodamos a linha 3 até encontrar o proximo sucessor disjunto de k.



Note como o algoritmo - **se excluirmos o tempo de processamento para ordenar A e B** - é linear.


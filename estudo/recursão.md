# Recursão

***

A idéia de um algoritmo recursivo se resume a simplesment:

1. Ensinar ao computador como reduzir a instância do problema
2. Como obter uma solução a partir da subinstância

Assim, o computador faz o resto. Para tanto, algoritmos recursivos devem resolver problemas com **natureza recursiva**, isto é, problemas nos quais soluções de instâncias de tamanho n são compostas por soluções de instancias menores

Ex.: O problema de somar n inteiros. Podemos pensar isso como o problema de somar 1 único inteiro ao problema de somar n-1 inteiros. Assim, podemos quebrar nosso problema em varios casos extremamente simples: somar 2 inteiros.

Sempre ao desenhar um algoritmo recursivo, devemos ter em mente o **caso base da recursão**: iremos quebrar nosso problema em subproblemas, mas até que ponto? Isso precisa ser explicito ao programa.

Abaixo, um programa recursivo de soma dos números de um vetor:

```
SOMA(n, a)
1. se n = 0
2.	s:=0
3. senão s:= SOMA(n-1, A) + A[n]
4. devolva s
```

Note que o caso base é quando chegamos a n = 0. Nesse momento a recursão atinge seu fim e vai voltando para chamadas superiores.



### Recursão de cauda

Recursão padrão possui um problema bem grande: o que nós fazemos é ir divididno um problema até chegarmos ao caso base. Nesse processo, acumulamos diversas chamadas em aberto na pilha de execução. Ao chegar no caso base, subimos  apilha resolvendo contas que ficaram para trás. Esse "sobe e desce" é um problema e pode causar estouro de pilha se a chamada for muito grande. Tome o problema do fatorial:

```
fatorial(n)
1. se n = 0
2.	devolva 1
3. se não devolva n * fatorial *n(n-1)
```

Note como deixamos o trabalho sujo pro final, e inicialmente só nos preocupamos em chegar ao caso base. Uma alternativa mais eficiente (e que muitos compiladores suportam em baixo nível) é utilizar a **recursão de cauda**: ela possui esse nome porque fazemos o trabalho sujo primeiro, e deixamos a recursão por último:

```  
fatorial(n)
1. devolva fatorial-aux(n, 1)

fatorial-aux(n, acc)
1. se n = 0
2.	devolva acc
3. se não devolva fatorial-aux(n, acc*n)
```

**IMPORTANTE**: pra isso ser realmente eficiente, os parametros da função devem ser estritamente avaliados, isto é, não vale usar linguagem com avaliação preguiçosa de parametros. Devemos primeiro avaliar os parametros da função antes de fazer a chamada recursiva, do contrario não faz sentido.
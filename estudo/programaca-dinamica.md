## Programação dinâmica

**O que é**: Programação dinâmica é uma técnica de desenho de algoritmos na qual aplicamos **armazenamento de soluções de subproblemas** de problemas de natureza recursiva numa **tabela**. Dessa forma, conseguimos agilizar a resolução do problema e evitar retrabalho.

**pré requisito para uma solução com programação dinâmica**: O problema necessita ter **subestrutura ótima**, ou seja, possuir estrutura recursiva. Importante: normalmente algoritmos em PD são escritos **iterativamente**, e não recursivamente. Usamos a propriedade de subproblemas para calcular a solução de um problema baseado em outros subproblemas, cujas soluções estão armazenadas em uma tabela.

Tempo de execução: Geralmente, um algoritmo de programação dinamica tem seu tempo de execução limitado pelo tamanho da tabela.

### Exemplo: fibonacci

Um exmplo clássico é da sequência de fibonnaci. Um algoritmo ingênuo de fibonacci recursivo é:

```
fib(n)
1. se n = 0
2.   devolva 0
3. se n = 1 
4.   devolva 1
5. devolva fib(n-1) + fib(n-2)
```

Se explorarmos rapidamente a arvore de recursão para resolver fib(5), vemos uma explosão de cálculos:

```
fib(5)----------fib(4)--------fib(3)-------fib(2)....
|				|				|
|				|				|
fib(3)			fib(2)			fib(1)
```

Acima exploramos a resolução de fib(n-1) na horizontal e fin(n-2) na vertical. Note que só nesse exemplo rapido, fib(3) é resolvido duas vezes, fib(2) será resolvido umas 4 vezes. Inclusive, o desempenho dessa implementação é péssimo: estamos falando de $\Theta(1.5^n)$. O problema de fibonacci tem estrutura recursiva então é ótimo para ser reimplementado em programação dinamica.

### Fibonacci em pd

Para implementarmos fibonacci em programação dinamica precisamos de duas coisas:

1. Reinterpretar a recorrência fazendo uso de uma tabela
2. Criar uma tabela pertinente

A recorrencia de fibonnaci é:
$$
fib(n) = fib(n-1) + fib(n-2)
$$
Vamos então criar uma tabela f preenchida de 1's inicialmente, assim, faremos:

```
fib-pd(n, f)
1. f[0] = 0
2. f[1] = 1
3. para i = 2 até n, faça:
4.  f[i] = f[i-1] + f[i-2]
5. devolva f[n]
```

Assim, a gente não recalcula nada e ainda armazena valores úteis para o futuro. Mesmo tendo um tradeoff de tempo de execução com expaço em memória, acaba valendo a pena porque esse novo algoritmo é linear.


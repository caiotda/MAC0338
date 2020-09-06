# Notação assintótica

Ao analisar o desempenho de um algoritmo, é útil pensar como ele varia de acordo com o tamanho da entrada: se dobrarmos a entrada (n), quanto cresce o tempo de execução (podemos chamar isso de f(n))?

Assim, seria muito legal se conseguissemos dizer que nossa função f(n) cresce de maneira similar a uma função arbitrária g(n), por exemplo, g(N) = n². Se podermos falar isso, poderiamos afirmar que quando dobramos a entrada n, f(n) quadriplica.

Para conseguirmos fazer essas afirmações, analisamos nossas funções f(n) e g(n) para ns grandes. Isso é o conceito de **assintótico**. 

Em termos gerais, o tópico de notação assintótica está preocupado em estudar o **crescimento** de funções. Isso é feito por meio por meio de **comparações** entre funções. Uma função, assintoticamente, pode ser maior, menor ou igual que outra. 

Para as comparações fazerem sentido, vamos convencionar que estamos selecionando um n grande o bastante tal que as duas funções são positivas (f(n), g(n)) >= 0 para um n suficientemente grande). Chamamos essas funções de  **assintoticamente não-negativas**.

Para cada um desses casos de comparação, há um conceito assintotico relacionado: 

O estudo assintótico traz três conceitos poderosíssimos para a análise de algortimos:

* Notação $\Omicron$
* Notação $\Omega$
* Notação $\Theta$ 

## Ordem $\Omicron$

Em termos gerais, utilizamos a notação $\Omicron$ para determinar que uma função $$f$$ é **limitada superiormente** por outra função $$g$$. Quando isso acontece, dizemos que "f é $\Omicron$ de g" (f é óh de g ). Alternativamente, dizemos que **f pertence a ordem O de g**. Claro, estamos analisando em termos assintoticos então tal definição vale para n muito grande. Em termos um pouco mais matematicos, podemos dizer quem uma função f é  $\Omicron$ de g se:
$$
\exists c, n_0 \in \mathbb{R}, c > 0,  n_0 > n, \forall n : f(n) \leq c.g(n) \implies f(n) \in \Omicron (g(n))
$$
Em português: se estamos analisando nossas funções assintoticamente e existe um positivo c tal que vaçe f(n) <= c g(n), então f é O(g(n)) 



Graficamente, se f é big o g, então toda função na ordem $\Omicron$ g é limitado **superiormente** por g;

### Notação

Para dizer que f é $\Omicron$ de g podemos falar:

1. $f(n) = \Omicron(g(n))$
2. $f(n) \in \Omicron(g(n))$

Vamos focar no uso 1.

## Ordem $\Omega$

Se a ordem $\Omicron$ é util para dizer quando uma função f, em analise assintotca, é menor que outra função g, a ordem $\Omega$ serve exatamente para o contrario: afirmar que uma função f é **maior** que a função g, para n suficientemente grande.

A definição é muito parecida com a ordem $\Omicron$, só mudamos a comparação:
$$
\exists c, n_0 \in \mathbb{R}, c > 0,  n_0 > n, \forall n : f(n) \geq c.g(n) \implies f(n) =\Omega(n))
$$
Ou seja, para um c positivo e n suficientemente frande, se $f(n) \geq cg(n)$, então $f(n) = \Omega g(n)$. De novo, tomando f e g assintoticamente não negativos.

Graficamente, se f é omega g, então toda função na ordegm omega g é limitado **inferiormente** por g;

## Ordem $\Theta$

Além de termos conceitos que abrangem as ideias de que uma função é menor do que outra ou maior, também temos o conceito de $Ordem \Theta$, que, em termos informais, afimra que **f = g** assintoticamente. A definição:
$$
f(n) = \Theta(g(n)) \iff f(n) = \Omicron g(n) \and f(n) = \Omega(g(n))
$$
Isso quer dizer que existem positivos c e d tal que:
$$
c g(n) \leq f(n) \leq d g (n)
$$
Pensando graficamente, pode-se afirmar que se f é Theta g, então assintoticamente as duas funções crescem de forma identica. A ordem theta é a afirmação mais poderosa sobre crescimento de funções dentro das tres ordens acima.


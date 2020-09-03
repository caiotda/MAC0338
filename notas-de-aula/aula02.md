# Aula 02

## Comparação assintótica de funções

***

Assintótico: para um n grande.

Nosso objetivo aqui é comparar duas funções f(n) e g(n) para um n grande e eventualmente responder perguntas como 
$$
f(n) \leq g(n) ?
$$
Onde cada função f e g são funções que representam o consumo de tempo de 2 algoritmos baseado em sua entrada de tamanho n.

Isso vem com um problema:

1. Quanto vale n?

   Para um dado n, podemos ter f(n) > g(n). Para outros, f(n) < g(n);

   Fazendo a anpálise **assintótica**, podemos analisar para valores grandes de n a partir de um $n_0$ inicial

A primeira comparação que vamos fazer é se a f é **menor** que g:

### Notação big O

A comparação é feita da seguinte maneira:

Existe c tal que f(N) <= c g(n) para todo n suficientemente grande (ou seja, maior que um $n_0$)

Se isso for atendido, podemos dizer que $f(n) =  \Omicron(g(n))$

Ou, dizemos que f está na classe de funções $\Omicron  (g(n))$.

Exemplos:
$$
2n² + 30n + 400 = \Omicron(N^2)
$$
Verdadeiro. Note que:
$$
Para \ n \geq  \ 1 \ temos: \\
2N^2 + 30 N + 400 \leq 2N^2 + 30N^2 + 400N^2
\\ \therefore
\\
2N^2 + 30N + 400 \leq 432N^2
$$
Logo, para c = 432 e $n_0$ = 1, vale a afirmação.

Exemplo:

Prove que $\lceil\frac{n}{2} \rceil + 10 \in \Omicron(n)$

Para todo $n \geq 1$ temos
$$
\lceil\frac{n}{2} \rceil + 10  \leq \frac{n}{2} + 1 + 10
\\
\lceil\frac{n}{2} \rceil + 10  \leq \frac{n}{2} + 11
\\
\lceil\frac{n}{2} \rceil + 10  \leq n + 11n
\\
\lceil\frac{n}{2} \rceil + 10  \leq 12n
$$
Assim, vale para $n_0 = 1$ e $c = 12$.

Ou, para n >= 22
$$
\lceil\frac{n}{2} \rceil + 10  \leq \frac{n}{2} + 1 + 10
\\
\lceil\frac{n}{2} \rceil + 10  \leq \frac{n}{2} + 11
\\
\lceil\frac{n}{2} \rceil + 10  \leq \frac{n}{2} + \frac{n}{2}
\\
\lceil\frac{n}{2} \rceil + 10  \leq 1n
$$

***

### Notação Omega

Alternativamente, podemos analisar assintoticamente:
$$
f(n) <= c g(n), n >= n_0 \and c \in R
$$
Se isso é atingido, dizemos que
$$
f(n) \in \Omega (g(n))
$$

***

### Notação theta

Existe uma ordem de grandeza qie combina as duas notações:

Se f é $\Omicron(g(n))$ e f é $\Omega(g(n))$, dizemos que f é $\theta(g(n))$. 

Ser theta de uma função significa dizer que, assintoticamente, as duas funções são iguais (tomando um n muito grande, as duas funções asão iguais):
$$
c_1 * g(n) \leq f(n) \leq c_2 * g(n)
$$
Note como f(n) é sanduichado pelas duas funções. Assintoticamente, elas se aproximam e tornam-se indistinguiveis.
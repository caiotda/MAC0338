# Algoritmo de Karatsuba

***

### Introdução

Problema: Multiplicar dois números inteiros de, no máximo, n dígitos. O algoritmo intuitivo é quadráticco (aquele que a gente aprendeu na escola).

Mas como os números que multiplicamos no dia a dia tem, normalmente, uns 2,3, ou 4 digitos, o algoritmo acaba sendo bem rápido se implementarmos no computador (seriam umas 16 multiplicações, onde cada multiplicação demora um tempo minúsculo). No entanto, quando lidamos com problemas combinatórios de números grandes, como em criptografia, faz sentido começar a pensar em algoritmos mais eficientes para multiplicação de números inteiros. Vamos estudar o algoritmo de karatsuba, que é $\Theta(n^{lg(3)})$. O que é ligeiramente melhor que quadrático.

### Intuição matemática

Vamos tomar dois números de no máximo `n` digitos, seja `n` um número par. Assim, podemos dizer que um número `u` é composto por dois números:

* Os seus $\frac{n}{2}$ primeiros algarismos significativos. Vamos chamar esse número de `p`.
* Os seus outros $\frac{n}{2}$ algarismos menos significativos. Chamaremos de `q`.

Assim, qualquer número u de n algarismos pode ser escrito como:
$$
u = p * 10^\frac{n}{2} + q
$$
E a idéia do karatsuba gira toda em torno disso: podemos separar um número com muitos algarismos em dois números com menos algarismos. Disso vai surgir um algoritmo de **divisão e conquista** que faz uso dessa manipulação para acelerar a multiplicação de dois inteiros.

Analogamente, podemos definir outro inteiro v como:
$$
v = r * 10^\frac{n}{2} + s
$$
Assim, tome $u*v$ como:
$$
u*v = (p*10^\frac{n}{2} + q) * (r*10^\frac{n}{2} + s)
\\
= 10^\frac{n}{2} * (qr+ ps) +10^n*pr + qs
$$
Então conseguimos quebrar u*v em quatro subproblemas:

1. q*r
2. p*s
3. p*r
4. q*s

Podemos ir além: conseguimos reduzir uma multiplicação em 3 multiplicações: Se tomarmos
$$
y = (p+q)*(r+s)
$$
Podemos reescrever um dos termos da multiplicação como:
$$
qr + ps = y - pr - qs
$$
Ou seja:
$$
u*v = 10^\frac{n}{2}(y - pr - qs) +qs + 10^n*pr
$$
Pronto, agora temos só 3 multiplicações pra fazer. Então, como algoritmo de divisão e conquista temos duas fases:

1. Quebrar nossa divisão u*v em 3 subproblemas: y, qr e ps (**divisão**)
2. Somar os resultados seguindo a fórmula acima (**conquista**).

Para cobrir casos que n não é par, basta tomar o **teto** de n (isso basicamente equivale a colocar um 0 na frente do número). Assim, se $m = \lceil \frac{n}{2} \rceil$ podemos reescrever a expressão como:]
$$
u*v = 10^m(y - pr - qs) +qs + 10^{2m}*pr
$$

### O algoritmo

Com isso tudo em mente, podemos montar o algoritmo de karatsub: um algoritmo que recebe dois números, seus números de digitos e recursivamente calcula o produto. Ou seja: 

```python
karatsuba(u, v, n)
1. se n <= 3
2. 		devolva u * v
3. m := teto(n/2)
4. p := piso(u/10^m)
5. q := u * mod10^m
6. r := piso(v/10^m)
7. s := u * mod10^m
8. pr := karatsuba(p, r, m)
9. qs := karatsuba (q, s, m)
10.y := karatsuba(p+q, r+s, m+1)
11. uv := pr * 10^2m + 10^m * (y - pr - qs) + qs
12.devolva uv
```

Na linha 4 e 6 estou pegando os m digitos mais significativos. Nas linhas 5 e 7, os menos significativos. Note que ao calcular y teriamos um numero de m+1 digitos.



O caso base da recursão é 3 porque queremos que os subproblemas sejam menores que os problemas originais. Assim, o subproblema da linha 10 só vale se n >3, já que
$$
\lceil\frac{n}{2} +1\rceil < n \iff n> 3
$$

### Análise do algoritmo de karatsuba



É razoável afirmar que o algoritmo não depende dos números envolvidos, e sim da quantidade de algarismos (já que supomos que toda multiplicaçõa suficientemente pequena é computacionalmente identica). Uma recorrência razoável é 
$$
T(n) = 2*T(\lceil\frac{n}{2} \rceil) + T(\lceil\frac{n}{2} \rceil + 1) + n
$$
Onde n é um natural. O termo $2*T(\lceil\frac{n}{2} \rceil)$ vem das linhas 8 e 9 e o termo $T(\lceil\frac{n}{2} \rceil + 1)$ vem da linha 10. O n é uma aproximação assintotica de todas as outras operações do algoritmo. 

Para estudar essa recorrência, vamos estudar outra muito similar cujo resultado assintotico vale para T(n):


$$
S(n) = 3S(\frac{n}{2}) + n
\\
= 3 * (3*S(\frac{n}{2^2} + \frac{n}{2})) + n
\\
 = 3^2 * S(\frac{n}{2^2}) + \frac{3n}{2} + \frac{3^0n}{2^0} 
 \\
 \vdots
 \\
 = 3^i * S(\frac{n}{2^i}) + \frac{3^{i-1}n}{2^{i-1}} + .... \frac{3^0n}{2^0}
$$
Se tomarmos $i = lg(n)$, teremos $S(\frac{n}{2^i})$ = S(1) = 1, logo:
$$
S(n) = \frac{3^in}{2^i} + ... \frac{3n}{2} + n
\\
= n*(\frac{3^{i}}{2^{i}} + \frac{3^{i-1}}{2^{i-1}} + \dots + \frac{3^{0}}{2^{0}})
\\
= n * \frac{\frac{3}{2}^{i+1} -1 }{\frac{3^{}}{2^{}} - 1}
\\
= 2n*[\frac{3}{2}^{i+1} - 1]; n = 2^i
\\
= 2^{i+1}*[(\frac{3}{2})^{i+1} - 1]
\\
= 3^{i+1} - 2^{i+1}
\\
= 3*3^i - 2*2^i; 2^i = n; i = lg_2(n)
\\
= 3*3^{lg_2(n)} -2*2^{lg_2(n)}
\\
= 3*n^{lg3} -2n
$$
No fim ali eu usei a propriedade do log:
$$
a^{log_b(c)} = c^{log_b(a)}
$$
Assim, fica facil notar que o algoritmo é $\Theta(n^{lg(3)})$. Note que assintoticamente, $n^{lg3} < n^2$, ent"ao karatsuba realmente é mais rapido assintoticamente. No entando, o que a notação theta esconde é o valor da constante c e n_0 a partir dos quais isso é verdade, e são valores bem altos. Assim, para multiplicações cotidianas, o algoritmo ensino médio é mais rápido.
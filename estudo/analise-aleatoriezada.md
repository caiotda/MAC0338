# Análise aleatoriezada de algoritmos

***

Objetivo: estudar o caso **médio** de um algoritmo.

Até agora, nos preocupamos com o pior e melhor caso de um algoritmo: mas como podemos determinar quanto tempo um algoritmo demora em média? Até agora estavamos supondo que caso médio = pior caso, o que, em muitos algoritmo, é verdade. Mas agora vamos aprender a mostrar essa equivalência e conseguir mostrar o caso médio para qualquer algoritmo.



### Estudo de caso: o problema da contratação

Suponha que você é o chefe de uma empresa e quer contratar um assistente. Para tanto, você preparar n candidatos para serem entrevistados ao longo de n semanas (ou seja, 1 entrevista por semana). Além disso, você é um chefe ansioso: sempre que você encontrar um assistente melhor que o atual, você contrata o candidato (naturalmente, o primeiro candidato sempre recebe o emprego porque inicialmente você não tem assistente). Ao fim das n semanas, **quantas contratações você fez?** Se o primeiro candidato for o melhor de todos, então você faz só uma contratação. Se os candidatos estiverem ordenados em ordem de competência, você fará n contratações. **Mas quantas contratações são feitas, na média?**

Suponha que registramos os n candidatos num vetor tal que A[i] = competência do iésimo candidato. Assim, podemos algoritmizar essa busca como:

``` 
max(A, n)
1. max := 0
2. para i := 1 até n
3. 	 se A[i] > max
4.	 max := A[i] //contratação
5. devolva max
```

Quantas vezes a linha 4 é chamada?  Note que esse número independe dos valores de A, e sim da relação entre os itens de A. Portanto, podemos simplesmente alterar A para que ele represente uma **permutação** da sequência 1..n;

### Resolvendo com probabilidades

Para resolver com probabilidades, vamos supor que todas as permutações de A são **independentes e igualmente distribuídas**: ou seja, a ocorrência de uma permutaçõa não impacta a probabilidade de outras permutações ocorrerem; além disso, todas as permutações tem a mesma chance de ocorrer.

Quando falamos do número **esperado** de alguma coisa acontecer, normalmente falamos da **esperança**. Assim, vamos calcular a esperança da **variavel aleatoria** (variavel cujo resultado depende de fatores aleatórios) `x`, que dá a quantidade de vezes que a linha 4 é executada:
$$
\mathbb{E}(x) = \sum_{k=1}^n k * \mathbb{P}r(x = k)
$$
Onde k é a quantidade de vezes que a linha 4 é executada: essencialmente o que fazemos é multiplicar o valor pela sua probabilidade. Note que, conforme k cresce, esperamos que Pr(x = k) caia.

Para facilitar o entendimento, vamos usar **variáveis indicadoras**, ou seja, uma variavel que vale 1 se o fenômeno ocorre. Então seja $X_k$ uma variável indicadora para o k-ésimo elemento tal que:

* $X_k = 1$ se a linha 4 é executada quando i = k (ou seja, nosso k-ésimo elemento é o máximo)
* $X_k = 0$ do contrário.

Naturalmente, se a variável vale 1 ou 0, podemos dizer que a esperança pode ser calculada, para variáveis indicadoras:
$$
E(x) = \sum_{i=k}^nPr(x_k)
$$
Mas como estamos lidando com permutações igualmente distribuídas, a probabilidade do k-ésimo elemento no vetor A[1..k] ser o máximo é exatamente $\frac{1}{k}$

Logo:
$$
E(x) = \frac{1}{1} + \frac{1}{2} + \frac{1}{3} + \dots +\frac{1}{n}
$$
O que é uma **série harmônica**. Vale que a esperança é limitada por $ln(n) < E(x) < ln(x) + 1$. Logo, o número esperado de execuções da linha é $\Theta(ln(n))$.
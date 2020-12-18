### Complexidade de problemas

Até agora, quando analisavamos a complexidade de alguma coisa, nos referíamos a um **algoritmo**. A complexidade de algoritmo se refere a qual a ordem de grandeza do tempo que **um algoritmo leva para resolver uma instância de algum problema**. 

Quando falamos da complexidade de um **problema**, estamos nos referindo à complexidade do **algoritmo mais eficiente que resolve um problema**. Ao invés de analisar a complexidade de problema em relação à entrada em si, analisamos em relação ao **tamanho** da entrada. Isto é, se a entrada é um inteiro de 8 bits, veja que dobrar o valor do inteiro não altera o **tamanho** desse valor: continua um inteiro de 8 bits; 

Dizemos que um problema é **polinomial** se a eficiencia do melhor algoritmo que resolve uma instância desse problema é polinomial em relação ao tamanho da entrada:
$$
T = \Omicron(N^\alpha)
$$
Onde N é o tamanho da instância. Problemas polinomiais são frequentemente referidos como problemas **Tratáveis**, ou **fáceis**.



Dizemos que um problema é **exponencial** se a eficiência do melhor algoritmo que resolve uma instância desse problema é **exponencial** em relação ao tamanho da entrada:
$$
T = \Omicron(2^N)
$$
Um exemplo de problema exponencial é o problema de subset sum. 

**Tipos de problemas**

Neste momento, é útil quebrar todo problema que iremos abordar em três categorias:

* Problemas de **otimização**: São problemas que buscam o **melhor valor para uma instância**. Exs:
  * Encontre o valor ótimo para a mochila com capacidade C, valores V e pesos P.
* Problemas de **busca**: São problemas que buscam encontrar uma **solução** para um problema
  * Ex.: Dado uma quação ax^2 + bx + c = 0, encontrar a raíz real, se houver
  * Encontre uma mochila válida dados capacidade C, valores V e pesos P
* Problemas de **decisão**: são problemas que visam responder **sim ou não**
  * Dado uma equação ax^2 + bx + c = 0, x1 = 5 é solução?
  * Existe um ciclo hamiltoniano no grafo G?
  * A mochila X = {a, b, c, ...} é válida?

Esses problemas são elencados em ordem decrescente de complexidade: podemos usar um problema de otimização para resolver um problema de busca  e um problema de decisão(Se encontrei uma mochila ótima, naturalmente encontrei uma mochila válida qualquer e também consigo verificar se a mochila é válida ). Também podemos usar um problema de busca para resolver um problema de decisão (Se encontrei um ciclo hamiltoniano num grafo, é natural responder se existe um tal ciclo).



Vamos nos preocupar primariamente com os problemas de **decisão**.

***

### Classes P, NP e coNP

Classe P: quando um problema de **decisão** é polinomial, dizemos que esse problema pertence à classe P.



O conceito NP está relacionado ao processo de **verificação** de um problema. Queremos, por exemplo, verificar se um número t é raíz de ax^2 + b + c = 0. Como podemos fazer isso, e quão rápido?

Agora vamos introduzir dois conceitos auxiliares que vão nos ajudar a definir o que é a classe NP: certificados e verificadores.

Um **certificado** ou **testemunha** é uma regra, ou sequência de instruções que permitem verificar se uma instância é solução do problema. No caso da equação do segundo grau, um certificado seria substituir x por t na equação e verificar se a equação vale 0

Um **verificador** é um programa que toma o certificado e responde se a entrada é valida ou não. O verificador retorna SIM se a instância for positiva, e retorna NÃO se a instância for negativa.



Um problema é **polinomialmente verificável** se ele é de decisão e existe um verificador X que:

1. Para alguma instância "sim", algum certificado leva o verificador a devolver SIM
2. Para cada instância "não", nenhum certificado leva o verificador a devolver SIM

E faz isso em tempo polinomial (Exceto para o caso de rejeição do certificado. Nesse caso não há limite de tempo)

A classe NP é a classe dos **problemas de decisão que são polinomialmente verificáveis**.

Veja: **não confunda problemas que NÃO pertencem a P com problemas NP**. A notação pode parecer confusa, mas não tem nada a ver.

**Classe CoNP**

é a mesmíssima coisa que NP. A diferença é que estamos querendo verificar aqui que uma instância NÃO é solução. Então um problema pertence a classe coNP se ele for de decisão e:

1. Para alguma instância "não", algum certificado leva o verificador a devolver NÃO
2. Para cada instância "sim", nenhum ceritificado leva o verificador a devolver NÃO

E ele faz isso em tempo polinomial.

***

### P = NP ?

É fácil verificar que $ P \subseteq NP $: Se usarmos o próprio algoritmo (que é polinomial) como verificador, é óbvio que o verificador será polinomial.

Ainda não há prova de que P = NP, apesar de existirem algumas suspeitas: ainda não se encontrou um problema NP que não seja P. Como sabemos que P é um subconjunto de NP, se encontrarmos um problema NP que não seja P, acabou: $P \neq NP$.

Mas ainda assim, é uma possibilidade um tanto quanto mágica: ela implica que **todo problema que pode ser resolvido em tempo polinomial também pode ser verificado em tempo polinomial**.

***

### Redução polinomial

Ao estudar problemas na classe NP, podemos estar interessado em descobrir quão difícil é o problema. Ou seja, queremos saber se o problema é polinomial ou não.

Naturalmente, isso é uma tarefa árdua e complexa, então é interessante estudar a dificuldade **relativa** entre dois problemas. Fazemos isso analizando problemas que são **casos específicos**. Ao compararmos dois problemas Y e X queremos responder: **Y é mais difícil que X?**. 



Se Y é um caso específico de X, ou seja, **Y não é mais difícil que X** (em outras palavras, Y é mais fácil que X), dizemos que $Y \leq X$. Afirmamos que **Y é um caso específico de X**. Alguns exemplos:

* Quadrado perfeito <= eq de segundo grau
* Subset sum <= problema da mochila
* Cobertura pequena <= conjunto independente grande.

Formalizando um pouco mais, dizemos que **Y é polinomialmente redutível a X** se:

1. Y <= X
2. Uma instância de Y pode ser transformada em uma instância de X em tempo polinomial
3. Podemos resolver a instancia de X e obter uma resposta S
4. Podemos converter a resposta S em uma resposta do problema Y em tempo polinomial.

Essencialmente, isso quer dizer que, para resolver Y, eu resolvo no caso geral e retorno o resultado.

![](/home/caio/Documentos/BCC/atual/MAC0338/estudo/reducao.png)

E quando nos referimos a tempo polinomial, estamos sempre nos referindo ao **tamanho de Y**. Uma consequência natural é a seguinte:

Se Y *não* está na classe P e Y ≼ X então X também *não* está na classe P. Além disso, se X está em P, então Y também está em P.

***

### Problemas NP difíceis e NP completos

Faltam só mais algumas definições.



Dizemos que um problema T é NP difícil se, para todo problema H em NP vale que $T \leq H$. Isto é, todo problema em NP é, no máximo, tão difícil quanto H.



Um problema é NP completo se for NP difícil e pertencer a NP



Cooke e Levin, em 1970, **provaram que existe um problema NP completo: o problema de satisfabilidade**.



Agora que temos um problema NP completo Z, se conseguirmos fazer $X \leq Z$, então encontramos outro problema NP completo.



**Até hoje não foi encontrado um único problema NP completo que pertença a P**. Caso isso ocorra, provou-se que P=NP.
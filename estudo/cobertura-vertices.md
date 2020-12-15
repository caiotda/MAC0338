### Cobertura de um grafo

Dado um conjunto de vértices e arestas de um grafo, dizemos que um conjunto S é uma cobertura se **toda aresta de G tem pelo menos uma ponta em S**.

Alternativamente, dizemos que um conjunto de vértices **cobre** uma aresta uv se  se v pertence a C ou se u pertence a C. Uma cobertura é um conjunto que cobre todas as arestas.



Uma cobertura é mínima **se não existe outra cobertura menor**. 



Existe uma relação muito forte entre **cobertura** de um grafo e **conjunto independente**: Sejam V o conjunto de vértices do grafo G. **C é cobertura se e só se V - C é conjunto independente**.

**Prova**: (ida) Se C é cobertura, então toda aresta possui uma ponta em C. Então, nenhuma aresta de G tem todas as pontas fora de C. Assim, V - C é conjunto independente

(volta) Se V - C é conjunto independente, nenhuma aresta possui as duas pontas em V - C, logo, deve possui uma ponta em C. Se toda aresta possui uma ponta em C, C é cobertura.



**Consequencia natural**: Como consequência, se S é cobertura mínima, então V - S é **conjunto independente maximo** e vice versa. Portanto, qualquer algoritmo que resolva o problema do conjunto independente pode ser usado para resolver o problema da cobertura e vice versa.
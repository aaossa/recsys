---
layout: post
title: Comentario sobre "The link-prediction problem for social networks" (2007) de David Liben-Nowell and Jon Kleinberg.
description: Prediciendo interacciones entre humanos
---

> David Liben-Nowell and Jon Kleinberg. (2007). "The link-prediction problem for social networks". Disponible en: [www.cs.carleton.edu](http://www.cs.carleton.edu/faculty/dlibenno/papers/link-prediction/link.pdf)

---

En este paper, los autores formalizan la siguiente pregunta: ¿podemos predecir las siguientes interacciones entre miembros de una red social? Creo que es un problema muy interesante de anlizar y muy relevante para el contexto de los sistemas recomendadores, ya que, potencialmente, podría ser usado para combatir el *cold-start* problem, prediciendo las siguientes relaciones de un usuario nuevo.



### Formalización del problema

Tomemos una red social como un grafo $G=\langle V, E\rangle$ donde cada vértice $e=\langle u, v \rangle \in E$  representa una interacción entre los usuarios $u$ y $v$ en un momento particular, digamos $t(e)$. La diferencia particular de este problema, es que, en lugar de utilizar un arco para determinar que un usuario se relaciona con otro, se usará un arco por cada interacción. Si un usuario interactúa muchas veces con otro, hay muchos arcos paralelos, con tiempos $t(e)$ potencialmente distintos.

Para configurar la experimentación, se definieron cuatro tiempos $t_0 < t'_0 < t_1 < t'_1$. El algoritmo tendrá acceso al grafo $G[t_0, t'_0]$ (intervalo de entrenamiento), retornará una lista de arcos no presente en este que serán las predicción para el grafo $G[t_1, t'_1]$ (intervalo de testeo). 



### Métodos aplicables

Esta sección es similar a los papers tipo "*survey*", donde se hace una revisión de métodos que podrían predecir los *links*.

* **Métodos basados en vecindades de nodos:** Se considera la vecindad de un nodo $x$ , $\Gamma(x)$. Algunas aproximaciones al problema indican que dos nodos tienen una alta probabilidad de unirse si sus vecindades son parecidas.
* **Métodos basados en unir todos los caminos** El puntaje (probabilidad de unión entre dos nodos) es determinado a partir de considerar todos los caminos posibles que unen dos nodos.
* **Modelos de alto nivel:** Aquí se nombran tres "*meta-approaches*" que pueden ser utilizados con cualquiera de los anteriores:
  * *Low-rank approximation*: Esto consiste en analizar la estructura de la matriz de adjacencia $M$ a través de una reducción de dimensionalidad de esta a $M_k$, para lo que se podría usar SVD, por ejemplo.
  * *Unseen bigrams:* Consiste en mejorar las estimaciones para $score(x, y)$ usando los valores de $score(z, y)$ para $z$ similar a $x$. Es decir, usar la estimación de que un usaurio similar esté ligado al usuario consultado.
  * Clustering: Se podría aplicar una técnica de *clustering* para borrar los arcos más "tenues" de la red y luego predecir sobre la red "limpia".

Me gustó bastante esta sección porque tomaba modelos existentes y los adaptaba a la modelación del problema entregada inicalmente. Como en otros papers, establecer un problema inicial, transversal a todo el paper, es la mejor forma de mantener un lenguaje común.



### Resultados

Se presenta una gran cantidad de tablas y gráficos junto con el resultado. La conclusión principal es que entre las técnicas usadas no hay un claro ganador, pero que se supera largamente el predictor *random*, por lo que la lógica de los modelos está funcionando. 

Lamentablemente, los resultados son solo correctos en cerca de un 16% de las predicciones, valor bastante bajo. La modelación del problema está bastante bien, la revisión de técnicas también, pero queda mucho en avanzar en el uso de estos datos, algo que los mismos autores dicen.



---

### Conclusión

Los resultados del paper son bastante alentadores en el sentido de que se obtienen mejores resultados que random, pero están lejos de ser un predictor "real" con solo un 16% de las predicciones. ¿Quizás hay un error en el modelo? ¿Error en los datos? ¿La naturaleza humana es así? Como dijeron los autores, es una pregunta abierta, pero que volverá a aparecer debido a la importancia de las redes sociales hoy en día.



---

### Referencias

* [David Liben-Nowell and Jon Kleinberg. (2007). "The link-prediction problem for social networks"](http://www.cs.carleton.edu/faculty/dlibenno/papers/link-prediction/link.pdf)


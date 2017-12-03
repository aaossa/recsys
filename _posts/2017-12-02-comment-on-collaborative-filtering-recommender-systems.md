---
layout: post
title: Comentario sobre "Collaborative filtering recommender systems" (2007) de Schafer, J. B., Frankowski, D., Herlocker, J., & Sen, S.
description: La mejor introduccion posible al filtrado colaborativo
---

> Schafer, J. B., Frankowski, D., Herlocker, J., & Sen, S. (2007). "Collaborative filtering recommender systems". Disponible en: [Springer](https://link.springer.com/chapter/10.1007/978-3-540-72079-9_9)

---

En este capítulo, los autores hacen una descripción del filtrado colaborativo (VF), modelamiento, diseño, evaluación, todo. Para mi gusto, cuando un artículo está escrito de tan buena forma como este, perfectamente puede formar un libro. Además, se relaciona completamente con lo que vimos en el curso. Un muy buen punto de partida en el mundo de CF.



### Filtrado colaborativo

Como todo buen artículo, define un problema mínimo inicial. En este caso, toma como ejemplo MovieLens para explicar la relación entre usuarios y ratings. Lamentablemente, en una de las pequeñas fallas para mi gusto de este capítulo, no establecen una formalización del problema. Si bien se establece una intuición de este, no existe una forma de relacionar las ecuaciones que describen cada modelo o métrica con el problema mínimo inicial. Las primeras ecuaciones vienen a aparecer a la hora de describir lo algoritmos de predicción.



### *Design Tradeoffs*

Se profundiza en distintos tipos de evaluación que pueden ser usados, con sus respectivas ventajas y desventajas. Me gustó que a cada *tradeoff* se le dedicara un par de párrafos explicando todo el problema. Creo que es una buena introducción, bastante intuitiva a estos, que rápidamente convence al lector de que el feedback explícito es la información más valiosa, pero dificil de conseguir, mientras que el feedback implícito está en grandes cantidades, pero no entrega información completa (hay que saber ocuparla).



### Evaluación

Los primeros métodos de evaluación descritos no son específicos a CF, pero es bueno tenerlos a mano, aunque poner un par de ecuaciones para ejemplificar hubiera sido positivo. Eché de menos un comentario sobre los aspectos "no directamente medibles" de los sistemas recomendadores, que son los que provienen de evaluaciones con usuarios. 



---

### Conclusión

Gran lectura para introducir el mundo del filtrado colaborativo. Permite formar una idea muy buena a raiz de (casi) pura intuición. En algunas partes faltaron ecuaciones para describir matemáticamente lo que sucede, y en otras faltaron un par de temas por cubrir, como las evaluaciones con usuarios. En mi opinión, si bien es un paper introductorio, hubiera sido bueno repasar algunos modelos del estado del arte, aunque es posible que en ese año (2007) el problema no hubiera sido muy cubierto (Aunque lo dudo, porque ya eran los años del Netflix Prize).



---

### Referencias

* [Schafer, J. B., Frankowski, D., Herlocker, J., & Sen, S. (2007). "Collaborative filtering recommender systems"](https://link.springer.com/chapter/10.1007/978-3-540-72079-9_9)


---
layout: post
title: Comentario sobre "Collaborative Filtering for Implicit Feedback Datasets" (2008) de Hu, Y., Koren, Y., & Volinsky, C.
description: ¿Cómo utilizar el feedback implícito?
---

> Hu, Y., Koren, Y., & Volinsky, C. (2008). "Collaborative Filtering for Implicit Feedback Datasets". Disponible en: [yifahnhu.net](http://yifanhu.net/PUB/cf.pdf)

---

El paper escrito por Hu, Koren y Volinsky propone un nuevo modelo para el uso de *feedback* implícito, donde a diferencia del *feedback* explícito, no hay evidencia clara de los *items* que al usuario no le gustan. Es por ello que la propuesta es asociar las *features* que se poseen con el nivel de confianza que se tiene del gusto de la preferencia del usuario por el *item*.

Inicialmente los autores hacen una revisión básica de los diferentes tipos de módelos en sistemas recomendadores. Luego proceden a explicar el trabajo previo: modelos de vecindad y de factores latentes, que luego se utilizarán para contrastar el modelo propuesto. Creo que es una muy buena manera de realizar la evaluación del modelo matemáticamente y computacionalmente hablando.

### El modelo

Los autores proponen utilizar $r_{ui}$ para representar las observaciones de eventos entre un usuario y un *item*. Esto se contrasta con la interpretación en el caso del *feedback* explícito, donde representa un *rating*. La idea es interpretar la preferencia de un usuario por un *item* a partir de las observaciones de hechos.

Una interpretación propuesta es "$r_{ui}$ es el número de visitas del usuario $u$ a la página web $i$", lo que permite llegar (de forma ingenua) a una variable binaria de preferencia:

$$p_{ui} = \begin{cases}1,  & r_{ui} \gt 0 \\0, & r_{ui} = 0 \end{cases}$$

Creo que algo que podría complementar la propuesta es explicitar cómo considerar más eventos dentro del *feedback* implicito. Por ejemplo, podría considerarse el número de visitas a la página web $i$ y además el tiempo que pasa en ella.

Luego de esto se muestra la función a minimizar y se propone una forma bastante inteligente de reducir la complejidad de su resolución, llegando a una forma casi lineal (segun los autores).  El problema de la complejidad computacional en los sistemas recomendadores es reconocido y se ha tocado en post anteriores, por lo que una disminución de la complejidad, con ciertos "trucos" algebraicos a partir de la naturaleza de las variables,  es un buen avance.

### Explicación de las recomendaciones 

La estructura del modelo permite recuperar, a través de los factores latentes, las acciones que llevaron a recomendar cierto *item*. Este tema ha sido comentado en clases y es un avance importante para los usuarios finales mas que para los sistemas en sí, porque a través de este "*feedback*" al usuario de la justificación de las recomendaciones se gana confianza del usaurio en el sistema.

En cuanto al experimento, creo que faltó evaluar las recomendaciones con los usuarios reales, para tener conocimiento de las opiniones de los usaurios finales por la razón explicada en el párrafo anterior. De todas formas, se entiende que no fuera así ya que fondo del *paper* apunta al modelo y no a su aplicación.

---

Me llamó la atención ver que Koren y Volinsky aparezcan en este *paper* sobre *feedback* implicito (2008), ya que la semana pasada también eran autores (junto con Bell) de un *paper* sobre factorización matricial (2009). Encuentro emocionante ver como el paper de 2009 se construye a partir de la publicación de 2008 y que esto llevara a los autores a ser parte del equipo ganador del Netflix Prize.

---

### Referencias

* [Hu, Y., Koren, Y., & Volinsky, C. (2008). "Collaborative Filtering for Implicit Feedback Datasets"](http://yifanhu.net/PUB/cf.pdf)


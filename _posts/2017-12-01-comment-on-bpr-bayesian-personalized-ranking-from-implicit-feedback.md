---
layout: post
title: Comentario sobre "BPR Bayesian Personalized Ranking from Implicit Feedback" (2009) de Rendle, S., Freudenthaler, C., Gantner, Z., & Schmidt-Thieme, L.
description: Un modelo que incluye mucha creatividad...
---

> Rendle, S., Freudenthaler, C., Gantner, Z., & Schmidt-Thieme, L. (2009). "BPR: Bayesian personalized ranking from implicit feedback". Disponible en: [arXiv.org](https://arxiv.org/ftp/arxiv/papers/1205/1205.2618.pdf)

---

El paper de Rendle, Fredenthaler, Gantner y Schmidt-Thieme introduce una nueva técnica de recomendación basada en ranking personalizado. La técnica se basa en una innovadora representación de datos de *feedback* implícito y el uso de un análisis Bayeasiano para encontrar una función a optimizar utilizando la curva ROC, grafico que compara los "verdaderos positivos" y los "falsos positivos" de configuraciones de un clasificador.   



### Manejando información incompleta

Si bien la información más relevante se encuentra en el *feedback* explícito,  no siempre es posible conseguir esta información, pero sí es fácil conseguir *feedback* implícito. El *feedback* implícito comunmente se compone de distintos eventos que indican interacción de un usuario con un *item*. 

Uno de los problemas de este tipo de información es que solo tenemos datos positivos, es decir, si un usuario interactuó (a través del evento) con un *item*, pero en caso de que no lo haya hecho no sabemos si es porque no se le ha dado la oportunidad, lo ignoró, no le gusta, etc.

Los autores proponen crear una matriz de preferencias entre pares de items. Con esto, ya no solo se tienen los ejemplos positivos, sino que se cuenta con valores positivos y negativos (además de los desconocidos). Notar que los valores desconocidos son los que deben ser predecidos:

> ![Explicación de la división de datos](/recsys/public/img/bpr-data.jpg)
>
> Para cada usuario, se descomponen los datos en preferencias entre pares de items. Un $+$ indica que el usuario prefiere el item $i$ por sobre el $j$, mientras que el $-$ indica que el usuario prefiere el $j$ por sobre el $i$. Imagen: Recorte del paper original.

En esta parte del paper no me quedó clara a la primera la construcción de ambas matrices ni como son ocupadas después. Quizás con un ejemplo pequeño que explicara todo el proceso, el paper hubiera quedado más claro.



### *Bayersian Personalized Ranking* (BPR)

En la explicación del algoritmo, se describen los criterios a optimizar, se plantea el problema y se explica cómo se produce el aprendizaje. Creo que aquí es importante recordar que la propuesta apunta a aprender un ranking personalizado, es decir, para cada usuario, que sea un orden total para los ítems.

A partir de la formulación del modelo Bayesiano se derivan las ecuaciones del modelo. Por ejemplo, a continuación se formula el estimador a optimizar:

> ![BPR-Opt](/recsys/public/img/bpr-opt.jpg)
>
> El estimador incluye un parametro de regularización específico para cada modelo, $\lambda_{\Theta}$. Imagen: Recorte del paper original.

Uno de los fuertes uspuestos del modelo, es que los usuarios actúan de forma independiente entre sí. Esto puede no parecer un problema, pero a mi parecer, en un contexto de redes sociales, no siempre se puede asumir eso, ya que la actividad de un usuario es visible para otros y puede influir en sus decisiones. 

Como $BPR-Opt$ es la función a optimizar, debe ser derivada y aprendida. Esto permite que sea aprendida a través de métodos clásicos como el del gradiente o SGD. La ecuación correspondiente se añade a continuación: 

![BPR-Opt derivada](/recsys/public/img/bpr-optder.jpg)

Luego, el algoritmo de aprendizaje sería:

> ![Algoritmo de aprendizaje de BPR](/recsys/public/img/bpr-algo.jpg)
>
> Notar que $\alpha$ es el *learning rate* y el parámetro de regularización se mantiene. Imagen: Recorte del paper original.

### Evaluación

Además de toda la derivación del modelo, explicación del algoritmo, el planteamiento directo del algoritmo de aprendizaje y la comparación de este con otros modelos, los autores nos regaln la evaluación del modelo con dos *datasets*. Este punto es algo que he criticado de otros artículos, que no muestran su modelo sobre ningún dato, solo lo plantean. Este es uno de los más completos en ese sentido. Además, sus resultados son bastante favorables:

> ![Resultados de BPR sobre los datasets](/recsys/public/img/bpr-datasets.jpg)
>
> La métrica de comparación es el área bajo la curva ROC (explicada al inciio). Además de medir esto, se compara con la misma métrica a otros modelos que conforman el estado del arte en recomendadores. Imagen: Recorte del paper original.

---

### Conclusión

Este paper es uno de los más completos que he visto a la hora de plantear un nuevo modelo. Tiene la explicación matemática del modelo, bastante bien fundamentada, y una evaluación y comparación con otras técnicas. Un factor común entre este y otros papers que he encontrado completos es Rendle entre los autores. 

BPR tiene bastante creatividad, primero con la redefinición de los datos implícitos y luego con la creación de la función a optimizar. Además, tuvo buenos resultados en los *datasets* usados en la evaluación. Este es un modelo que conocía poco y del que me gustaría comprender más.



---

### Referencias

* [Rendle, S., Freudenthaler, C., Gantner, Z., & Schmidt-Thieme, L. (2009). "BPR: Bayesian personalized ranking from implicit feedback"](https://arxiv.org/ftp/arxiv/papers/1205/1205.2618.pdf)


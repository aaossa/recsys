---
layout: post
title: Comentario sobre "A survey of active learning in collaborative filtering recommender systems" (2016) de Mehdi Elahi, Francesco Ricci, Neil Rubens.
description: Active learning al rescate
---

> Mehdi Elahi, Francesco Ricci, Neil Rubens. (2016). "A survey of active learning in collaborative filtering recommender systems". Disponible en: [ScienceDirect](http://www.sciencedirect.com/science/article/pii/S1574013715300150?via%3Dihub)

---

En este (largo) paper, los autores hacen una revisión del estado del arte de técnicas de filtrado colaborativo que utilizan estrategias de aprendizaje activo. Personalmente, lo encontré hermoso y bastante completo, casi como un libro.



### Filtrado Colaborativo

Inicialmente, se hace una descripción del problema de recomendación y como distintas aproximaciones utilizan los datos para recomendar. Gran parte de estas técnicas las hemos estudiado en el curso y en otras lecturas, por lo que fue un agrado leer que tantas técnicas que hemos aprendido se usan hoy (el paper es batante reciente, 2016).

Además de la descripción de cada categoría de modelos, ofrece el planteamiento matemático de cada una, para facilitar el entendimiento del modelamiento. Me parece bastante destacable que las ecuaciones cubran solo la parte general de cada categoría y no un modelo en específico (por ejemplo, en la sección de factores latentes).



### *Active Learning*

Esta es la parte más interesante (para mi gusto). ¿Cómo funciona? Dado un set de entrenamiento de $N$ pares $\{ (x_1, y_1), (x_2, y_2), ..., (x_N, y_N)\}$, donde $x_i$ es un ejemplo y su etiqueta es $y_i$, asumimos que existe un modelo que hace el mapeo desde $X$ a $Y$, $M:X \rightarrow Y$ y una función $Loss(M)$ que mide el error del modelo. En cada iteración $j$ del aprendizaje activo, el modelo puede hacer una consulta $q_j \in potentialQueries \subset X$ con la que obtiene $y_j$ (desconocido hasta antes de hacer la consulta). Con esto, el modelo $M$ puede ser re-entrenado y convertirse en $M'$ que, dado que $q_j$ era desconocido hasta antes de re-entrenar y que $y_j$ es correcto:

$Loss(q_j)=E(Loss(M'))$

El algoritmo general planteado es el siguiente:

> ![Algoritmo general de aprendizaje activo](/recsys/public/img/al-algo.jpg)
>
> Algoritmo general de Active Learning. Imagen: Recorte del paper original.

La idea de usar active learning es intentar obtener más datos desde los usuarios cuando no tenga información suficiente para hacer una recomendación.

Me gustó que en esta sección se explicara con un ejemplo básico y se planteara el aprendizaje de forma general, y con un algoritmo, para proceder a explicar la aplicación de esta estrategia en los modelos que ya conocemos.



### Filtrado Colaborativo + *Active Learning*

En el paper se describen distintas estrategias de aprendizaje, categorizadas en personalizadas y no-personalizadas, y cada una sub-dividida en *single-heuristic* y *combined-heuristic*. Hay mucha matemática y categorización en esta sección del artículo. 

La primera división viene de a quienes se les piden los datos en el aprendizaje. La categoría no-personalizada le pide a todos los usuarios que evaluen un mismo item, ignorando observaciones anteriores, mientras que la estrategia personalizada propone un item a un usuario en base a lo que ya han evaluado.

La segunda división viene de la cantidad de estrategias consideradas a la hora de seleccionar los items de los que se pedirá evaluación. La *single-heuristic* utiliza un solo criterio, mientras que la *combined-heuristic* una hibridación de estrategias.



### Comparación

Una de las mayores sorpresas es la tabla de comparación de *performance* de cada estrategia de aprendizaje presentada en el artículo. Esto demuestra que hay un gran trabajo de recopilación en el paper, fundamentado y explicado a lo largo de sus páginas. Me gustó bastante el tono del paper y el análisis comparativo de los autores. 



---

### Conclusión

Mucho de lo que hemos aprendido en el curso me permitió entender el paper, bastante reciente, sobre el estado del arte. Además, la parte que no hemos cubierto tanto, aprendizaje activo, estaba muy bien explicada, y el análisis de las estrategias de aprendizaje estaba muy completo. Lo que más destaco es que este es uno de los pocos papers tipo "*survey*" que veo, que describe y explica los modelos en lugar de limitarse a citar para funcionar como puntero.



---

### Referencias

* [Mehdi Elahi, Francesco Ricci, Neil Rubens. (2016). "A survey of active learning in collaborative filtering recommender systems"](http://www.sciencedirect.com/science/article/pii/S1574013715300150?via%3Dihub)


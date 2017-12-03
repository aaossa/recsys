---
layout: post
title: Comentario sobre "Collaborative filtering for social tagging systems, an experiment with CiteULike" (2009) de Parra, D., & Brusilovsky, P.
description: Atacando un problema de recomendacion a partir del analisis del mismo
---

> Parra, D., & Brusilovsky, P. (2009). "Collaborative filtering
>  for social tagging systems: an experiment with CiteULike". Disponible en: [dl.acm.org](https://dl.acm.org/citation.cfm?id=1639757)

---

En este paper, los autores se enfrentan a la recomendación de artículos en CiteULike. Para contextualizar, las implementaciones tradicionales de filtrado colaborativo (CF) no estaban dando buenos resultados en sistemas de etiquetado colaborativo. Por esto, tarea utilizan tres variantes de filtrado colaborativo (CF) basado en usuarios, utilizando algunos ajustes que dieron buenos resultados.



### *CiteULike*

[CiteULike](http://www.citeulike.org/) es un sitio para manejar y descubrir referencias a artículos.  Contextualizando esto dentro de un sistema recomendador, los usuarios se relacionan con los artículos, los items en este caso. Los autores argumentan que a pesar de que tanto el filtrado colaborativo como el basado en usuarios dieron buenos resultados, se necesitan nuevas aproximaciones a la recomendación por las siguientes razones:

* El contenido es contribuido por usuarios, por lo que es más diverso en su naturaleza y calidad que el creado centralmente.
* No hay ratings, solo un evento: el usuario guardó esta referencia.
* La perdida del control de calidad (por la primera razón) es compensada por la presencia de *tags* (etiquetas) y por conexiones explícitas entre usuarios.

Para el usuario se utilizaron usuarios centrales, los que quieren recibir recomendaciones, seguramente debido a que no se cuenta con la base de datos completa, sino que solo con un extracto que fue obtenido con un *crawler* desde CiteULike. Me hubiera gustado una fundamentación de esta idea, pero asumo que se debe a lo que observé.



### Algoritmos usados

Los autores describen tres variaciones de filtrado colaborativo usadas en esta tarea de recomendación:

* ***Classic Collaborative Filtering (CCF):*** Es el clásico modelo de CF que usa la correlación de Pearson sobre los ratings para determinar la similaridad entre dos usuarios. Primero se determinan los 10 usuarios más similares al usuario central, y luego se rankean los artículos de estos usuarios para realizar la recomendación.
* ***Neighbor-weighted Collaborative Filtering (NwCF):*** Es una mejora sobre la implementación anterior que obtiene los usuarios de la misma forma, pero que considera el número de evaluadores (personas que dieron rating) en el cálculo del ranking de artículos.
* ***BM25-based Similarity (BM25):*** Se realiza un cálculo de similaridad basada en el modelo BM25. Se calcula la similaridad entre el usuario central y un vecino, representado como un conjunto de *tags* con sus respectivas frecuencias. Después de calcular la similaridad entre cada usuario y vecino, se obtienen los $N$ más ismilares y se calcula el ranking con la fórmula del modelo anterior.

Cabe destacar que, para cada modelo, se muestra la función de predicción de rating respectiva, lo que da un sustento matemático asociado a la modelación propuesta. Quizás una pequeña explicación formal del problema, antes de la descripción de los algoritmos, hubiera facilitado la comprensión de las ecuaciones.



### Resultados

A la hora de comparar los resultados de los distintos modelos, se utilizan los 3 propuestos (el último con una variación en el número de vecinos). Se ofrece una tabla con distintas métricas:



> ![Resultados](/recsys/public/img/citeulike-results.jpg)
>
> Métricas aplicadas sobre los modelos utilizados. Imagen: Recorde del paper original.

Me hubiera gustado la inclusión de modelos *baseline*, como los nombrados inicialmente, para comparar en cada métrica las mejoras y analizar estas. Destaco que se utilizó una técnica para medir la novedad, que no había visto en otros papers.



---

### Conclusión

Este es el tipo de papers que me gusta. Toma un problema, lo explica, lo analiza, le da unas vueltas y propone posibles soluciones novedosas. En el artículo se proponen tres aproximaciones distintas, que entregaron resultados favorables y permitieron aprender más del problema.



---

### Referencias

* [Parra, D., & Brusilovsky, P. (2009). "Collaborative filtering for social tagging systems: an experiment with CiteULike"](https://dl.acm.org/citation.cfm?id=1639757)


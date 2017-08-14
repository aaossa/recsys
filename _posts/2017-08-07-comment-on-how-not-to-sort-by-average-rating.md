---
layout: post
title: Comentario sobre "How Not To Sort By Average Rating" (2009) de Evan Miller
description: Evaluacionando desde recomendaciones en base a evaluaciones "positivo"/"negativo"
---

> "How Not To Sort By Average Rating" (2009), Evan Miller, disponible en: [evanmiller.org](http://www.evanmiller.org/how-not-to-sort-by-average-rating.html).

---

En su artículo **"How Not To Sort By Average Rating"** ("Como no ordenar por *rating* promedio"), Evan Miller nos coloca en una situación donde debemos ordenar ítems desde el de mayor rating al de menor rating. La dificultad radica en que **no todos los productos tienen la misma cantidad de ratings**, por lo que métricas basadas en la diferencia absoluta entre ratings positivos y negativos para un ítem, o la proporción de ratings positivos, fallan.

La propuesta del autor es utilizar el intervalo inferior del **[*Wilson score* con un parámetro Bernoulli](https://en.wikipedia.org/wiki/Binomial_proportion_confidence_interval#Wilson_score_interval)**. El uso de esta función de *scoring* permite considerar la incertidumbre de tener un número pequeño de *ratings*, pero dado que considera una distribución Bernoulli estamos atados a considerar que los experimentos (*ratings*) solo tienen dos posibles resultados: **éxito o fracaso** (*rating* positivo o negativo).

> ![Ecuacion del intervalo de Wilson](/recsys/public/img/wikimedia-wilson-scoring-interval.jpg)
> Ecuación del intervalo de Wilson, desarrollada por Edwin Bidwell Wilson en 1927. Imagen: [Wikimedia](https://wikimedia.org/api/rest_v1/media/math/render/svg/98574edd47e0f7aa49666e38d6dc2b43e2cbb71c)

A pesar de que el artículo original es del año 2009 (bastante tiempo en el área de sistemas recomendadores), este se mantiene relevante, ya que es un problema que sigue existiendo. Sin ir mas lejos, sitios como [UrbanDictionary](https://www.urbandictionary.com/) siguen utilizando el sistema de voto positivo/negativo. La solución propuesta por Miller resuelve el problema de ese momento, permitiendo **evaluar bajo la misma lupa a distintos ítems que tengan dispar cantidad de evaluaciones**. Además, existen distintas aplicaciones en las que este algoritmo sería útil, siempre que las acciones tengan resultado éxito/fracaso.

Pero el mundo evoluciona y **hoy los sistemas de evaluación disponibles para los usuarios son más complejos**. Por ejemplo, los sistemas de evaluación por cantidad de estrellas no se pueden resolver como evaluaciones con resultado éxito/fracaso. El sistema propuesto tampoco considera el momento en que las evaluaciones fueron hechas (*aging*) donde queremos que los votos positivos más recientes tengan más peso que aquellos de mayor "edad". Sistemas similares han sido usados por [Hacker News](https://medium.com/hacking-and-gonzo/how-hacker-news-ranking-algorithm-works-1d9b0cf2c08d) y [Reddit](https://medium.com/hacking-and-gonzo/how-reddit-ranking-algorithms-work-ef111e33d0d9).

> ![Captura de Hacker News](/recsys/public/img/hacker-news-capture.jpg)
> Hacker News considera un factor de decaimiento (o tiempo) y un factor de gravedad para ordenar sus entradas. Imagen: Captura propia

En resumen, el artículo cumple con lo prometido en el título presentando soluciones ingenuas, pero que son comunmente usadas, procediendo a explicar por qué están mal y proponiendo un método que permite incluir dichos errores en el cálculo del *ranking*. Pero hoy nos interesan más cosas, como la dimensión temporal de las evaluaciones y el tamaño del rango de evaluación, para lo que han surgido nuevas soluciones. Sin ir mas lejos, el mismo autor cubre el problema de evaluar items con un rango mayor de evaluaciones (5, 10 o K estrellas) en su artículo ["Ranking Items With Star Ratings" (2014)](http://www.evanmiller.org/ranking-items-with-star-ratings.html), por lo que **este es un indicio de lo rápido que evoluciona el mundo de los sistemas recomendadores**... lo que será abarcado en futuros *posts*.

---

### Referencias

* [How Not To Sort By Average Rating - Evan Miller](http://www.evanmiller.org/how-not-to-sort-by-average-rating.html)
* [How Hacker News ranking algorithm works - Amir Slihefendic](https://medium.com/hacking-and-gonzo/how-hacker-news-ranking-algorithm-works-1d9b0cf2c08d)
* [How Reddit ranking algorithms work - Amir Salihefendic](https://medium.com/hacking-and-gonzo/how-reddit-ranking-algorithms-work-ef111e33d0d9)
* [Reddit's comment ranking algorithm - Possibly Wrong](https://possiblywrong.wordpress.com/2011/06/05/reddits-comment-ranking-algorithm/)
* [Ranking Items With Star Ratings - Evan Miller](http://www.evanmiller.org/ranking-items-with-star-ratings.html).


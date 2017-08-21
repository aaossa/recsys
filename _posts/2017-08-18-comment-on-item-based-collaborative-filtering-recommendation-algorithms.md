---
layout: post
title: Comentario sobre "Item-based collaborative filtering recommendation algorithms" (2001) de Sarwar, B., Karypis, G., Konstan, J., & Riedl, J.
description: Una nueva propuesta de filtrado colaborativo que permite aprovechar la naturaleza poco dinámica de los items para precalcular el modelo basandose en los items y no en los usuarios

---

> Sarwar, B., Karypis, G., Konstan, J., & Riedl, J. (2001). "Item-based collaborative filtering recommendation algorithms". Disponible en: [wwwconference.org](http://wwwconference.org/www10/cdrom/papers/pdf/p519.pdf).

---

El paper de Sarwar, Karypis, Konstan y Riedl llega a proponer un nuevo algoritmo de recomendación de filtrado colaborativo, esta vez basado en items (IB-CF). El objetivo del filtrado colaborativo es **sugerir nuevos ítems (a.k.a predecir la utilidad de cierto item) a un usuario particular en base a las evaluaciones de usuarios similares**.

Algunos problemas del filtrado colaborativo basado en usuarios (UB-CF) son la **baja densidad de la matriz** y que el algoritmo de vecinos cercanos **no es escalable**, ya que es mas preciso cuando considero más vecinos (`k`) y su complejidad depnede del número de ítems (`d`) y de usuarios (`n`). (La complejidad de UB-CF: `O(dnk)`). Si el número de usuarios es muy dinámico, la matriz debe ser recalculada muchas veces con esa tremenda complejidad computacional.

> ![Comparación entre UB-CF e IB-CF](/recsys/public/img/collaborative-filtering-basics.jpg)
> En UB-CF buscamos usuarios similares, mientras que en el IB-CF buscamos itemes similares. Imagen: [www.salemmarafi.com](http://www.salemmarafi.com/code/collaborative-filtering-with-python/)

Siguendo el paper, con IB-CF **primero calculamos la similaridad de los ítems**, en el paso de construcción del modelo, y **luego hacemos la predicción** en la fase de recomendación, donde se usan los items mas similares a los que un usuario ya evaluo para generar las recomendaciones.

Sin entrar al detalle matemático, se puede notar que una de las ventajas de IB-CF está en que **si el número de ítems es menos dinámico que el de usuarios, las similaridades (la fase de construcción del modelo) pueden ser calculadas de forma previa** y recalculada solo cuando sea necesario. Un punto débil de la implementación es que los productos novedosos, que cuentan con pocas evaluaciones, sufren de cierto tipo de "inanición" (o "no-recomendación")

> **Dato freak:** El filtrado colaborativo basado en items fue usado por primera vez **en 1998** por **Amazon.com**, mientras que el paper fue publicado **en 2001**. Fuente: [La patente relevante](https://www.google.com/patents/US6266649)

Un punto debil del paper es que **para la evaluación experimental utilizaron solamente un dataset**, MovieLens, que aunque haya sido uno de los más utilizados en el área, solamente es un problema de recomendación particular, que **no representa todo el espectro de problemas de recomendación que se podrían enfrentar**. Hubiera sido mejor si consideraran un dataset con gran densidad y otro con una baja densidad de evaluaciones por item, para permitir la discusión del segundo punto del párrafo anterior.

El paper se necuentra bastante fundamentado y es bien completo, incluso **discutiendo cómo se calcula la similaridad entre los items**. También creo que es destacable que usaran como *benchmark* un sistema basado en usuarios, ya que lo que el paper propone es precisamente **un nuevo enfoque al problema que enfrenta el uso de UB-CF**.

---

Como comentario personal: **Si estas cosas fueron inventadas hace casi 20 años, no me imagino las cosas que se están desarrollando hoy.**

---

### Referencias

* [Sarwar, B., Karypis, G., Konstan, J., & Riedl, J. (2001). "Item-based collaborative filtering recommendation algorithms"](http://wwwconference.org/www10/cdrom/papers/pdf/p519.pdf)
* [US 6266649 B1 (patent) - "Collaborative recommendations using item-to-item similarity mappings "](https://www.google.com/patents/US6266649)
* [Item-based collaborative filtering - CS Carleton](http://www.cs.carleton.edu/cs_comps/0607/recommend/recommender/itembased.html)

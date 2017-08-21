---
layout: post
title: Comentario sobre "Slope One Predictors for Online Rating-Based Collaborative Filtering" (2005) de Lemire, D., & Maclachlan, A.
description: Una tecnica que permite reducir el costo computacional del filtrado colaborativo (entre otras cosas) aproximando los predicciones con funciones del tipo `f(x) = x + b`
---

> Lemire, D., & Maclachlan, A. (2005). "Slope One Predictors for Online Rating-Based Collaborative Filtering". Disponible en: [cogprints.org](http://cogprints.org/4031/1/lemiremaclachlan_sdm05.pdf).

---

Slope One es una familia de algoritmos introducidas por Lemire y Maclachlan como una extensión al filtrado colaborativo que es mas fácil de implementar, mas eficiente y dinámica, todo con un rendimiento similar a los algoritmos más complejos.

En el paper se proponen 3 nuevos esquemas de filtrado colaborativo: Promedio por usuario, Desviación de la media y Coseno ajustado basado en items. Este es uno de los pocos algoritmos que considera efectivamente el número de evaluaciones de un item, en su versión del esquema Slope One con pesos.

A pesar de lo positivo que se destaca del paper, creo que hubiese sido mejor utilizar más métricas de error, ya que MAE no es la única métrica conocida que podría darnos información relevante.

---

### Referencias

* [Lemire, D., & Maclachlan, A. (2005). "Slope One Predictors for Online Rating-Based Collaborative Filtering"](http://cogprints.org/4031/1/lemiremaclachlan_sdm05.pdf)

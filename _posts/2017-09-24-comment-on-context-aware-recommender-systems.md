---
layout: post
title: Comentario sobre "Context-Aware Recommender Systems" (2012) de Adomavicius, G., Mobasher, B., Ricci, F. & Tuzhilin, A.
description: Incorporando el contexto como una nueva dimension
---

> Adomavicius, G., Mobasher, B., Ricci, F. & Tuzhilin, A. (2012). "Context-Aware Recommender Systems". Disponible en: [aaai.org](https://www.aaai.org/ojs/index.php/aimagazine/article/view/2364)

---

Tradicionalmente, los sistemas recomendadores trabajan con información latente, como los *ratings* y los usuarios. Sin embargo, existen algunos dominios donde las aplicaciones ganan poder predictivo con información del contexto de la recomendación. Por ejemplo, la hora en la que un usuario visita una página de *e-commerce* para adquirir un producto puede ser relevante en sus preferencias. Estos son los sistemas recomendadores conscientes de contexto (*CARS*).

Los contextos son observables en distinta medida y cambian a lo largo del tiempo. En la primera categoría se distinguen los completamente observables (donde el sistema sabe todo sobre el contexto), los parcialmente observables y los no observables (donde no hay información sobre los factores contextuales). Además, el contexto puede ser estático (la estructura de los factores y su relevancia se mantiene en el tiempo) o dinámicos.

La propuesta del paper es incorporar al contexto en la función de *rating*, como parte del *input* del sistema recomendador:

$$R: Users \times Items \times Contexts \rightarrow Ratings$$

La matriz de contextos ($Contexts$) representaría el conjunto de factores que describen las condiciones bajo las que a un par usuario-item se le asigna un *rating*. Esto, como ya se dijo, hace que el sistema recomendador entregue mejores recomendaciones, pero también aumenta el tamaño del *dataset*, la complejidad de los algoritmos y las matrices de datos serán menos densas (más datos posibles, más vacíos posibles).

> ![Incorporación de contexto en el sistema recomendador](/recsys/public/img/context-matrix.png)
>
> Incorporar el contexto en un sistema recomendador, por ejemplo el clima, agrega una nueva dimensión. Imagen: [Matthias Braunhofer @ SlideShare](https://www.slideshare.net/mbraunhofer/hybridisation-techniques-for-coldstarting-contextaware-recommender-systems)

La incorporación del contexto puede ocurrir en distintas etapas:

* Partir contextualizando los datos de $U \times I \times C \times R$ y luego trabajar con los datos contextualizados (*contextual prefiltering*),
* Generar las recomendaciones para un usuario y luego contextualizarlas (*contextual postfiltering*),
* O recomendar utilizando el contexto como dato y luego contextualizar la recomendación para el usuario en particular (*contextual modeling*)

Un análisis que se podría haber hecho en el paper es, para algun caso particular, comparar los resultados de las distintas recomendaciones o analizar la complejidad de algunos algoritmos sobre este caso hipotético, ya que las matrices van cambiando de tamaño y, a pesar de que los paradigmas se muestran como *pipeline*, esto influye en el tiempo de ejcuicón. Un problema que no se menciona es que al agregar una nueva dimensión al sistema recomendador, agregamos una nueva dimensión donde podríamos tener *cold-start*.

> ![Problemas agregando elementos nuevos](/recsys/public/img/context-cold-start.png)
>
> Cuando agregamos un nuevo contexto también puede haber *cold-start*. Imagen: [Matthias Braunhofer @ SlideShare](https://www.slideshare.net/mbraunhofer/hybridisation-techniques-for-coldstarting-contextaware-recommender-systems)

Un tema interasante que se podría haber profundizado en la sección de aplicaciones de *CARS* es como se incorpora el contexto en el *feedback* que se le da al usuario. ¿Es explícito? ¿Se le dice al usuario "se te recomendó esto porque está lloviendo" o "porque estás en X ciudad"? ¿Existen otras opciones? Creo que es un tema interesante de profundizar, ya que las preferencias del usuario cambian con el contexto, pero también cambian con el *feedback* que la aplicación le entrega, aunque esto podría tener la misma dificultad, pero también abarcarse de la misma forma, que la justificación de recomendaciones común ("te recomendamos esto porque te gusta X item").

---

Creo que el paper se contextualiza (*heh*) en un momento en que los *CARS* estaban recién surgiendo y quedaba mucho por explorar, aunque ya habían aplicaciones que los utilizaban. De todas formas me pareció bastante interesante y me gustaría tener alguna comparación, de una misma aplicación, con y sin uso del contexto.

---

### Referencias

* [Adomavicius, G., Mobasher, B., Ricci, F. & Tuzhilin, A. (2012). "Context-Aware Recommender Systems"](https://aaai.org/ojs/index.php/aimagazine/article/view/2364)


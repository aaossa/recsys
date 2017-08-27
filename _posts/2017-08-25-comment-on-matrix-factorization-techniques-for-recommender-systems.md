---
layout: post
title: Comentario sobre "Matrix Factorization Techniques for Recommender Systems" (2009) de Koren, Y., Bell, R., & Volinsky, C.
description: El poder de la factorización matricial (SVD) mostrando todo su potencial para ganar una de las competencias más recordadas del área, el Netflix Prize
---

> Koren, Y., Bell, R., & Volinsky, C. (2009). "Matrix Factorization Techniques for Recommender Systems". Disponible en: [base.sjtu.edu.cn](http://base.sjtu.edu.cn/~bjshen/2.pdf)

---

Este paper visita una gran cantidad de temas, por lo que se descompondrá en distintas secciones y se visitará cada una por separado, siempre teniendo al paper como referencia.

---

Dentro de las distintas aproximaciones al problema de la recomendación se distinguen 3 tipos: filtrado colaborativo (CF), filtrado basado en contenido y sistemas híbridos. Entre los métodos de filtrado colaborativo se encuentran los basados en vecindades o similaridad entre ítems o usuarios, donde es común el uso de algoritmos como k-NN. En el paper de Koren, Bell y Volinsky se describe otro método de CF, basado en factores latentes, que utiliza la factorización matricial como una de sus herramientas. 

A diferencia de los métodos de CF, donde la recomendación es realizada en base al comportamiento de usuarios similares y/o sobre ítems similares, los métodos de factores latentes buscan **describir las caracteristicas de los ítems y las preferencias de los usuarios por estas características en un espacio común**. Para lograr esto, se infieren factores a partir de las evaluaciones, lo que crea nuevas dimensiones que podrían ser dificiles de interpretar, pero que en la práctica permiten interpretaciones humanamente entendibles (como el género de una canción, por ejemplo).



### Método de factorización matricial

Si bien la información más relevante se encuentra en el *feedback* explícito, el *rating* que un usuario específico le asigna a un *item* específico, es dificil conseguir un número de evaluaciones significativo, por lo que las matrices usuario-item son muy poco densas. Como indica el paper, una de las fortalezas de la factorización matricial es que permite incluir información adicional a las evaluaciones explícitas. 

El *feedback* implícito comunmente se compone de distintos eventos que indican interacción de un usuario con un *item*. Por ejmplo, en Spotify no se utilizan *ratings*,  pero sí se considera si un usuarió escuchó una canción, cuando lo hizo, si le dió *thumps up* e incluso si se saltó el tema alguna vez.

> ![Captura de Spotify mostrando la lista "Descubrimiento semanal"](/recsys/public/img/spotify-weekly.jpg)
>
> Spotify utiliza este *feedback* para hacer sus recomendaciones en radios, listas sugeridas y en particular en su lista de "Descubrimiento semanal". Imagen: Captura propia.

Lamentablemente el paper no indica en detalle como aplican esta aproximación, el uso de *feedback* implícito, en el *dataset* del Netflix Prize, porque de acuerdo a lo presentado en [el *dataset* en Kaggle](https://www.kaggle.com/netflix-inc/netflix-prize-data) no se incluye información de este tipo. Solamente se incluye información para identificar a los usuarios y a las películas, los *ratings* y la fecha de la evaluación.

> **Nota:** Al parecer Netflix ya no tiene el *dataset* público por temas de privacidad. De hecho, [este paper](https://www.cs.utexas.edu/~shmat/shmat_oak08netflix.pdf) demuestra que los datos del *dataset* se podían de-anonimizar. De todas formas, la idea del link a *Kaggle* es mostrar qué viene en el *dataset* y no entregar el *dataset* en sí. 



### Predicción de rating

La idea de la factorización matricial es trabajar con usuarios e *items* en un espacio equivalente. Este resultado permitirá trabajar con los vectores representantes de los usuarios e *items* en este nuevo espacio de la siguiente forma:

* $q_i$ : Contiene los pesos de los factores latentes para el *item* $i$.
* $p_u$: Contiene el interés del usuario $u$ por los correspondientes factores latentes.

Esto entrega como resultado que la predicción de rating se calcule como $r_{ui} = q_i^Tp_u$. La dificultad está en calcular los valores para $p_u$ y $q_i$, lo que se traduce en un problema de oprimización no convexo:

![Función a optimizar para aprender los vectores p y q](/recsys/public/img/p-q-optimization-problem.png)

Notar que $\lambda$ es un parámetro de regularización que busca evitar el problema  de sobreajuste (*overfitting*). El paper sugiere dos algoritmos de aprendizaje: el método del descenso por gradiente estocástico y mínimos cuadrados alternantes (ALS). Personalmente no conocía ALS, pero el paper explica su funcionamiento. Se destaca que al usar ALS se gana poder de paralelización, pero no se explica si se pierde precisión o el error se ve afectado de alguna manera. Tampoco se habla de la complejidad computacional de ambos algoritmos de aprendizaje.

Sin embargo, se sigue construyendo y proponiendo nuevos factores que se pueden tomar en cuenta para la recomendación: *biases* (algunos usuarios evaluan mejor que otros en promedio), factores implícitos, el aspecto temporal (las preferencias de los usuarios cambia en el tiempo) y los distintos niveles de confianza asociados al valor de las evaluaciones (un item muy publicitado en algun momento recibirá muchas menos evaluaciones después). Considerando todos estos factores, el problema de optimización de arriba se hace mas complejo, pero más preciso. 



### Reducción de dimensionalidad de datos

Los autores solamente enuncian el uso de SVD para reducir la dimensionalidad de las matrices, pero no explican el detalle de como pasar de la matriz usuario-item a los factores latentes, quizás pensando en el paper como una obligación para el concurso mas que en un aporte al estado del arte.

La idea es descomponer los factores de la matriz de evaluaciones en dos matrices, donde una describe el interés de los usuarios por ciertos factores (*features*) y la otra describe el peso de dicho factor en un item.

> ![Ejemplo de SVD](/recsys/public/img/svd-example.png)
>
> Queremos nuevos descriptores, en una matriz mas densa, sin perder información. Imagen: [Hasso-Plattner-Institut](https://hpi.de/fileadmin/user_upload/fachgebiete/naumann/lehre/SS2011/Collaborative_Filtering/pres1-matrixfactorization.pdf).

Hoy en día se utilizan distintas aproximaciones para encontrar los mejores descriptores de un espacio multidimensional, principalmente para visualizar datos. A la par de SVD se utiliza el Análisis de componentes principales (PCA), siendo calculado de una forma bastante similar (de hecho, [se puede llegar a PCA a partir de SVD](https://stats.stackexchange.com/a/134283)). Un método bastante popular recientemente es **t-SNE**, que es más caro computacionalmente por lo que algunas implementaciones utilizan SVD para reducir la dimensionalidad (digamos, de 10000 a 200 dimensiones) y luego aplican t-SNE para graficar.

> ![Visualización usando t-SNE](/recsys/public/img/fashion-msnist.gif)
>
> Con t-SNE se utilizan las dimensiones más descriptivas, o que mejor separen el *dataset* en base a sus etiquetas, para graficar en un espacio de menos dimensiones. Imagen: [zalandoresearch/fashion-mnist @ GitHub](https://github.com/zalandoresearch/fashion-mnist)



---

### Importancia del Netflix Prize

El Netflix Prize permitió que los métodos de factorización matricial (como SVD) destacaran al ser parte del algoritmo gandaor y ser usados por los equipos de mejor ranking. Si bien esta competencia no llevó a que se desarrollaran muchos nuevos algoritmos o técnicas revolucionarias, si permitió al entorno de los Sistemas Recomendadores darse cuenta de cieras cosas, como que el momento de la evaluación importa, que un solo método no es suficiente (la entrada ganadora usaba **más de 100 algoritmos**) y que hay que considerar el ruido en el *dataset*. 

> **Dato freak:** De acuerdo a [Forbes](https://www.forbes.com/sites/ryanholiday/2012/04/16/what-the-failed-1m-netflix-prize-tells-us-about-business-advice/#69572ea673c9), Netflix no llegó a utilizar el algoritmo ganador debido a que la mejora lograda no se justifica con el esfuerzo necesario para llevar el algoritmo a producción.

Esto me recuerda un poco al caso de [ImageNet](http://www.image-net.org/), una base de datos organizada de acuerdo a [WordNet](http://wordnet.princeton.edu/), con **más de 14 millones de imágenes**. Este *dataset* es la muestra de que **más datos desarrollan mejores algoritmos**. A través de competencias anuales, permitió que el área del reconocimiento visual mejorara de cerca de un 25% de error en 2010 a **menos de un 2% hoy**. 

> ![Resultados de la competencia ImageNet](/recsys/public/img/imagenet-error.png)
>
> La reducción del error en la tarea de reconocimiento visual es clara. Imagen: [Quartz](https://qz.com/1034972/the-data-that-changed-the-direction-of-ai-research-and-possibly-the-world/)

¿Cómo se comparan en su relevancia el Netflix Prize con ImageNet? Esa es pregunta para otro post.



### ¿Qué pasó con el Netflix Prize?

Para cerrar la historia, el equipo conformado por los autores (originalmente "BellKor") se fusionó con el equipo de Andreas Töscher y Michael Jahrer (originalmente "BigChaos") y con el equipo de Martin Piotte y Martin Chabber (originalmente "PragmaticTheory") para conformar el equipo que terminaría siendo el ganador: "BellKor's Pragmatic Chaos". 

> ![Tabla final del Netflix Prize](/recsys/public/img/netflix-prize-leaderboard.jpg)
>
> Tabla de resultados final del Netflix Prize. Cabe destacar que "BellKor's Pragmatic Chaos" logró el mismo porcentaje de mejora que "The Ensemble", pero los primeros ganaron por subir su entrada primero... por 20 minutos. Captura: [Netflix Prize leaderboard](http://www.netflixprize.com/leaderboard.html).

Cabe destacar que cada equipo por su cuenta de todas formas estaba en el "Top 10". "PragmaticTheory" quedó 6°, "BellKor in BigChaos" ("BellKor" + "BigChaos") quedó 7°, "BigChaos" quedó en el décimo lugar y "BellKor" en el lugar 12.

> ![Ganadores del Netflix Prize](/recsys/public/img/netflix-prize-winners.jpg)
>
> Los ganadores del Netflix Prize, de izquierda a derecha: Yehuda Koren, Martin Chabbert, Martin Piotte, Michael Jahrer, Andreas Toscher, Chris Volinsky y Robert Bell. Imagen: [Jason Kempin/Getty Images @ The New York Times](https://bits.blogs.nytimes.com/2009/09/21/netflix-awards-1-million-prize-and-starts-a-new-contest/)



---

### Conclusión

El paper es un buen articulo que resume las tecnicas utilizadas para alcanzar uno de los mejores rendimientos vistos hasta entonces en el Netflix Prize y en el estado del arte. Lamentablemente, pareciera que el documento buscaba explicar las técnicas utilizadas revelando la menor información posible de la implementación. Existe poca descripción de los aspectos matemáticos usados y menos información aun de la aproximación utilizada en el *dataset* particular del concurso. De hecho, [el mismo Xavier Amatriain escribió en Medium](https://medium.com/netflix-techblog/netflix-recommendations-beyond-the-5-stars-part-1-55838468f429) que el equipo ganador utilizó una combinación de 107 algoritmos, por lo que este equipo seguramente utilizaba cantidad similar o un poco menor al momento de esta publicación. Por lo tanto, el paper reune una gran cantidad de información, pero hay que recurrir a muchas de las referencias y buscar por cuenta propia para acceder al conocimiento del articulo, sin llegar a conocer los secretos de una de las implementaciones de mejor rendimiento de la competencia.



---

### Referencias

* [Koren, Y., Bell, R., & Volinsky, C. (2009). "Matrix Factorization Techniques for Recommender Systems"](http://base.sjtu.edu.cn/~bjshen/2.pdf)
* [Narayanan, A., & Shmatikov, V. (2008). "Robust De-anonymization of Large Sparse Datasets"](https://www.cs.utexas.edu/~shmat/shmat_oak08netflix.pdf)
* [SlideShare - Collaborative Filtering at Spotify (Erik Bernhardsson, former Engineering Manager @ Spotify)](https://es.slideshare.net/erikbern/collaborative-filtering-at-spotify-16182818)
* [mit.edu - Singular Value Decomposition (SVD) tuorial](http://web.mit.edu/be.400/www/SVD/Singular_Value_Decomposition.htm)
* [@lvdmaaten - t-SNE](https://lvdmaaten.github.io/tsne/)
* [Quora - What developments have occurred in recommender systems after the Netflix Prize? (respuesta de Xavier Amatriain)](https://www.quora.com/What-developments-have-occurred-in-recommender-systems-after-the-Netflix-Prize/answer/Xavier-Amatriain?srid=uEw8q)


---
layout: post
title: Comentario sobre "A Survey of POI Recommendation in LBSN" (2015) de Yu, Y., & Chen, X.
description: Un paseo por los distintos modelos explicando las ideas incluidas dentro de cada uno
---

> Yu, Y., & Chen, X. (2015). "A Survey of Point-of-Interest 
> Recommendation in Location-Based Social Networks". Disponible en: [www.aaai.org](https://www.aaai.org/ocs/index.php/WS/AAAIW15/paper/viewFile/10132/10253)

---

El paper de Yu y Chen es una revisión del estado del arte en recomendadores de puntos de interés (POIs). Se hace una descripción del problema que resuelven estos recomendadores, utilizada para sentar las bases de los modelos a explicar, se explican y categorizan los modelos, y se entrega una visión a futuro del área. Todo esto se hace en el contexto de redes sociales basadas en localización (LBSN).



### *Point-of-interest (POI) recommendation*

Para establecer una base común a la hora de hablar de estos algoritmos, los autores ofrecen una formalización del problema. Consiste en un conjunto de $N$ usuarios $U=\{ u_1, u_2, ..., u_N\}$ y un conjunto de $M$ lugares, o puntos de interés, $L = \{ l_1, l_2, ..., l_M\}$. El conjunto de POIs visitados por el usuario $u$ es $L_u$, y cada lugar es una tupla codificada de la forma $<longitud, latitud>$. 

Los check-ins (visitas) de los usuarios se convierten a una matriz $C$, donde la entrada $c_{ui}$ es la frecuencia de check-in del usuario $u$ al lugar $i$. Se considera que la frecuencia de check-ins refleja la preferencia del usuario por ese lugar. Normalmente, un usuario visita una poca cantidad de estos puntos de interés, por lo que la matriz es muy poco densa. Además, cada usuario tiene una lista de usuarios con los que se relaciona, reflejado en la matriz de relaciones $S$, donde la entrada $s_{uv}$ indica el valor de "social trust" (concepto no profundizado) que normalmente toma valores binarios ($1$ indica que el usuario $u$ está relacionado con el $v$, $0$ en otro caso). 

El objetivo del recomendador es aprender las preferencias implicitas de acuerdo al historial de check-ins de los usuarios y ofrecer recomendaciones de nuevos lugares en los que el usuario podría estar interesado.

> ![Ejemplo básico de POI](/recsys/public/img/poi-basics.png)
>
> Diagrama básico del modelamiento del problema. Lo que nos interesa son 3 cosas: usuarios, POIs (*items*) y check-ins (eventos). Imagen: [deeplearn.school.blog](https://deeplearn.school.blog/2017/01/02/point-of-interest/).



### Categorización

Los autores describen cuatro aproximaciones al problema, cada uno con distintos modelos representantes:

* **Recomendación basada solo en datos de check-in:** Estos son los sistemas tradicionales, basados en la idea de que la cantidad de check-in  de un usuario en un punto refleja la preferencia de este por ese POI. Esto permite que técnicas de filtrado colaborativo sean utilizadas si consideramos que los POI son items.
* **Recomendación mejorada con influencia geográfica:** La característica diferenciadora de las recomendaciones de las que hablamos es que estamos hablando de lugares, con ubicación geográfica. Aquí aparecen dos intuiciones: los usuarios prefieren visitar POIs cercanos, y prefieren visitar POIs cerca de otros preferidos por el usuario. En este contexto se utilizan modelos que incluyen la ubicación geográfica de los puntos para estimar la preferencia de ese usuario por los demás puntos integrando las intuiciones ya nombradas.
* **Recomendación mejorada con influencia social:** Esta aproximación busca utilizar la naturaleza similar de este problema con el filtrado colaborativo para incluir la influencia social de, por ejemplo, amigos, a través de la inclusión de la similaridad entre usuarios en el modelo.
* **Recomendación mejorada con influencia temporal:** Estos modelos utilizan una función de decaimiento en la influencia de un POI a la hora de hacer la recomendación. Esto permite modelar, por ejemplo, que la tendencia de los usuarios a visitar ciertos lugares cambie en el tiempo.

Cabe destacar que, dentro de cada categoría, se referencian modelos y se explica cómo es que estos incluyen estos cambios en sus funciones. Esto permite demostrar cómo es que la intuición se relaciona con las matemáticas detrás de los recomendadores.



---

### Conclusión

De este paper me gustó que categorizara los modelos para proceder a explicar la idea detrás de cada modelamiento y cómo esta se incluye en las funciones y ecuaciones de cada uno. Creo que cumple con su papel de ser *survey* y no se sale de ese rol. Normalmente me gustan los papers que incluyen diagramas para explicar ideas, seudo-código y graficos mostrando los resultados, pero este paper incluía las matemáticas justas y necesarias para dar a entender las ideas. Bastante bueno para alguien que no sabe tanto de recomendación de POIs.



---

### Referencias

* [Yu, Y., & Chen, X. (2015). "A Survey of Point-of-Interest Recommendation in Location-Based Social Networks"](https://www.aaai.org/ocs/index.php/WS/AAAIW15/paper/viewFile/10132/10253)


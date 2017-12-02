---
layout: post
title: Comentario sobre "Factorization Machines" (2012) de Rendle, S.
description: Uniendo lo mejor de dos mundos en un nuevo modelo
---

> Rendle, S. (2010). Factorization machines. In Data Mining (ICDM), 2010 
> IEEE 10th International Conference on (pp. 995-1000). IEEE.

---

En este paper, Steffen Rendle introduce las maquinas de factorización, o *Factorization Machines* (FM), una combinación de las ventajas de SVM y de los modelos de factorización. Inicialmente se explican las desventajas de las dos técnicas ya comentadas: SVM no funciona bien en filtrado colaborativo debido a la baja densidad de los datos, mientras que los modelos de factorización tienen problemas trabajando con valores reales. 

La propuesta de Rendle es aprender una factorización de cada feature, permitiendo trabajar en un espacio más denso, y aprender los pesos asociados a cada feature. En el paper, se plantea el modelo, se explican (e incluso una se demuestra) las ventajas de FMs sobre SVM y los modelos de factorización, y luego se generaliza su uso. Creo que contraponer el modelo propuesto con otros es una muy buena manera de realizar la evaluación del modelo matemáticamente y mostrar sus propiedades. 

### ¿Cuál es el problema?

En sistemas recomendadores, normalmente se cuenta con una matriz bastante *sparse* (o poco densa) de datos, lo que lleva a que modelos basados en márgenes, como SVM, no aprendan hiperplanos confiables. Por su parte, los modelos de factorización no son aplicables a datos basados en valores reales y requieren esfuerzo de modelación y diseño acorde al problema, mientras que SVM sí es un modelo general. Por esto, la propuesta es unir lo mejor de dos mundos.

Las ideas claves de Rendle para FM son: modelar todas las iteracciones de variables pero usando una parametrización factorizada (como la que viene de los modelos de factorización) en lugar de una parametrización densa como en SVM. Esto permite ignorar que los datos son poco densos, ya que se trabajará sobre un espacio generado por la factorización de cada variable.

### Modelo propuesto: *Factorization Machines*

Primero que todo, destaco que el autor hace algo muy inteligente: utilizar un mismo ejemplo para todo el paper, sentando una base común para la representación del problema a resolver. Entrega un ejemplo lo suficientemente básico como para ser lo más general posible, pero lo suficientemente complejo como para aplicar el modelo propuesto. El ejemplo se muestra a continuación:

> ![Ejemplo propuesto por Rendle](/recsys/public/img/fm-example.jpg)
>
> En este ejemplo, cada vector es un evento, con una parte indicando el usuario que participa en la transacción, el item evaluado, momento de la evaluación, etc. con el *rating* como valor objetivo. Imagen: [Recorde del paper original. Rendle, S. (2010). "Factorization machines"](https://www.csie.ntu.edu.tw/~b97053/paper/Rendle2010FM.pdf)

El modelo propuesto se conforma de las siguientes ecuaciones, donde los parámetros que deben ser estimados son:

* $w \in \mathbb{R}$,  el vector de pesos para cada variable y 
* $V \in \mathbb{R}^{n\times k}$, la matriz que contiene la descripción de cada variable en $k$ factores.

$\hat{y}(x):=w_0+\sum_{i=1}^{n} w_ix_i+\sum_{i=1}^{n}\sum_{j=1}^{n}\langle v_i, v_j \rangle x_ix_j$

Lo que define el modelo es una representación de cada aspecto del vector $x_i$ en $k$ factores, en la i-ésima fila de la matriz $V$. Notar que entonces, el primer término es el intercepto global, el segundo acumula la suma ponderada de las variables $x_i$ con su peso $w_i$ y el último es el producto punto de dos filas de $V$ representando la interacción entre cada par de variables.

Para Rendle, las ventajas del modelo propuesto, listadas en el paper, son:

1. FMs permiten estimar parámetros en datos poco densos (a diferencia de SVM).
2. FMs tiene complejidad lineal, pueden optimizarse en el primal, y no necesita vectores de soporte (a diferencia de SVM).
3. FMs son un predictor general que puede trabajar con valores reales (a diferencia de los modelos de factorización)

Analizaremos punto por punto cada una de las ventajas, explicando su origen.

#### FM > SVM: "FMs estiman parámetros en datos poco densos"

Los datos poco densos son comunes en las representaciones de eventos. Por ejemplo, si un usuario visitó la página de cierto item, le dió *like* a una foto, si una palabra aparece en un texto, etc. colocamos un $1$ en nuestra matriz de eventos, y un $0$ si el evento no ha ocurrido. Estos eventos permiten analizar similaridad entre usuarios, similaridad entre items y secuencias de eventos, por lo que, en mi opinión, son la herramienta más intuitiva a la hora de representar los datos para trabajar con sistemas recomendadores.

La idea para combatir la baja densidad es dividir cada variable en otras, representadas en la matriz $V$ del modelo, lo que permite trabajar con las factorizaciones de cada variable, que a su vez permite modelar las interacciones entre variables. Esta idea es bastante similar a la de otros modelos que prefieren trabajar con una versión reducida del problema que represente las variables en un espacio más denso.

#### FM > SVM: "FMs tiene complejidad lineal"

Viendo la ecuación del modelo propuesto, existe una parte que no parece ser lineal, por lo que podría ser cara computacionalmente. El autor ofrece una demostración de que esta función puede ser calculada en tiempo lineal:

> ![Demostración de complejidad lineal](/recsys/public/img/fm-proof.jpg)
>
> Imagen: [Recorde del paper original. Rendle, S. (2010). "Factorization machines"](https://www.csie.ntu.edu.tw/~b97053/paper/Rendle2010FM.pdf)

¿Por qué esto es importante? Porque permite que la optimización usando el método del gradiente sea factible, facilitando el aprendizaje de los parámetros. De hecho, se muestra el gradiente del modelo en el paper y se ofrece una implementación que utiliza SGD (libFM, ya hablaré de esto).

#### FM > modelos de factorización: "FMs son un predictor general"

Todo el trabajo lo hace el modelo. Este punto no se vuelve a tocar en el paper, pero las interacciones son aprendidas por el modelo (en la matriz $V$), al igual que los pesos de cada una.

### Conclusión

En mi opinión, el paper es una gran introducción de un nuevo modelo. Cuando se está proponiendo algo nuevo, lo primero que hay que hacer es explicarlo desde sus bases y luego compararlo con lo que ya existe. Rendle hace precisamente eso, establece un ejemplo básico, explica su razonamiento, muestra las ecuaciones y luego se pone a comparar. 

Algo que me pareció novedoso es que el nuevo modelo viene acompañado de una implementación. Ya conocía libFM y sabía que tenía un paper asociado, lo que me parece bastante positivo ya que permite utilizar en la práctica el modelo propuesto.

Siguendo esa línea, creo que al paper le faltó utilizar datos reales, mostrar una aplicación, idealmente sobre un dataset conocido y probado, que permitiera dar números y mostrar que en la práctica el modelo (con la implementación) funcionan y entregan "estos" resultados.

---

### Referencias

* [Rendle, S. (2010). "Factorization machines"](https://www.csie.ntu.edu.tw/~b97053/paper/Rendle2010FM.pdf)
* [srendle/libfm @GitHub](https://github.com/srendle/libfm.git)


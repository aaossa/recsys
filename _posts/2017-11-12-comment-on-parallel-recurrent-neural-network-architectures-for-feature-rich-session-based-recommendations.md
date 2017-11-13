---
layout: post
title: Comentario sobre "Parallel recurrent neural network architectures for feature-rich session-based recommendations" (2016) de Hidasi, B., Quadrana, M., Karatzoglou, A., & Tikk, D.
description: Proponiendo una nueva arquitectura a partir de RNNs para mejorar la recomendacion en sesiones
---

> Hidasi, B., Quadrana, M., Karatzoglou, A., & Tikk, D. (2016). "Parallel recurrent neural network architectures for feature-rich session-based recommendations". Disponible en: [dl.acm.org](https://dl.acm.org/citation.cfm?id=2959167)

---

En nuestro día a día visitamos distintas páginas que buscan entregarnos un mejor servicio recomendando alguno de los *items* presentes en su plataforma. Por ejemplo, si queremos ver un video, vamos a una página de videos y esta intentará recomendarnos uno que nos interese ver después. Si estamos navegando por una página de venta de productos y estamos viendo alguno en particular, la página intentará al que podría ser que estemos buscando o que nos interese.

Un problema que enfrentan estas páginas es que, a diferencia de las plataformas que hemos visto previamente, no tienen una "matriz" de usuarios, no tienen datos de usuarios, sino que simplemente de sesiones. ¿Qué es una sesión? Cuando ingresamos a un sitio y vamos haciento *click* sobre los distintos items que nos ofrecen estamos en una misma sesión. Las sesiones separan objetivos del usuario. ¿Cómo es esto? Cuando un usuario ingresa a una tienda virtual está buscando un producto en particular, y hará eso hasta que encuentre lo que busca en una misma sesión.

En el paper de Hidasi, Quadrana, Karatzoglou y Tikk, se explora la posibilidad de aplicar *deep learning* en el proceso de extracción de *features* para generar mejores recomendaciones a partir de datos de sesiones.

### *Deep Learning meets RecSys*

Parte del trabajo relacionado nombrado en el paper, en cuanto a *deep learning*, son los modelos de redes recurrentes o RNN. Las RNNs han mostrado muy buenos resultados en información secuencial, como en tareas de NLP (procesamiento de lenguaje natural), temporales y en videos, por lo que el modelo es un muy buen candidato para trabajar con sesiones, ya que es información secuencial.

> ![Modelo básico de RNN](/recsys/public/img/rnn.jpg)
>
> Básicamente (en términos muy generales), una red recurrente utiliza el pasado para predecir el futuro. Imagen: [Recorte de "Recurrent Neural Networks (RNN) and Long Short-Term Memory (LSTM)" (video)](https://youtu.be/WCUNPb-5EYI).

### *Parallel-RNN*

La arquitectura propuesta en el paper consiste en utilizar múltiples RNNs, una para cada aspecto o representación del item: ID, *thumbnail* (imagen) y/o descripción (texto). Luego, las capas ocultas de la arquitectura son combinaciones de las salidas de estas RNNs (con distintas configuraciones) para obtener un *score* que indica para un item que tan bueno sería siendo el siguiente en la secuencia/sesión.

> ![Arquitectura mostrda en el paper](/recsys/public/img/prrn-architecture.jpg)

En el paper se utilizan como *baseline* las arquitecturas comunmente utilizadas: solo ID, solo *features* y una concatenación de ambos como entrada del modelo. Las arquitecturas propuestas son 3:

* **Parallel**: Se entrena una red para cada representación y se utilizan sus *output* para obtener el *score*.
* **Parallel shared-W**: Similar a la arquitectura anterior, pero el *output* de cada red es multiplicado por una matriz para determinar el *score*.
* **Parallel interaction**: La capa oculta del primer modelo es una multiplicación elemento por elemento de los output del primero, lo que permite mezclar las *features* de las distintas representaciones de un item.

### Extracción de *features*

El elemento diferenciador del paper es que mezcla las distintas representaciones de los items para generar la recomendación y que utiliza esto en una red recurrente. Al trabajar con imágenes y texto es necesario utilizar procesamiento de imágenes y de lenguaje natural, lo que ha sido revisado por otros autores y que es solo utilizado en este paper.

En el caso de las imágenes, se utiliza una implementación pre-entrenada de GoogLeNet para extraer *features* de las imágenes. El modelo está bastante probado y destacó en 2014 por ser el ganador de la competencia ImageNet.

> ![Arquitectura de GoogLeNet](/recsys/public/img/googlenet-table.jpg)
>
> La tabla muestra la arquitectura de la instancia más exitosa mostrada en el paper "Going deeper with convolutions", la que resultó gandora en ImageNet 2014. Imagen: [Recorte de "Going deeper with convolutions"](https://arxiv.org/pdf/1409.4842.pdf).

En cuanto al procesamiento de texto, al ser descripciones cortas con distintos problemas (lenguaje y largo del mismo), los modelos que mejor funcionaron no eran técnicas de *deep learning* sino que TF-IDF y bag-of-words.

### Análisis de resultados

Para probar el modelo propuesto, los autores utilizaron su modelo sobre dos *dataset*:

* **VIDXL**: Datos de sesiones de un sitio similar a YouTube, acumulados a lo largo de 2 meses.
* **CLASS**: Datos de vistas a productos de un sitio de avisos clasificados.

Uno de los posibles problemas (análisis personal) de estos conjuntos de datos es que la nueva arquitectura utilizará como *ground truth* el *output* del algoritmo presente en la plataforma al momento de recolectar los datos. Si estoy recomendando con un algoritmo X y no funciona tan bien, es posible que ese "no tan bien" se refleje en los datos y sea el aprendido por el modelo propuesto. Fuera de esto, los autores comentan haber logrado mostrar que usar p-RNNs mejora el resultado alcanzable por RNNs (sobre IDs).

---

### Conclusión

Quedo con la duda sobre si el modelo se puede mejorar con un mejor dataset. Ojalá hubiera una forma de extraer las *features* a partir de los usuarios, lo que es bastante dificl al utilizar sesiones, pero me sigue haciendo ruido el que el *dataset* me parezca "algoritmo-dependiente". 

Encuentro que este paper es similar al que me tocó presentar en la semana de las presentaciones de *deep learning*, ya que en ese paper se utilizaba un modelo pre-entrenado para extraer *features* de imágenes y luego ese output era usado sobre un modelo ya diseñado, lo que hacía que el nuevo modelo fueran dos modelos "pegados". En este caso, se utilizan modelos existentes pero con un *twist*: se utilizan en paralelo, se exploraron distintas formas de utilizar en conjunto su *output* y distintas formas de entrenar el modelo. Creo que es bastante valioso porque no solo construye sobre modelos ya creados, sino que va más allá y propone una verdadera arquitectura en torno a estos modelos.

---

### Referencias

* [Hidasi, B., Quadrana, M., Karatzoglou, A., & Tikk, D. (2016). "Parallel recurrent neural network architectures for feature-rich session-based recommendations"](https://dl.acm.org/citation.cfm?id=2959167)

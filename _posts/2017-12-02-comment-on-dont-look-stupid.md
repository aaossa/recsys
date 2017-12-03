---
layout: post
title: Comentario sobre "Don't look stupid, avoiding pitfalls when recommending research papers" (2006) de Sean M. McNee, Nishikant Kapoor, and Joseph A. Konstan.
description: Como no caer en trampas (escrito por gente que cayo en ellas)
---

> Sean M. McNee, Nishikant Kapoor, and Joseph A. Konstan. (2006). "Don’t look stupid: avoiding pitfalls when recommending research papers". Disponible en: [dl.acm.org](https://dl.acm.org/citation.cfm?id=1180903)

---

En este paper, los autores comentan sobre las trampas (*pitfalls*) en que se puede caer a la hora de recomendar. Para esto, ejemplifican con un sistema recomendador de papers. No saber qué opciones darle al usuario, recomendar para la tarea incorrecta, o no generar recomendaciones atingentes son algunas de las trampas en que se puede caer. Los autores aseguran que diferentes algoritmos de recomendación, funcionan mejor para diferentes tareas, para lo que hacen un estudio de usuarios que les permita conocer sus apreciaciones.



### Recomendadores: visión desde el usuario

Primero que todo, este paper toma una perspectiva distinta a la usada por la mayoría de los otros artículos. Considera teoría de Interacción Humano-Recomendador (HRI) para establecer una visión centrada en el usuario de los aspectos que debe trabajar un buen sitema recomendador. Esto permite establecer un lenguaje común para el resto del paper:

> ![Aspectos de HRI](/recsys/public/img/stupid-hri.jpg)
>
> Aspectos de la interacción entre humano y recomendador. Imagen: Recorte del paper original



### Algoritmos usados

Los autores utilizan cuatro algoritmos para recomendar papers: 

* ***User-based Collaborative Filtering:*** Para predecir la opinión de un usuario, este modelo utiliza la opinión de usuarios similares. Los autores apuntan que el modelo es lento en correr, no hace pre-procesamiento y se espera que tenga una lata serendipidad. A pesar de esto, es un modelo ampliamente conocido y probado.
* ***Naïve Bayes Classifier:*** Modelo probabilistico que asume independencia entre las co-citaciones (supuesto MUY fuerte) para predecir la probabilidad de que un artículo sea co-citado con otros. También es un algoritmo conocido, que a pesar de recomendar rápido tiene un pre-procesamiento muy lento. Un aspecto negativo es que intenta predecir el siguiente item que recibirá una evaluación, lo que no se alinearía con lo que un usuario espera de un recomendador.
* ***Probabilistic Latent Semantic Indexing:*** PLSI es un algoritmo de reducción probabilistica con una fuerte base matemática, pero similar, en el fondo, al modelo anterior. Es muy rápido en recomendar, pero lento en pre-procesar. Generaría recomendaciones con alta serendipidad pero dentro de una clase latente.
* ***Content-based Filtering with TF/IDF:*** Este modelo incluye el contenido de los papers para representar los papers, lo que arrastraría los problemas de este tipo de modelos: es posible encontrar documentos similares en palabras, que no sean similares en contenido. A pesar de esto, se espera que genere recomendaciones con bastante similaridad entre sí.

Lo que no me gustó de este segmento es que ofrece una descripción que podría ser más clara si se usaran ecuaciones para explicar qué hace o qué varía cada modelo respecto a los demás. Me da la sensación de que las descripciones quedan "en el aire" si no se muestran con ecuaciones.



### Estudio con usuarios

En el experimento con usuarios se utilizaban parejas de recomendadores para que los usuarios pudieran compararlos directamente. Esto podría generar un poco de ruido en la evaluación de los usuarios, desde mi punto de vista, si es que el usuario no revisaba completamente las recomendaciones o si estas no estaban rankeadas de alguna forma (y si esto era explicitado o no a los usuarios), aunque no se me ocurre una mejor forma de haber diseñado el experimento. A pesar de esto, creo que el experimento estuvo bastante bien diseñado en cuanto a las preguntas, ya que permitían analizar las respuestas desde la visión de HRI planteada inicialmente. 



### Resultados

No hay que olvidar que, a pesar de que el paper utilizara modelos sobre un problema en particular, el paper no trata sobre el modelo o sobre la predicción o el dataset. El paper busca mostrar las trampas en que se puede caer porque ellos cayeron en estas. *Don't look stupid*:

* Bayes hizo recomendaciones similares para todos los usuarios
* PLSI hacía recomendaciones sin sentido
* El orden de las listas en el experimento influyó en las respuestas
* Distintas tareas dieron resultados distintos
* El dataset no estaba completo

Si bien algunas de estas trampas eran observables antes de la evaluación con usuarios, es dificil pensar que se podría estar cayendo en ellas. Ese es el punto del paper y creoque lo mostraron de forma magnífica. 



---

### Conclusión

Recomendar es dificil. Más aun si uno no se pone en el papel del usuario.



---

### Referencias

* [Sean M. McNee, Nishikant Kapoor, and Joseph A. Konstan. (2006). "Don’t look stupid: avoiding pitfalls when recommending research papers"](https://dl.acm.org/citation.cfm?id=1180903)


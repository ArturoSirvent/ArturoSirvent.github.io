---
title: "Cómo crear un asistente nutricional con IA (parte 1, estructura)"
date: 02/07/2024
tags: [data, blog,LLMs]
excerpt: "Asistente nutricional con IA"
mathjax: "true"

---  

Este post es el primero de varios en los que revisaremos la **implementación de un asistente conversacional** para realizar tareas que dependan de información real y actualizada procedente de una base de datos externa. 
En concreto, os mostraré las bases teóricas básicas, con las que creé un **asistente nutricional**. Este asistente nos ayuda a llevar un recuento aproximado de nuestras macros, unicamente **mediante intrucciones en lenguaje natural**, y pudiendo hacer indicaciones poco precisas como "un puñado", "un tazón", etc.

Ejemplo del resultado final:   
*gif*

En esta primera aproximación al problema, revisaremos como montar la estructura base del proyecto, para después darle progresivamente la funcionalidad completa. Estás serán las partes:  
1. Estructura y stack tecnológico.   👈 **Estás aquí**
2. Creación de agentes con langchain, RAG y self-querying.  
3. Integración con LangGraph y LangGraph Cloud.  
4. Revisión resultado final.  

Comencemos, revisando el primer punto de la lista, la "big picture", el flujo de funcionamiento:  

1. El usuario usa la app e informa al asistente nutricional de la cantidad de cada alimento alimentos. Además puede indicarle el momento de la ingesta. Mediante esto, el usuario tiene toda la flexibilidad del lenguaje para expresarse, de modo que se pueden usar expresiones como "un puñado", "medio vaso", etc. 
2. La consulta del usuario es procesada, las cantidades son identificadas y las indicadas en formato "no concreto", son traducidas a cantidades más concreta usando los estándars (contando con un cierto error). Por otro lado los ingredientes o comidas son identificadas. Si se indica una materia prima la identificación es más sencilla, si se trata de un plato preparado, se usarán los platos más similares en la base de datos.
3. Una vez se tienen identificados los alimentos, se obtiene de la base de datos nutricional, las informaciones necesarias, por ejemplo, cantidad de hidratos de carbono, proteinas y grasas, además de las kCal.  
4. Se realiza un cálculo y se devuelve la información nutricional de la ingesta. 
5. Por último, se le da al usuario la opción de guardar su información.  

![image](/images/ANutricional/flujo1.drawio_3.svg)    

Una vez tenemos la imagen a gran escala, debemos particularizar cada parte, cómo se va a abordar, en qué tiempos y usando qué tecnologías. Esto es el denominado "stack tecnológico":    

**Frontend (Interfaz mediante telegram)** 
Ciertamente no es la alternativa más comercial o personalizable en el aspecto visual si quisiéramos desarrolar una producto comercial, pero hemos hecho esta elección por la sorprendente sencillez que ofrece para servir una aplicación/modelo directamente al usuario en su dispositivo móvil, y como prueba de concepto funcionará perfectamente.   
Tenemos que entender este "bloque" como la conexión entre usuario y backend, nada más. Para ello usaremos la librería pyTelegramBotAPI.  

**Backend**  
Esto va a ser la maquinaria que le va a dar valor al proyecto, lo que hace que todo funcione por detrás, el código de la app.  
Aquí tendremos la gestion de usuarios, el sistema de NLU (natural language understanding), los modelos del lenguaje para generar la respuesta, los sistemas RAG (retrieval augmented generation) en caso de que tengamos que obtener datos extra de una base de datos por ejemplo, etc.   

**Base de datos**  
La base de datos dependerá de la aplicación que tenga nuestro programa. Si estamos tratando con archivos como .pdfs, o .docs, entonces tendremos que establecer un sistema de archivos como los "buckets" o el S3 de amazon. Si por el contrario, solo se trata de información estructurada, nos valdrá alguna base de datos SQL como un postgres. Y además de todo esto, si estamos montando un sistema RAG, también tendremos que añadir al "stack" una base de datos vectorial, para gestional correcta y eficientemente el contexto usado para las respuestas.   

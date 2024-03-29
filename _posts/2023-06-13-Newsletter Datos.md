---
title: "Rincon de las curiosidades (mayo 2023)"
date: 13/06/2023
tags: [data]
excerpt: "El funcionamiento de shazam"
mathjax: "true"

---

*Arturo Sirvent Fresneda*

Publicado originalmente en la [Newsletter: El rincón de los Datos](https://www.linkedin.com/pulse/el-rinc%2525C3%2525B3n-de-los-datos-datamecum%3FtrackingId=rF52m%252BrkTZWnRwcPm0g8gw%253D%253D/?trackingId=rF52m%2BrkTZWnRwcPm0g8gw%3D%3D)

-----
Este mes en el rincón de las curiosidades, veremos cómo una buena extracción de características y una organización inteligente de la base de datos pueden llegar a venderse por **400 millones de dólares**. Este es el caso del algoritmo de Shazam, la famosa aplicación para identificación de canciones.  
Si no la has usado nunca, el funcionamiento es muy sencillo: grabas con el móvil 5\~15 segundos de una canción, y el software te indica de qué canción se trata.  
Para entender el reto que supone **solo** la parte de encontrar una canción en la base de datos, pongámoslo con números. Si quisiéramos encontrar una grabación de 10 segundos (a 44.1kHz) en una base de datos de 1 millón de canciones (~ 3 minutos/canción), haciendo la comparación por fuerza bruta tardaríamos un promedio de ¡¡327 años!!  
  
Como queremos que sea breve y simple, voy a exponer una analogía, sin embargo aquí se puede encontrar el paper original.  
Supongamos que queremos encontrar un recorte de una imagen mucho más compleja (esto sería análogo a nuestra búsqueda de los 10 segundos en la base de datos):  
![image](/images/shazam/escena_Wally_sleepydays2.jpg)   
Una buena forma de proceder sería simplificar la búsqueda mediante **índices**. Estos índices los calcularemos usando una extracción de características de cada recorte de imágenes. Para este ejemplo hemos escogido como característica, el número de elementos con tono amarillo:  
![image](/images/shazam/escena_Wally_sleepydays_amarillo2_2.png)   
Esto logrará una subdivisión que simplificará mucho futuras búsquedas. De modo que cuando tengamos que identificar un nuevo segmento, podremos ir directamente a buscar al grupo con el mismo número de zonas amarillentas.  
![image](/images/shazam/Pasted_image_20230526124031.png)    
  
En este rincón hemos aprendido sobre el concepto de indexación en bases de datos y la extracción de características para ello.  
En concreto, la extracción de características que hace el algortimos de Shazam es una selección local (sobre el espectrograma) de las frecuencias predominantes en las grabaciones. Dichas frecuencias predominantes se agrupan en pares, y los índices de búsqueda se calculan aplicando una función hash a la tríada de valores: frecuencia 1, frecuencia 2 y la separación temporal entre ellas. Esto logra que las comparaciones sean muy efectivas y rápidas para la identificación.  
  
Con este ejemplo espero que también se deje entrever, que no siempre hace falta una inteligencia artificial hecha de redes neuronales super complejas y extensas para resolver un problema. A veces pensando un poco, se puede encontrar una solución elegante a un problema complicado.

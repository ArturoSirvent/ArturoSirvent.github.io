---
title: "La hipótesis del Cerebro Bayesiano"
date: 06/10/2023
tags: [stats,ontologia]
excerpt: "Cerebro Bayesiano"
mathjax: "true"

---
*Arturo Sirvent Fresneda*

-----

Este mes en el rincón de las curiosidades nos vamos a poner un poco metafísico para hablar de un enfoque muy interesante sobre los modelos predictivos, en concreto, de la Hipótesis del Cerebro Bayesiano.  
Esta hipótesis comienza estableciendo que por mera selección evolutiva, el cerebro se ha ido optimizando para ser bueno prediciendo su entorno, pues aquellos capaces, serán los que más probabilidades tengan de sobrevivir y transferir sus genes. Y es en esta modelización del mundo donde entra en juego la estadística bayesiana.  
Para entenderlo un poco mejor, hagamos un breve inciso sobre como funciona esta interpretación de la estadística. La estadística bayesiana (a diferencia de otras interpretaciones como la frecuentista) trabaja con "grados de creencia", que tan probable es un suceso. Y esto lo podemos complicar todo lo que queramos, empezando por: "si ocurre esto, ¿Qué tan probable es esto otro?", o "¿en que grado A influencia a B?"   
Esto abarca una rama completa de la estadística, y han demostrado ser sorprendentemente efectivas en modelos de Machine Learning.  
Para relacionar esto con el cerebro, pensemos en la probabilidad condicional que mencionaba. Cuando observamos evidencias/estímulos de un hecho, actualizamos nuestras creencias sobre la probabilidad de este, de manera que la llamada probabilidad "prior" se ve actualizada tras recibir un estimulo, y obtenemos la llamada probabilidad "posterior".  Por ejemplo, no nos planteamos que va a llover (hecho) hasta que vemos un cielo nublado (evidencia).    
La Hipótesis del Cerebro Bayesiano, va muy de la mano del dualismo de Kant, donde un mundo interno (nuestra percepción del mundo), y un mundo externo (lo que sea que haya ahí fuera), tienen que comunicarse por medio de una interfaz, que serían nuestros sentidos. Y este modelado del mundo exterior se produce gracias a estadística condicional Bayesiana (más concretamente propone *modelos bayesianos jerárquicos*), por ejemplo: Evidencia 1 + Evidencia 2 + Evidencia 3 + ... = probabilidad de X suceso.  
Viéndolo de esta manera, no es inusual que los modelos de Naïve Bayes se hayan usado tanto durante tanto tiempo, según esta hipótesis, los podríamos hasta clasificar de "bioinspirados" (aunque recordemos que estamos en un área casi filosófica). 
Al igual que un modelo entrena, nuestro cerebro optimiza las decisiones tomadas para que los errores cometidos en la interfaz: mundo interior vs. mundo exterior, sean mínimas.  De esta manera tan lógica, también podemos explicar los sesgos cognitivos y conductuales que observamos en la sociedad, si una persona ha recibido X impulsos en su interfaz con el mundo (sus sentidos), pues su modelo interno del mundo habrá sido optimizado acorde.   

![image](/images/BYB/BayesianBrain.png)    

Para terminar, es interesante reflexionar hasta que punto los modelos que construimos en Machine Learning pueden llegar a resolver el problema que planteamos, y al abordar un problema nuevo, cabe preguntarse: ¿es esa interfaz lo suficientemente detallada (tienen nuestros datos la precisión necesaria)?, ¿le estamos danto al modelo estímulos relevantes (esta la información importante para resolver el problema, codificada en los datos que usamos)?

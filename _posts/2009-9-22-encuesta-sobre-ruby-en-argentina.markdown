--- 
layout: post
title: Encuesta sobre Ruby en Argentina usando Google Forms
---
Hace unas semanas, usando "Google Forms":http://docs.google.com, creé una encuesta que intentaba responder ciertas preguntas básicas respecto a "nuestra comunidad":http://www.rubyargentina.com.ar/. La idea era entender un poco mejor quienes eramos y qué queríamos. En un tiro la creé, y pasé a anunciarla en la "Lista de Correo de Ruby Argentina":http://rubyargentina.soveran.com/signup

El resultado de la misma se encuetra publicado aquí: 

* "Encuesta v0.1":http://www.lucasefe.com.ar/encuesta-0.1.html

A la semana siguiente, tomando un poco del feedback que me habían pasado, construí de la misma forma la versión 0.2. Esta incluía un montón de preguntas extra referidas a carga horaria, salario y expectativas, además de uno que otro dato regional. Los resultados fueron interesantes, pero cometí varios errores (por calentón) con respecto a Google Forms. 

Google Forms (GF) está muy bien cómo herramienta rápida de contrucción de formularios, pero no te permite modificar, o vaciar el form de una manera simple. Hay que tener muy claro el tipo de respuesta que se espera de cada pregunta, como para que el resultado sea representativo. 

Ejemplo: GF te genera gráficas automáticamente de cada un de las preguntas, pero solo si *no* se trata de preguntas de texto libre. Bien, yo cometí el error de preguntar el salario de esa forma, así que la gráfica que se generó inicialmente no servía de nada (4500$ 900U$$ ... ). Lo mismo me sucedió con las ciudades de origen. Finalmente lo pude corregir, pero hacerlo fue un parto. 

Ah, los resultados de la segunda encuesta se encuentran aquí:

* "Encuesta v0.2":http://www.lucasefe.com.ar/encuesta-0.2.html

Espero que les sirva y provea de información útil para hacer crecer a Ruby en Argentina. 

Y recuerden: Si usan Google Forms, verifiquen una y mil veces con casos de prueba si están obteniendo el resultado gráfico que esperaban.

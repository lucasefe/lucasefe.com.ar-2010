--- 
layout: post
title: Encuesta sobre Ruby en Argentina usando Google Forms
---
Hace unas semanas, usando "Google Forms":http://docs.google.com, cre� una encuesta que intentaba responder ciertas preguntas b�sicas respecto a "nuestra comunidad":http://www.rubyargentina.com.ar/. La idea era entender un poco mejor quienes eramos y qu� quer�amos. En un tiro la cre�, y pas� a anunciarla en la "Lista de Correo de Ruby Argentina":http://rubyargentina.soveran.com/signup

El resultado de la misma se encuetra publicado aqu�: 

* "Encuesta v0.1":http://www.lucasefe.com.ar/encuesta-0.1.html

A la semana siguiente, tomando un poco del feedback que me hab�an pasado, constru� de la misma forma la versi�n 0.2. Esta inclu�a un mont�n de preguntas extra referidas a carga horaria, salario y expectativas, adem�s de uno que otro dato regional. Los resultados fueron interesantes, pero comet� varios errores (por calent�n) con respecto a Google Forms. 

Google Forms (GF) est� muy bien c�mo herramienta r�pida de contrucci�n de formularios, pero no te permite modificar, o vaciar el form de una manera simple. Hay que tener muy claro el tipo de respuesta que se espera de cada pregunta, como para que el resultado sea representativo. 

Ejemplo: GF te genera gr�ficas autom�ticamente de cada un de las preguntas, pero solo si *no* se trata de preguntas de texto libre. Bien, yo comet� el error de preguntar el salario de esa forma, as� que la gr�fica que se gener� inicialmente no serv�a de nada (4500$ 900U$$ ... ). Lo mismo me sucedi� con las ciudades de origen. Finalmente lo pude corregir, pero hacerlo fue un parto. 

Ah, los resultados de la segunda encuesta se encuentran aqu�:

* "Encuesta v0.2":http://www.lucasefe.com.ar/encuesta-0.2.html

Espero que les sirva y provea de informaci�n �til para hacer crecer a Ruby en Argentina. 

Y recuerden: Si usan Google Forms, verifiquen una y mil veces con casos de prueba si est�n obteniendo el resultado gr�fico que esperaban.

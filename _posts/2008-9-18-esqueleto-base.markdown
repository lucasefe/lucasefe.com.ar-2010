--- 
layout: post
title: Esqueleto Base para aplicaciones Rails
---
¿Quién no se puso alguna vez a armar una aplicación de cero y repitió una y otra vez los clásicos pasos de agregar los plugins típicos, más los toques personales? Yo lo hago siempre, y justo ayer me puse a pensar en que ya era hora de solucionarlo. Me estaba por poner y dí con este proyecto en github, gracias a los muchachos de RailsEnvy. 

Es simplemente un proyecto pre-armado. Me gustó bastante lo que incluye. Quizás le agregaría "Paperclip":http://github.com/thoughtbot/paperclip/tree/master y "Factory Girl":http://github.com/thoughtbot/factory_girl/tree/master, pero por ahora está bien. 

http://github.com/fudgestudios/bort/tree/master

La lista completo de lo que le puso el flaco que construyó el proyecto es la siguiente:

* Acts As State Machine
* Asset Packager
* Restful Authentication + Forgot Password (a este no lo conocía)
* Exception Notification (no muy necesario si se está usando "Hoptoad":http://www.hoptoadapp.com/)
* Rspec & RspecRails
* Will Paginate
* Role Requirement (para el manejo de roles, muy práctico a decir verdad)

Mi recomendación es hacerse un fork en tu propio perfil de github (si lo estás usando, obviamente) y clonar ese proyecto. Así si le hacés algún agregado particular, lo podés persistir para no tener que hacerlo en el siguiente proyecto. 

El mio quedó "acá":http://github.com/lucasefe/bort/tree/master, ojo, no tiene nada nuevo. Seguro que en un rato le agrego lo que puse arriba. 

Fuente: "RailsEnvy":http://www.railsenvy.com/

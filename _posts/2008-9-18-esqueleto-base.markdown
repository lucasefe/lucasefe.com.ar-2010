--- 
layout: post
title: Esqueleto Base para aplicaciones Rails
---
�Qui�n no se puso alguna vez a armar una aplicaci�n de cero y repiti� una y otra vez los cl�sicos pasos de agregar los plugins t�picos, m�s los toques personales? Yo lo hago siempre, y justo ayer me puse a pensar en que ya era hora de solucionarlo. Me estaba por poner y d� con este proyecto en github, gracias a los muchachos de RailsEnvy. 

Es simplemente un proyecto pre-armado. Me gust� bastante lo que incluye. Quiz�s le agregar�a "Paperclip":http://github.com/thoughtbot/paperclip/tree/master y "Factory Girl":http://github.com/thoughtbot/factory_girl/tree/master, pero por ahora est� bien. 

http://github.com/fudgestudios/bort/tree/master

La lista completo de lo que le puso el flaco que construy� el proyecto es la siguiente:

* Acts As State Machine
* Asset Packager
* Restful Authentication + Forgot Password (a este no lo conoc�a)
* Exception Notification (no muy necesario si se est� usando "Hoptoad":http://www.hoptoadapp.com/)
* Rspec & RspecRails
* Will Paginate
* Role Requirement (para el manejo de roles, muy pr�ctico a decir verdad)

Mi recomendaci�n es hacerse un fork en tu propio perfil de github (si lo est�s usando, obviamente) y clonar ese proyecto. As� si le hac�s alg�n agregado particular, lo pod�s persistir para no tener que hacerlo en el siguiente proyecto. 

El mio qued� "ac�":http://github.com/lucasefe/bort/tree/master, ojo, no tiene nada nuevo. Seguro que en un rato le agrego lo que puse arriba. 

Fuente: "RailsEnvy":http://www.railsenvy.com/

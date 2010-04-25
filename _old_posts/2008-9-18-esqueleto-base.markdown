--- 
layout: post
title: Esqueleto Base para aplicaciones Rails
---
¿Qui&eacute;n no se puso alguna vez a armar una aplicaci&oacute;n de cero y repiti&oacute; una y otra vez los cl&aacute;sicos pasos de agregar los plugins t&iacute;picos, m&aacute;s los toques personales? Yo lo hago siempre, y justo ayer me puse a pensar en que ya era hora de solucionarlo. Me estaba por poner y d&iacute; con este proyecto en github, gracias a los muchachos de RailsEnvy. 

Es simplemente un proyecto pre-armado. Me gust&oacute; bastante lo que incluye. Quiz&aacute;s le agregar&iacute;a "Paperclip":http://github.com/thoughtbot/paperclip/tree/master y "Factory Girl":http://github.com/thoughtbot/factory_girl/tree/master, pero por ahora est&aacute; bien. 

http://github.com/fudgestudios/bort/tree/master

La lista completo de lo que le puso el flaco que construy&oacute; el proyecto es la siguiente:

* Acts As State Machine
* Asset Packager
* Restful Authentication + Forgot Password (a este no lo conoc&iacute;a)
* Exception Notification (no muy necesario si se est&aacute; usando "Hoptoad":http://www.hoptoadapp.com/)
* Rspec & RspecRails
* Will Paginate
* Role Requirement (para el manejo de roles, muy pr&aacute;ctico a decir verdad)

Mi recomendaci&oacute;n es hacerse un fork en tu propio perfil de github (si lo est&aacute;s usando, obviamente) y clonar ese proyecto. As&iacute; si le hac&eacute;s alg&uacute;n agregado particular, lo pod&eacute;s persistir para no tener que hacerlo en el siguiente proyecto. 

El mio qued&oacute; "ac&aacute;":http://github.com/lucasefe/bort/tree/master, ojo, no tiene nada nuevo. Seguro que en un rato le agrego lo que puse arriba. 

Fuente: "RailsEnvy":http://www.railsenvy.com/

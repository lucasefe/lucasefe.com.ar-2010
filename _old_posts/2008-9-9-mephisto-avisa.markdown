--- 
layout: post
title: Mephisto, avis&aacute;!
---
Estuve luchando un buen rato con esto. Instal� Mephisto, configur� la base de datos, mod_rails, y luego habilit� Multi Site. Hasta ah�, todo perfecto. 

Agregu� el segundo sitio, que era www.algunsitio.com, pero no me lo detectaba. Iba de una al primero. Cuando cre� el sitio lo hice desde el backend (/admin) y desde la consola (Site.create :host => "www.algunsitio.com"....) pero nada lo solucionaba. Siempre terminaba yendo al sitio default, que es el primero. 

Soluci�n? No declarar el sitio con el www, porque Mephisto se lo remueve si comienza con esas m�gicas 3 letras. 

O sea... no usar como host (cuando se lo crea) *www.algunsitio.com*, sino *algunsitio.com*. Mephisto solito le agrega el www. 

_Ay, dios... costaba tanto poner una validaci�n para eso?_

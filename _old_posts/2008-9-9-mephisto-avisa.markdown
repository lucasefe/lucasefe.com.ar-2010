--- 
layout: post
title: Mephisto, avis&aacute;!
---
Estuve luchando un buen rato con esto. Instal&eacute; Mephisto, configur&eacute; la base de datos, mod_rails, y luego habilit&eacute; Multi Site. Hasta ah&iacute;, todo perfecto. 

Agregu&eacute; el segundo sitio, que era www.algunsitio.com, pero no me lo detectaba. Iba de una al primero. Cuando cre&eacute; el sitio lo hice desde el backend (/admin) y desde la consola (Site.create :host => "www.algunsitio.com"....) pero nada lo solucionaba. Siempre terminaba yendo al sitio default, que es el primero. 

Soluci&oacute;n? No declarar el sitio con el www, porque Mephisto se lo remueve si comienza con esas m&aacute;gicas 3 letras. 

O sea... no usar como host (cuando se lo crea) *www.algunsitio.com*, sino *algunsitio.com*. Mephisto solito le agrega el www. 

_Ay, dios... costaba tanto poner una validaci&oacute;n para eso?_

Habitualment, tot servidor en Simatic NET té instal·lat un **Program Manager** que es diu _Communication Settings_.  
Es poden reiniciar sense problema els serveis del Simatic; fins i tot si el sistema queda corrupte, tenen un _backup_ del mapejat del PLC en un fitxer **.ati**.

![[Pasted image 20251117084411.png]]

Si en reiniciar des del menú de configuració el servidor no aplica els canvis, cal matar el procés específic del servidor, **no** només reiniciar els serveis:

![[Pasted image 20251117084611.png]]

Tot l'aplicatiu funciona a partir de múltiples servidors amb els seus respectius processos i un procés “pare”, que és el de dalt:

![[Pasted image 20251117084748.png]]

Pel que vaig entendre, sempre que el procés pare funcioni (o falli), els serveis fills es queden en una mena de _deadlock_ i cal matar-los a nivell de procés.
#Práctica 3. Balanceo de Carga
##Jose Antonio Plata Muñoz


***1El servidor web nginx*** 

Instalación:


![](http://i.imgur.com/4Kexzvy.png)

Configuración:

![](http://i.imgur.com/GH6v5rn.png)



Probando el balanceo:

Desde mi servidor apache B, he hecho un curl al balanceador y vemos como una vez nos manda a la máquina 1 y otra vez nos manda a la máquina 2 (desactivé el crontab previamente para ver que funciona todo correctamente):

![](http://i.imgur.com/QM1sivi.png)


Aquí podemos ver como funciona si le damos el doble de prioridad a la máquina:

![](http://i.imgur.com/w0Pgp8C.png)


Ahora hemos probado a instalar Haproxy en el balanceador, previamente parando el sevicio nginx.

![](http://i.imgur.com/VwECSrk.png)

![](http://i.imgur.com/lIViFXZ.png)


Y aquí comprobamos como funciona bien, al igual que Nginx:


![](http://i.imgur.com/ASxMim6.png)





#Práctica 2
##Jose Antonio Plata Muñoz

***1. Probar el funcionamiento de la copia de archivos por ssh***

Podemos como desde nuestro Server14 ejecutamos el comando para comprimirlo y mandarlo mediante ssh. En el Server14B podemos ver como está nuestro archivo .tar


 ![](http://i.imgur.com/s37Rqzd.png)


***2. Clonado de una carpeta entre las dos máquinas***

Vemos como en nuestro Server14B (derecha), en un principio no hay nada y posteriormente se encuentra todo el contenido de /var/www de Server14. Cuando automaticemos el proceso, añadiremos mas opciones a rsync para que sea mas "real" el caso.

![](http://i.imgur.com/dqGdRTP.png)

***3. Configuración de ssh para acceder sin que solicite contraseña***

Podemos ver como en Server14B, al conectarnos a Server14 no nos ha pedido la contraseña.

![](http://i.imgur.com/aG8gYok.png)

Aquí accedemos como root. He tenido problemas a la hora de acceder como root, ya que me rechazaba el acceso. Para solucionarlo, he ido al archivo "/etc/ssh/sshd_config" y en la línea que pone "PermitRootLogin" puse el valor "yes". Después de hacer eso hay que hacer un restart al ssh. (service ssh restart)


![](http://i.imgur.com/iyDQBd4.png)


***4. Establecer una tarea en cron que se ejecute cada hora para mantener actualizado el contenido del directorio /var/www entre las dos máquinas***


Podemos ver que no hay nada en la carpeta /var/www de Server14B:

![](http://i.imgur.com/8hg0iZr.png)

Obsérvese la hora.

Añadimos al crontab la línea para que se actualice:

![](http://i.imgur.com/84U1i37.png)

Ahora vemos como (llegando el momento, cualquier hora a las 23 minutos) se ha copiado lo que contenia la carpeta /var/www de Server14.


![](http://i.imgur.com/R6SOsYR.png)





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




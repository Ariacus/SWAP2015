Cristina Rosillo Arenas
Jose Antonio Plata Muñoz

#Práctica 6

- **Creación de dos discos duros**

El primer paso será crear dos discos duros de las mismas características (tamaño etc), en nuestro caso los hemos llamado RAID1_0 Y RAID1_1.

![captura1_0](http://i.imgur.com/5AmgBwO.png)

Una vez añadidos a nuestra máquina, la arrancamos y procederemos a configurar el funcionamiento de estos dos discos como RAID 1.

- **Configuración como RAID 1**

Instalaremos en la máquina el software necesario para hacerlo, ejecutando la siguiente instrucción.

![captura2_0](http://i.imgur.com/kayhwxg.png)

A continuación buscaremos la identificación que ha asignado linux a cada disco.

	> fdisk -l

![captura3_0](http://i.imgur.com/Gk4Hk1t.png)

Ya podemos crear el RAID1_0 :

![captura4_0](http://i.imgur.com/TwojKbg.png)

Le damos formato al dispositivo RAID que acabamos de crear.

![captura5_0](http://i.imgur.com/DILD8pc.png)

Creamos el directorio en el que montaremos la unidad RAID.

![captura6_0](http://i.imgur.com/WQBBao9.png)

Para comprobar el estado en el que se encuentra el RAID podemos ejecutar:

	> mdadm detail /dev/md0

![captura7_0](http://i.imgur.com/fRrv9mF.png)

Por último configuraremos el sistema para que  que monte el dispositivo RAID al arrancar el sistema.
Para ello hemos añadido al ficher /etc/fstab la última línea que podemos ver en la siguiente imagen.

![captura8_0](http://i.imgur.com/XBJxQSQ.png)

- **Simulando fallos con MDADM**

Para comprobar el correcto funcionamiento de nuestro RAID1 vamos a simular un fallo mediante mdadm,
retirarlo y comprobar que efectivamente se puede seguir accediendo a los datos.

Para simular el fallo en el disco sdc en /dev/md0 ejecutaremos:

	> mdadm --manage --set-faulty /dev/md0 /dev/sdc

![captura9_0](http://i.imgur.com/4WpNQfX.png)

Ahora veremos como el disco efectivamente ha fallado escribiendo:

	mdadm --detail /dev/md0

![captura10_0](http://i.imgur.com/xJxKdeA.png)

Ahora lo quitaremos y comprobaremos que podemos acceder a los datos.

![captura11_0](http://i.imgur.com/IA8IX3G.png)

![captura12_0](http://i.imgur.com/NZwW5W0.png)

Como podemos observar hemos quitado el disco y podemos aun así podemos acceder a los datos de forma correcta. A continuación
volveremos a añadir nuestro disco al RAID.

![captura 13_0](http://i.imgur.com/T9wj0Bs.png)

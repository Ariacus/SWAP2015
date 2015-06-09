#Práctica 5

Jose Antonio Plata Muñoz
Cristina Rosillo Arenas

- **Creación de una pequeña base de datos e inserción de datos**

El primer paso que daremos será crear una base de datos con una tabla, a la que añadiremos algunos
valores. Nos vamos a nuestro servidor principal (Máquina 0) y desde consola ejecutaremos los siguientes
comandos.

	> mysql -u root -p
	mysql> create database contactos;
	mysql> use contactos;
	mysql> create table datos(nombre varchar(100), tlf int);

Ya tenemos creada nuestra base de datos y una tabla, ahora añadiremos valores a la tabla de la siguiente
forma.

	mysql> insert into datos(nombre, tlf) values ("pepe", 958349871);
	mysql> insert into datos(nombre, tlf) values ("ana", 958222222);
	...

De forma que al final tendremos una tabla de éste estilo.

![captura1_0](http://i.imgur.com/SvUarvD.png)

- **Copia de seguridad de la Base de Datos con mysqldump**

Ahora realizaremos una copia de seguridad de nuestra base de datos, desde la misma máquina (Máquina 0)
ejecutamos el comando mysqldump.

Pero antes debemos tener en cuenta que al momento de realizar la copia se pueden estar realizando inserciones,
modificaciones, etc. Por lo que deberíamos impedir que se realizasen cambios en ella antes de hacer la copia.
Para ello antes de ejecutar la instrucción anterior, escribiremos:

	mysql> FLUSH TABLES WITH READ LOCK;

Y ya podemos realizar la copia.

![captura2_1](http://i.imgur.com/b5pWw81.png)

Una vez hecha debemos volver a permitir los cambios.

	mysql> UNLOCK TABLES;

De forma que se nos creará en el directorio /root/ un fichero .sql que contendrá toda la información de
nuestra base de datos y que nos servirá para hacer restauraciones.

- **Restaurar copia de seguridad en la segunda máquina**

 Teniendo ya nuestro fichero .sql lo copiaremos a la segunda máquina. Nos vamos al segundo servidor (Máquina 1) y ejecutamos:

![captura2_2](http://i.imgur.com/mwXnGeP.png)

Comprobamos que efectivamente el fichero se encuentra en /root/ y restauramos la copia como muestra la siguiente
imagen. Es importante para poder realizar la restauración de forma correcta, tener creada previamente la base de datos.

![captura2_3](http://i.imgur.com/PnwCT0k.png)

Entramos en mysql y vemos que efectivamente la tabla y los valores que definimos en la máquina 0 se encuentran ya en nuestra 
máquina 1.

![captura2_4](http://i.imgur.com/usZ0pWv.png)


- **Configuración maestro-esclavo de los servidores MySQL**

Antes de comenzar la configuración debemos comprobar que los servicios MySQL de ambos servidores sena versiones
similares, para prevenir posibles conflictos. Podemos hacerlo ejecutando:

	> mysql --version

Una vez comprobado que son la misma versión, empezaremos a editar el fichero de configuración de mysql "/etc/mysql/my.cnf"
de nuestra máquina 0 que en éste caso será el maestro.

Comentaremos el parámetro: #bind-address 127.0.0.1

Modificamos el valor del parámetro: server-id = 1

Y reiniciamos el servicio.

![captura3_1](http://i.imgur.com/xR7ZEPN.png)

A continuación nos vamos a la segunda máquina (máquina 1) y editamos el mismo fichero de forma similar a la enterior.

Modificamos el valor del parámetro: server-id = 2

Y reiniciamos el servicio.

![captura3_2](http://i.imgur.com/Db38qNg.png)

Ahora volvemos a nuestro servidor principal y crearemos un usuario con permisos de acceso. Ejecutamos las siguientes
instrucciones.

![captura3_3](http://i.imgur.com/7XOzzej.png)

Seguidamente vamos a nuestro servidor esclavo (Máquina 1) para configurar en ella los datos del maestro. Accedemos a 
la consola mysql y paramos al esclavo antes de poder configurar la información del maestro¹.
Ejecutaremos las siguientes instrucciones en orden:
	
	mysql> STOP SLAVE;
	
![captura3_4](http://i.imgur.com/hm29a7S.png) 

	mysql> START SLAVE;

Por último nos quedaría desbloquear las tablas del maestro para poder volver a realizar cambios. En la máquina 0 escribimos:

	mysql> UNLOCK TABLES;

Y para comprobar que todo funciona de forma correcta y que no existe ningún problema, desde la máquina esclavo
(máquina 1) ejecutamos:

	mysql> SHOW SLAVE STATUS\G;

Si el valor de la variable Seconds_Behind_Master es distinto de NULL significaría que todo está correcto.

![captura3_5](http://i.imgur.com/m5U6fno.png)

Ahora sí, para terminar insertaremos un nuevo registro en la tabla datos de nuestro servidor principal y comprobaremos 
como efectivamente esa inserción también nos aparece en la tabla datos de nuestro esclavo.

![captura3_6](http://i.imgur.com/jPdXcAV.png)


¹: En ésta captura existe una pequeña errata en el parámetro MASTER_LOG_FILE, el valor correcto es: MASTER_LOG_FILE='bin.000001'.

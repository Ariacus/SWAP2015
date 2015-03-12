Ejercicio T2.1: Calcular la disponibilidad del sistema descrito en edgeblog.net si tenemos dos réplicas de cada elemento salvo para el centro de datos (en total 3 elementos en cada subsistema).


	Partimos del caso hecho en que replicamos dos veces cada elemento, nos queda la siguiente tabla:

	Web 97.75%
	Application 99%
	Database 99.9999%
	DNS 99.96%
	Firewall 97.75%
	Switch 99.99%
	Data Center 99.99%
	ISP 99.75%

	Replicamos cada uno de ellos nuevamente:

	Web: 0.9775 + (1-0.9775)*0.85 = 99.6625%
	Application: 0.99 + (1-0.99)*0.9 = 99.9%
	Database: 0.999999 + (1-0.999999)*0.999= 99.999999999% (no tiene mucho sentido replicar el servidor de bases de datos de nuevo)
	DNS: 0.9996 + (1-0.9996)*0.98 = 99.9992%
	Firewall: 0.9775 + (1-0.9775)*0.85 = 99.6625%
	Switch: 0.9999 + (1-0.9999)*0.99= 99.9999%
	ISP: 0.9975 + (1-0.9975)*0.95= 99.9875%

	Ahora tenemos una disponibilidad de:

	99.6625%+99.9%+99.999999999%+99.9992%+99.6625%+99.6625%+99.9875%+99.99%(data center) = 99.2037%

	Hemos pasado de un 94.35% duplicando dos veces cada elemento, a un 99.2037% duplicando tres veces cada elemento (excepto el data center)


Ejercicio T2.2: Buscar frameworks y librerías para diferentes lenguajes que permitan hacer aplicaciones altamente disponibles con relativa facilidad. Como ejemplo, examina PM2: https://github.com/Unitech/pm2 que sirve para administrar clústeres de NodeJS.


	-Kumbia Enterprise FrameWork: es un framework para php (un fork de KumbiaPHP), una de sus bazas es el uso de componentes ACL lo que permite controlar el flujo del tráfico en equipos de redes, lo que nos permite filtrar el tráfico de nuestro servidor.

	-Zope: funciona sobre Python y nos permite una alta disponibilidad a través de balanceadores de carga, servidores de cacheo web y replicación de bases de datos.

	-Node-forever: he visto que en algunos casos es comparado con PM2, es un CLI, sin embargo, no he sido capaz de encontrar algo que me permita ver claramente como nos puede ayudar para mejorar la disponibilidad.


Ejercicio T2.3: ¿Cómo analizar el nivel de carga de cada uno de los subsistemas en el servidor? Buscar herramientas y aprender a usarlas.

	-Web Page Test: con esta herramienta ( que he utilizado alguna vez), a pesar de que no mide directamente la carga de ningún sistema, si que nos permite detectar cuellos de botella en nuestra web. Mas que a nivel del alojamiento, a nivel de la propia web. Por ejemplo divide el resultado en muchas pequeñas cargas parciales como por ejemplo: el tiempo que tarda el texto de la página, las imágenes, hojas CSS, etc. Así por ejemplo podríamos comprobar que nuestra web tarda mucho en cargar las imágenes porque son muy grandes.

	-Loadimpact: con esta herramienta podemos comprobar cuantos usuarios simultáneos soporta nuestro alojamiento web. Es una herramienta super fácil de utilizar y rápida. Y los gráficos son bastante intuitivos.

	-Nsasoft Network Traffic Emulator: esta herramienta nos permite generar tráfico IP / ICMP /TCP /UDP. Lo que nos va a permitir testear nuestro servidor de Firewall. La interfaz es bastante sencilla y no es complicado de manejar. Nos permite también testear servidores.

	-DBMonster: herramienta que nos permite realizar test de stress a las bases de datos, es multiplataforma y funciona con PostgreSQL, MySQL, Oracle, HSQLDB, MSSQL y en resumen con cualquier base de datos que tenga drivers JDBC. 

	-DNSPerf: esta herramienta nos permite realizar pruebas de carga a servidores DNS. Lo que hace básicamente es simular tráfico DNS y reportar información relativa al número de consultas completadas, fallidas, latencia, códigos de respuesta, etc. Un tutorial bastante interesante que utilicé para su instalación y uso:

	http://rm-rf.es/pruebas-de-estres-de-dns-con-dnsperf-y-resperf/



Ejercicio T2.4: En este ejercicio debemos buscar diferentes tipos de productos: (1) Buscar ejemplos de balanceadores software y hardware (productos comerciales). (2) Buscar productos comerciales para servidores de aplicaciones. (3) Buscar productos comerciales para servidores de almacenamiento.


	1.1 Balanceadores Software:

		-VLM-200: el mas pequeño de su familia, el cual podemos adquirir en Amazon por el módico precio de $1,976.40. (el mas potente, VLM-10G sale por unos $22.000)
		-Si necesitamos algo mas económico podemos utilizar Linux Virtual Server (LVS), aunque obviamente las prestaciones no son las mismas y todo dependerá de lo que necesitemos.

	1.2 Balanceadores Hardware:

		-LM-2600 : en amazon su precio es de $6,835.85 y es capaz de soportar 2.000 transacciones SSL/segundo, 1.000 servidores soportados, 69.000 solicitudes HTTP/segundo.

		Utilizar balanceadores hardware en redes pequeñas no es rentable.

	
	2.1 Servidores de Aplicaciones:

		-Oracle GlassFish Server
		-WebLogic Server
		-WebSphere Application Server
		-Azure
		
	2.2 Servidores de Almacenamiento:

		-Dell PowerVault RD1000 con 2 cartuchos hasta 320GB por 359€
		-Dell PowerVault PV110T Tape Drive con 5 cartuchos de 400GB por 1859€
		-Servidor NAS Synology DS115j acepta hasta 1 HD de hasta 6TB por 92€ (opción económica)
















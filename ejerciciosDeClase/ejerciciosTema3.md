***Ejercicio T3.1:
Buscar con qué órdenes de terminal o herramientas gráficas podemos configurar bajo Windows y bajo Linux el enrutamiento del tráfico de un servidor para pasar el tráfico desde una subred a otra.***

Para activar el enrutamiento en un sistema Linux, tan solo basta con poner a '1' la variable ip_forward del sistema, es decir, basta con ejecutar desde una consola de root:


sudo echo "1" > /proc/sys/net/ipv4/ip_forward

El problema es que de esta forma, cada vez que reiniciamos el equipo se "resetea" el valor del ip_forward. Para hacerlo de manera permanente tendríamos que editar el fichero /etc/sysctl.conf y "descomentar" la línea: # net.ipv4.ip_forward=1

Posteriormente tendríamos que configurar el filtrado para que acepte el redireccionamiento de paquetes desde dentro hacia fuera de nuestra red y mediante NAT permita que los PCs de la red interna naveguen con la dirección IP 'publica' del servidor. 

Según encontré la configuración puede ser bastante compleja. No conseguí hacerlo bien, pero utilicé la siguiente fuente.

http://www.ite.educacion.es/formacion/materiales/85/cd/linux/m6/enrutamiento_en_linux.html


En Windows Server, existe un servicio llamado "Servicio de enrutamiento y acceso remoto". Para instalarlo, nos iremos en ventana principal, "Agregar funciones". 

O en tareas de configuración inicial -> Personalizar este servidor -> Agregar funciones. Luego en la lista de funciones de servidor, seleccionamos "Servicios de Acceso y directivas de Redes". 
Cuando estemos en la lista de servicios de función, seleccionaremos Servicios de enrutamiento y acceso remoto para seleccionar todos los servicios de función.


***Ejercicio T3.2: Buscar con qué órdenes de terminal o herramientas gráficas podemos configurar bajo Windows y bajo Linux el filtrado y bloqueo de paquetes. 

Para sistema Unix, podemos utilizar "iptables" para IPv4, o "ip6tables" para IPv6.

Para configurar iptables, necesitamos saber que iptables cuenta con cinco tablas, que son zonas en las que una cadena de reglas se puede aplicar:

-raw filtra los paquetes antes que cualquier otra tabla. Se utiliza principalmente para configurar exenciones de seguimiento de conexiones en combinación con el target NOTRACK.
-filter es la tabla por defecto (si no se pasa la opción -t).
-nat se utiliza para la yraducción de dirección de red (por ejemplo, el redirección de puertos). Debido a las limitaciones en iptables, el filtrado no se debe hacer aquí.
-mangle se utiliza para la alteración de los paquetes de red especializados (véase Mangles packet).
-security se utiliza para reglas de conexión de red Mandatory Access Control.

También contiene cadenas, contenidas en las tablas, que son listas de reglas que ordenan los paquete de red. 

Para configurar todo esto, podemos jugar con el comando iptables que dispone de muchísimas opciones, las cuales me llevaría mucho tiempo detallar o probar,


Para realizarlo en Windows Server, según la página oficial de Microsoft, podríamos hacer lo siguiente (no lo he probado porque no uso Windows Server):

Para configurar la seguridad TCP/IP:
-Haga clic en Inicio, seleccione Panel de control, Conexiones de red y haga clic en la conexión de área local que desee configurar.
-En el cuadro de diálogo Estado de conexión, haga clic en Propiedades.
-Haga clic en Protocolo Internet (TCP/IP) y, después, en Propiedades.
-En el cuadro de diálogo Propiedades de Protocolo Internet (TCP/IP), haga clic en Opciones avanzadas
y, a continuación, en Opciones.
-En Configuración opcional, haga clic en Filtrado TCP/IP y en Propiedades.
-Active la casilla de verificación Habilitar filtrado TCP/IP (todos los adaptadores).
-En el cuadro de diálogo Filtrado TCP/IP hay tres secciones en las que puede configurar el filtrado para puertos TCP, puertos UDP (protocolo de datagramas de usuarios) y protocolos Internet. Para cada sección, establezca la configuración de seguridad adecuada para el equipo que utiliza. 


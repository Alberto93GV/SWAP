# PRACTICA 3

## NGINX como balanceador de carga

Lo primero es **crear un nuevo servidor ubuntu** (sin instalarle el paquete LAMP). Accediendo a este como **root** lanzaremos las siguientes ordenes para **instalar NGINX**:

	apt-get update && apt-get dist-upgrade && apt-get autoremove
	apt-get install nginx
	systemctl start nginx

Una vez instalado creamos el **archivo de configuración** con la orden 'touch' en la siguiente ruta:
	
	etc/nginx/conf.d/default.conf

Con el editor 'vi' definimos la **configuración** que se muestra en la siguiente captura para que el balanceador gestione las solicitudes a los servidores creados en las practicas anteriores:

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica3/nginx_conf_1.png)

En el **archivo propio de configuracion de nginx** (que NO el anterior creado para el balanceador en si):

	/etc/nginx/nginx.conf

Lo abrimos con el editor 'vi' y comentamos la linea:

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica3/nginx_conf_2.png)


Finalmente **reiniciamos** el **servicio** con: 

	systemctl restart nginx

Para comprobar el correcto funcionamiento lanzamos varias ordenes '**curl**' a la **IP** del **balanceador** (192.168.56.115) desde la maquina anfitriona:

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica3/prueba_nginx.png)

Como podemos ver cada una de las peticiones la reenvia a un servidor diferente.

## HAPROXY como balaceador de carga

Lo primero es **crear un nuevo servidor ubuntu** (sin instalarle el paquete LAMP). Accediendo a este como **root** lanzaremos las siguientes ordenes para **instalar HAProxy**:

	apt-get update && apt-get dist-upgrade && apt-get autoremove
	apt-get install haproxy

Con el editor 'vi' definimos la **configuración** que se muestra en la siguiente captura para que el balanceador gestione las solicitudes a los servidores creados en las practicas anteriores:

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica3/haproxy_conf.png)

**Lanzamos** el **servicio** con la siguiente orden:

	sudo /usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg

Si no lanza ningun aviso o error es que todo ha ido correctamente.

Finalmente **reiniciamos** el **servicio** con: 

	systemctl restart haproxy

Para comprobar el correcto funcionamiento lanzamos varias ordenes '**curl**' a la **IP** del **balanceador** (192.168.56.120) desde la maquina anfitriona:

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica3/prueba_haproxy.png)

Como podemos ver cada una de las peticiones la reenvia a un servidor diferente.

## Apache BenchMark con NGINX y HAPROXY

Lo primero es **instalar Apache** en la **maquina anfitriona**. Para ello accedemos como **root** y lanzamos las siguientes ordenes:

	apt-get update
	apt-get install -y apache2

Una vez instalado comprobamos si el **servicio** esta **activo**. En caso contrario lanzamos la orden:

	systemctl start apache2

Ahora, con todas las maquinas levantadas (tanto servidores como balanceadores), procedemos a correr el benchmark de apache a ambos balanceadores.

Procedemos primero con **NGINX** para **10000 peticiones** y un **nivel de concurrencia 10**:

	ab -n 10000 -c 10 http://192.168.56.115/index.html

La **salida del benchmark** es la siguiente:

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica3/ab_nginx.png)

Procedemos finalmente con **HAPROXY** igualmente para **10000 peticiones** y un **nivel de concurrencia 10**:

	ab -n 10000 -c 10 http://192.168.56.120/index.html


La **salida del benchmark** es la siguiente:

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica3/ab_haproxy.png)


[**CONCLUSIÓN**]
En base a los resultados podemos concluir que **HAPROXY** tiene un **tiempo de respuesta menor** y por lo tanto mejor que **NGINX**.


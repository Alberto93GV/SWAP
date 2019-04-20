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

De nuevo con el editor 'vi' lo abrimos y comentamos la siguiente linea:

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica3/nginx_conf_2.png)


Finalmente **reiniciamos** el **servicio** con: 

	systemctl restart nginx

Para comprobar el correcto funcionamiento lanzamos varias ordenes '**curl**' a la **IP** del **balanceador** (192.168.56.115) desde la maquina anfitriona:

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica3/prueba_nginx.png)

Como podemos ver cada una de las peticiones la reenvia a un servidor diferente.

## HAPROXY como balaceador de carga



## Apache BenchMark con NGINX



## Apache BenchMark con HAPROXY

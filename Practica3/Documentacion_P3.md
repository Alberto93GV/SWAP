# PRACTICA 3

## NGINX como balanceador de carga

Lo primero es **crear un nuevo servidor ubuntu** (sin instalarle el paquete LAMP). Accediendo a este como **root** lanzaremos las siguientes ordenes para **instalar NGINX**:

	apt-get update && apt-get dist-upgrade && apt-get autoremove
	apt-get install nginx
	systemctl start nginx

Una vez instalado creamos el **archivo de configuración** con la orden 'touch' en la siguiente ruta:
	
	etc/nginx/conf.d/default.conf

Con el editor 'vi' definimos la **configuración** que se muestra en la siguiente captura para que el balanceador gestione las solicitudes a los servidores creados en las practicas anteriores:

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica3/nginx_conf.png)


Finalmente **reiniciamos** el **servicio** con: 

	systemctl start nginx






## HAPROXY como balaceador de carga



## Apache BenchMark con NGINX



## Apache BenchMark con HAPROXY

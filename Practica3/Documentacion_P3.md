# PRACTICA 3

## NGINX como balanceador de carga

Lo primero es ***crear un nuevo servidor ubuntu*** (sin instalarle el paquete LAMP). Accediendo a este como ***root*** lanzaremos las siguientes ordenes para ***instalar NGINX*** como balanceador:

	apt-get update && apt-get dist-upgrade && apt-get autoremove
	apt-get install nginx
	systemctl start nginx

Una vez instalado podremos acceder a su ***archivo de configuracion*** y editarlo con 'vi' en la siguiente ruta:
	
	etc/nginx/conf.d/default.conf

La configuracion quedaria como se muestra en la siguiente captura:





## HAPROXY como balaceador de carga



## Apache BenchMark con NGINX



## Apache BenchMark con HAPROXY

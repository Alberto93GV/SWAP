# PRACTICA 4

## Instalación certificado SSL autofirmado
Introduciendo las siguientes ordenes como root podemos **generar** en 'Ubuntu Server' un **certificado SSL autofirmado**. Para ello lo primero es **activar Apache**, generarlos y especificarle la ruta a estos:

	a2enmod ssl
	service apache2 restart
	mkdir /etc/apache2/ssl
	openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt

Tras esto se nos solicitaran un conjunto de datos para la configuracion del dominio como se muestra en la siguiente captura:

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica4/img.png)



## Configuración de las reglas del cortafuegoss





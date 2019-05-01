# PRACTICA 4

## Instalación certificado SSL autofirmado
Introduciendo las siguientes ordenes como root podemos **generar** en 'Ubuntu Server' un **certificado SSL autofirmado**. Para ello lo primero es **activar el modulo SSL** de 'Apache':

	a2enmod ssl

Reiniciamos 'Apache' y creamos un directorio para los certificados:

	service apache2 restart
	mkdir /etc/apache2/ssl

Generamos los certificados SSL autofirmados y le indicamos la ruta anterior:

	openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt

Tras esto se nos solicitaran un conjunto de datos para la configuracion del dominio como se muestra en la siguiente captura:

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica4/config_dominio.png)

Procedemos pues a **editar** con 'vi' el archivo de **configuracion por defecto** de **SSL**:

	vi /etc/apache2/sites-available/default-ssl.conf

Debemos **añadir** las **rutas** de los **certificados** como se muestra en la siguiente captura:

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica4/config_ssl.png)

Ahora **activamos** el sitio **default-ssl** y hacemos un **reload** a 'Apache':

	a2ensite default-ssl
	service apache2 reload

Tras esto tanto desde el **navegador** como desde la **terminal** con 'curl' probamos a conectarnos mediante '**https://IP**' y comprobar que funciona correctamente como se muestra en la siguiente captura:

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica4/prueba_https_m1.png)

Ahora debemos **copiar** tantos las **claves** como la **configuracion SSL** de m1 **en m2** usando **rsync** con los siguiente comandos desde m2:

	rsync -avz -e ssh 192.168.56.105:/etc/apache2/ssl/* /etc/apache2/ssl/
	rsync -avz -e ssh 192.168.56.105:/etc/apache2/sites-available/default-ssl.conf /etc/apache2/sites-available/

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica4/copia_claves_a_m2.png)

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica4/copia_config_ssl_a_m2.png)






## Configuración de las reglas del cortafuegoss





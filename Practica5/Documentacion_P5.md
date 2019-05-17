# PRACTICA 5

## Crear una BD con al menos una tabla y algunos datos
Lo primero es crear una BD en MySQL e insertar datos para poder hacer la copia de seguridad mas adelante. Para entrar en mysql y crear la BD junto con la tabla deberiamos lanzar las siguientes ordenes:

	mysql -uroot -p
	
	mysql> create database contactos;
	mysql> use contactos;
	mysql> show tables;
	mysql> create table datos(nombre varchar(100), tlf int);

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica5/creacion_bd_mysql_y_tabla.png)

Procedemos a introducir un registro de prueba y mostramos como quedaria la tabla:

	mysql> insert into datos(nombre,tlf) values ("Alberto",958553876);
	mysql> select * from datos;

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica5/insertar_dato_y_consultarlos.png)

En esa tabla hice la inserción de mas datos/registros para despues hacer la copia de seguridad quedando de la siguiente manera:

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica5/tabla_final.png)

## Copia de seguridad de la BD usando mysqldump
MySQL ofrece una herramienta para el clonado de las BD llamada 'mysqldump'. Con el siguiente comando obtenemos la lista de opciones disponibles para la misma:

	mysqldump --help

Antes de hacer la copia debemos cerrar el acceso a la BD para evitar que se cambie nada:

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica5/evitar_acceso_a_la_BD.png)

Nos salimos de mysql y hacemos una copia/clonado de la BD con la siguiente orden:

	mysqldump BD_ejemplo -u root -p > /tmp/BD_ejemplo.sql

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica5/copia_BD_en_m1.png)

Desbloqueamos las tablas como se muestra en la siguiente captura:

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica5/desbloquear_tablas.png)

Ahora abrimos la maquina 2 y copiamos la BD de m1 con la siguiente orden:

	scp IP:/dir/BD_ejemplo.sql /dirLocal/

Particularmente en mi caso lanzaria desde m2:

	scp 192.168.56.105:/tmp/contactos.sql /tmp/

Destacar que el archivo .sql contiene las sentencias necesarias para reconstruir los datos/registros de la BD pero antes de hacer esto deberiamos crear la BD en m2 como hicimos anteriormente en m1.

## Restaurar dicha copia en m2
Para restaurarla en m2, una vez creada la BD por lo anteriormente comentado, lanzariamos la siquiente orden:

	mysql -u root -p contactos < /tmp/contactos.sql

Mostramos la BD para comprobar que el volcado se haya realizado correctamente:






## Configuración maestro-esclavo replicación auto. de datos entre maquinas



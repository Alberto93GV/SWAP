# PRACTICA 5

## Crear una BD con al menos una tabla y algunos datos
Lo primero es crear una BD en MySQL e insertar datos para poder hacer la copia de seguridad mas adelante. Para entrar en mysql y crear la BD junto con la tabla deberiamos lanzar las siguientes ordenes:

	mysql -uroot -p
	
	mysql> create database contactos;
	mysql> use contactos;
	mysql> show tables;
	mysql> create table datos(nombre varchar(100), tlf int);

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica5/creacion_bd_mysql_y_tabla.png)

A continuación procedemos a introducir un registro de prueba:

	mysql> insert into datos(nombre,tlf) values ("Alberto",958553876);

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica5/insertar_dato_y_consultarlos.png)


## Copia de seguridad de la BD usando mysqldump




## Restaurar dicha copia en m2




## Configuración maestro-esclavo replicación auto. de datos entre maquinas



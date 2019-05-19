# PRACTICA 5

## Crear una BD con al menos una tabla y algunos datos
Lo primero es **crear una BD** en **MySQL** e **insertar datos** para poder hacer la copia de seguridad mas adelante. Para entrar en mysql y crear la BD junto con la tabla deberiamos lanzar las siguientes ordenes:

	mysql -uroot -p
	
	mysql> create database contactos;
	mysql> use contactos;
	mysql> show tables;
	mysql> create table datos(nombre varchar(100), tlf int);

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica5/creacion_bd_mysql_y_tabla.png)

Procedemos a **introducir** un **registro** de prueba y **mostramos** como quedaria la **tabla**:

	mysql> insert into datos(nombre,tlf) values ("Alberto",958553876);
	mysql> select * from datos;

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica5/insertar_dato_y_consultarlos.png)

En esa tabla hice la inserción de mas datos/registros para despues hacer la copia de seguridad quedando de la siguiente manera:

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica5/tabla_final.png)

## Copia de seguridad de la BD usando mysqldump
MySQL ofrece una **herramienta** para el **clonado** de las **BD** llamada '**mysqldump**'. Con el siguiente comando obtenemos la **lista de opciones** disponibles para la misma:

	mysqldump --help

Antes de hacer la copia debemos **cerrar el acceso a la BD** para evitar que se cambie nada:

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica5/evitar_acceso_a_la_BD.png)

Nos salimos de mysql y **hacemos** una **copia/clonado** de la **BD** con la siguiente orden:

	mysqldump BD_ejemplo -u root -p > /tmp/BD_ejemplo.sql

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica5/copia_BD_en_m1.png)

**Desbloqueamos** las **tablas** como se muestra en la siguiente captura:

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica5/desbloquear_tablas.png)

Ahora **arrancamos m2** y **copiamos la BD de m1** con la siguiente orden:

	scp IP:/dir/BD_ejemplo.sql /dirLocal/

Particularmente en mi caso lanzaria desde m2:

	scp 192.168.56.105:/tmp/contactos.sql /tmp/

Destacar que el **archivo .sql** contiene las **sentencias** necesarias para **reconstruir** los **datos/registros** de la BD pero **antes** de hacer esto **deberiamos crear la BD en m2** como hicimos anteriormente en m1.

## Restaurar dicha copia en m2
Para **restaurarla** en m2, una vez creada la BD por lo anteriormente comentado, lanzariamos la siquiente orden:

	mysql -u root -p contactos < /tmp/contactos.sql

Mostramos la BD para **comprobar** que el **volcado** se haya **realizado correctamente**:

	mysql> select * from datos;

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica5/volcado_copia_en_BD_m2.png)

## Configuración maestro-esclavo replicación auto. de datos entre maquinas
Todo el proceso anterior seria llevado acabo por un administrador a mano. La idea es **configurar** por un lado al **maestro (m1)** y por otro lado al **esclavo (m2)** para **automatizar** este **proceso** lo cual seria lo ideal en un escenario de produccion real.

En m1 **abrimos** como root con 'vi' el archivo:

	/etc/mysql/mysql.conf.d/mysqld.cnf

**Comentamos** el siguiente paremetro que sirve para escuchar a un servidor:

	#bind-address 127.0.0.1

**Indicamos** el archivo donde almacenar el **log** de **errores**:

	log_error = /var/log/mysql/error.log

**Establecemos** el **identificador** del servidor:

	server-id = 1

Finalmente **reiniciamos** el servicio **mysql**:

	/etc/init.d/mysql restart

Pasamos finalmente a **configurar** al **esclavo (m2)**. Deberiamos seguir los **mismos pasos** que acabamos de hacer en m1 **a diferencia** de que el **identificador** en esta maquina sera:

	server-id = 2

**Reiniciariamos** para acabar el **servicio**.

[**NOTA**]

Como mi version de MySQL es superior a la 5.5 (en concreto la 5.7.23) no debemos indicar los datos relativos al maestro en la configuración los cuales serian los siguientes:

	Master-host = 192.168.56.105
	Master-user = root
	Master-password = 1234

Ahora accedemos a MySQL en el maestro, **creamos** un **usuario** y le **damos permisos de acceso** para la replicación:

	mysql> CREATE USER esclavo IDENTIFIED BY 'esclavo';
	mysql> GRANT REPLICATION SLAVE ON *.* TO 'esclavo'@'%' IDENTIFIED BY 'esclavo';
	mysql> FLUSH PRIVILEGES;
	mysql> FLUSH TABLES;
	mysql> FLUSH TABLES WITH READ LOCK;

Para finalizar con el maestro vamos a **consultar los datos de la BD** que posteriormente vamos a replicar en el esclavo:

	mysql> SHOW MASTER STATUS;

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica5/show_master_status.png)

Nos iriamos pues al **esclavo**, entrariamos en MySQL, le **facilitariamos los datos** del maestro y **arrancariamos** el **esclavo**:


![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica5/configuracion_final_esclavo.png)

Volvemos al **maestro** para **desbloquear** las **tablas** para que puedan meterse nuevos datos con la siguiente orden:

	mysql> UNLOCK TABLES;

Para comprobar que la replicacion funciona correctamente vamos a introducir el siguiente registro en m1 e iremos a m2 para ver si este se ha copiado correctamente:

	mysql> use contactos;
	mysql> insert into datos(nombre,tlf) values ("Prueba",666555444);

Desde **m2 consultamos la tabla** y vemos que **efectivamente** dicho registro **ha sido replicado** como se muestra en la siguiente captura:

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica5/comprobacion_replicacion.png)










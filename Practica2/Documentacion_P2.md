# PRACTICA 2

## Clonación de archivos entre máquinas por SSH
En la P1 desactive el parámetro **PermitRootLogin** por motivos de seguridad. Para hacer el copiado/envió de datos entre máquinas vamos a activarlo a '**yes**' con el editor **vi** en la configuración del ssh: **/etc/ssh/sshd_config**. 

Una vez llevada acabo la modificación lanzaremos **:wq** para escribir/guardar los cambios y cerrar el editor. Posteriormente reiniciamos el servicio con: **systemctl restart ssh**.

Después crearíamos por ejemplo una carpeta en una de las maquinas y la enviariamos comprimida en un archivo tar por ssh a la otra con: **tar czf ./carpeta | ssh 192.168.56.xxx 'cat > ~/tar.tgz'**

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica2/envio_ssh_m1.png)

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica2/envio_ssh_m2.png)

**[NOTA]**

El clonado se podría realizar con un directorio ya existente lo cual suele ser lo mas habitual pero dado la simplicidad del ejemplo y como introducción decidí hacerlo sobre una carpeta nueva. Mas adelante vamos a hacer el clonado sobre el directorio web **/var/www/** que es en lo que se basa esta práctica.

## Clonación de archivos entre máquinas con RSYNC
Para algo puntual el procedimiento anterior puede ser muy útil. Sin embargo para la **sincronización de grandes cantidades de información** lo ideal es usar **rsync**. Se puede instalar con: **apt-get install rsync**. En mis máquinas no hizo falta por que ya lo estaba.

A la hora de trabajar podemos hacerlo como usuario root o con el usuario habitual. Como con este ultimo podremos realizar todas las configuraciones por comodidad vamos a **hacer al usuario habitual dueño del directorio** que queremos clonar con: **sudo chown alberto:alberto -R /var/www**

Lo que yo hice fue **clonar en el directorio web de m1** el de **m2**. Para comprobar el correcto funcionamiento previamente cree en el directorio web de m2 un archivo llamado "**archivo_m2**". Ademas en las capturas podemos ver como al abrir el "hola.html" que creamos en la P1 este corresponde efectivamente al de m2.

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica2/rsync_m1.png)

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica2/rsync_m2.png)

## Acceso SSH sin solicitud de contraseña
Como comente en la P1 cree llaves privadas y publicas en ambas maquinas (ssh-keygen) y compartí la pública (ssh-copy-id) de m1 con m2 y viceversa para poder conectarme entre ellas. Sin embargo el uso de estas exigía la solicitud de una contraseña.

Ahora la idea es que ambas máquinas compartan unas llaves publicas que no exijan contraseña. Podemos generarlas con ssh-keygen de la siguiente manera: **ssh-keygen -b 4096 -t rsa**. Posteriormente habría que compartirlas con **ssh-copy-id usuario@IP**.

A continuación en las **capturas** se muestra un ejemplo de la **generación de las clave en m1** y la **distribución de la pública a m2** y el **accesso de m2 a m1 sin contraseña**. El proceso de generación y distribución ha de realizarse con ambas máquinas.

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica2/ssh_sin_contraseña_m1.png)

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica2/ssh_sin_contraseña_m2.png)

## Programar con CRONTAB una tarea periódica
En la linea de esta práctica lo que vamos a hacer es programar en crontab que **cada 'x' tiempo** se haga una **copia del directorio web de m1 en m2**.

Para **comprobar y ver visualmente** en las capturas el **correcto funcionamiento** crearemos en el directorio de m1 por ejemplo el archivo "**crontab_OK**".

La **lista de tareas programadas** se encuentran en el archivo: **/etc/crontab**

[**NOTA**]
Podemos abrir, editar y guardar con **vi** el archivo anterior como se menciono en el primer apartado de esta practica. 

Añadiendo la siguiente orden conseguiremos que la copia se haga a los 45min de cada hora: 

	**45 *	* * *	root	rsync -avz -e ssh alberto@192.168.56.110:/var/www /var/www**.

Una vez hecho esto deberiamos reiniciar el servicio con **systemctl restart cron** y esperar a que se realice la copia.



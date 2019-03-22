# PRACTICA 2

## Clonación de archivos entre máquinas por SSH
En la P1 desactive el parametro **PermitRootLogin** por motivos de seguridad. Para hacer el copiado/envio de datos entre máquinas vamos a activarlo a '**yes**' con el editor **vi** en la configuración del ssh: **/etc/ssh/sshd_config**. 

Una vez llevada acabo la modificacion lanzaremos **:wq** para escribir/guardar los cambios y cerrar el editor. Posteriormente reiniciamos el servicio con: **systemctl restart ssh**.

Despues creariamos por ejemplo una carpeta en una de las maquinas y la enviariamos comprimida en un archivo tar por ssh a la otra con: **tar czf ./carpeta | ssh 192.168.56.xxx 'cat > ~/tar.tgz'**

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica2/envio_ssh_m1.png)

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica2/envio_ssh_m2.png)

**[NOTA]**

El clonado se podria realizar con un directorio ya existente lo cual suele ser lo mas habitual pero dado la simplicidad del ejemplo y como introducción decidi hacerlo sobre una carpeta nueva. Mas adelante vamos a hacer el clonado sobre el directorio web **/var/www/html** que es en lo que se basa esta práctica.

## Copia de archivos entre máquinas con RSYNC
Para algo puntual el procedimiento anterior puede ser muy útil. Sin embargo para la **sincronización de grandes cantidades de información** lo ideal es usar **rsync**.

Rsync se puede instalar con: **apt-get install rsync**. En mis máquinas no hizo falta por que ya lo estaba.

A la hora de trabajar podemos hacerlo como usuario root o con el usuario habitual. Como con este ultimo podremos realizar todas las configuraciones por comodidad vamos a hacer al usuario habitual dueño del directorio que queremos clonar en mi caso con: **sudo chown alberto:alberto -R /var/www**

Lo que yo hice fue **clonar en el directorio web de m1** el de **m2**. Para comprobar el correcto funcionamiento previamente cree en el directorio web de m2 un archivo llamado "**archivo_m2**". Ademas en las capturas podemos ver como al abrir el "hola.html" que creamos en la P1 este corresponde efectivamente al de m2.

## Apartado n




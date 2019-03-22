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
Para algo puntual el procedimiento anterior puede ser muy útil. Sin embargo para la sincronización de grandes cantidades de información lo ideal es usar **rsync**.

Podemos instalarlo con **apt-get install rsync** aunque en mis máquinas no hizo falta por que ya lo estaba.


## Apartado n




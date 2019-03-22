# PRACTICA 2

## Copia de archivos por SSH
En la practica anterior desactive el parametro **PermitRootLogin** por motivos de seguridad en la configuración del ssh. Para hacer el copiado/envio de datos entre máquinas vamos a activarlo (yes) con el editor vi en _/etc/ssh/sshd__config_. 

Una vez llevada acabo la modificacion lanzaremos **:wq** para escribir/guardar los cambios y cerrar el editor. Posteriormente reiniciamos el servicio con **systemctl restart ssh**.

Despues creariamos por ejemplo una carpeta en una de las maquinas (podriamos haberlo realizado con un directorio ya existente lo cual suele ser lo mas habitual en la vida real) y enviarla comprimida en un archivo tar por ssh a la otra maquina con el siguiente comando: **tar czf ./carpeta | ssh 192.168.56.xxx 'cat > ~/tar.tgz'**

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica2/envio_ssh_m1.png)

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica2/envio_ssh_m2.png)


## Apartado 1

...

## Apartado n




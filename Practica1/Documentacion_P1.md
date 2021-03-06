# PRACTICA 1

## Instalación de las máquinas
Máquinas ‘**m1**’ y ‘**m2**’:

- Sistema: Ubuntu Server 16.04 LTS
- RAM: 1GB
- HDD: 8GB 
- Usuario: alberto   Password: 1234
- Particionado: guiado por defecto
- LAMP y OpenSSH: añadidos durante la instalación
- Sin proxy añadido y sin actualizaciones automáticas

## Interfaces de RED
Interfaz de red por defecto:
 
- **enp0s3**: red NAT respecto al anfitrión para el acceso a internet

Interfaz de red definida:

- **enp0s8**: adaptador solo-anfitrión o red interna que incluye tanto al anfitrión como a la propia maquina

Las **IP definidas** para cada máquina son:

- **m1**:  192.168.56.105
- **m2**:  192.168.56.110


La **configuración** de la interfaz de red **enp0s8** se añade en:
_/etc/network/interfaces_

	auto enp0s8

	iface enp0s8 inet static

	address 192.168.56.xxx


**[NOTA]**

Previamente haciendo **CTRL+W** en virtualbox podríamos **crear la red** (enp0s8) para posteriormente desde la configuración de cada máquina también en el mismo virtualbox **añadirla en el 2 slot** como “**Adaptador solo-anfitrión**”.

## Servidor web (LAMP)
Se trata de una pila de servicios/programas para la instalación de un servidor web.
 
	LAMP = Linux Apache MySQL PHP

En mi caso lo añadí durante la instalación del servidor. En caso contrario habría que instalar manualmente cada uno de ellos.

## SSH
También fue añadido durante la instalación del servidor. Se trata de un servicio/protocolo seguro de **acceso remoto a servidores**.

Por motivos de seguridad **denegamos el acceso root** cambiando el valor del parametro 'PermitRootLogin' del archivo: _/etc/ssh/sshd_config_

Habria que en ambas maquinas **generar las llaves privada y publica** (ssh-keygen) y **copiar la publica en el cliente** (ssh-copy-id) para poder acceder de m1 a m2 y viceversa.

El puerto por defecto para ssh (22) no ha sido modificado.

## CURL
Se usa para la **transferencia de archivos** con **sintaxis URL** y soporta diversos protocolos. En general se utiliza para **automatizar transferencias** de archivos o **simular la navegación web** de un usuario en un servidor.

Esta herramienta si fue instalada desde la terminal con el comando: _apt-get install curl_

Para probar su funcionamiento creamos en ambas maquinas el archivo "hola.html" en el directorio: _/var/www/html_

## Acceso SSH (m1 a m2)

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica1/ssh_m1.png)

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica1/ssh_m2.png)

## Acceso CURL (m1 a m2)

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica1/curl_m1.png)

![imagen](https://github.com/Alberto93GV/SWAP/blob/master/Practica1/curl_m2.png)

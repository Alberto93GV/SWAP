# PRACTICA 1

## Instalación de las máquinas
Máquinas ‘**m1**’ y ‘**m2**’:
    * **Sistema**: Ubuntu Server 16.04 LTS
    * **RAM**: 1GB
    * **HDD**: 8GB 
    * **Usuario**: alberto	**Password**: 1234
    * **Particionado**: guiado por defecto
    * **LAMP** y **OpenSSH**: añadidos durante la instalación

_Sin proxy añadido y sin actualizaciones automáticas._

## Interfaces de RED
Interfaz de red por defecto: 
    * **enp0s3**: red NAT respecto al anfitrión para el acceso a internet

Interfaz de red definida:
    * **enp0s8**: adaptador solo-anfitrión o red interna que incluye tanto al anfitrión como a la propia maquina

Las **IP definidas** para cada máquina son:
    • **m1**:  192.168.56.105
    • **m2**:  192.168.56.110

La **configuración** de la interfaz de red **enp0s8** se añade en:
_/etc/network/interfaces_

Y es la siguiente:
**auto enp0s8**
**iface enp0s8 inet static**
**address 192.168.56.xxx**

**[NOTA]**
Previamente haciendo **CTRL+W** en virtualbox podríamos **crear la red** (enp0s8) para posteriormente desde la configuración de cada máquina también en el mismo virtualbox **añadirla en el 2 slot** como “**Adaptador solo-anfitrión**”.

## Servidor web (LAMP)
Se trata de una pila de servicios/programas para la instalación de un servidor web.
 
_LAMP = Linux Apache MySQL PHP_

En mi caso lo añadí durante la instalación del servidor. En caso contrario habría que instalar manualmente cada uno de ellos.

## SSH
También fue añadido durante la instalación del servidor. Se trata de un servicio/protocolo seguro de acceso remoto a servidores.

## CURL
Se usa para la **transferencia de archivos** con **sintaxis URL** y soporta diversos protocolos. En general se utiliza para **automatizar transferencias** de archivos o **simular** la **navegación web** de un **usuario** en un servidor.

Esta herramienta si fue instalada desde la terminal con el comando: _apt-get install curl_

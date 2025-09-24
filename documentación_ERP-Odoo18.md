# Instalación y configuración de un ERP (Odoo18)
En este archivo documentaremos la instalación de Odoo 18 paso a paso.

#### Lo primero que haremos será crear una maquina virtual con un Ubuntu server, para ello usaremos:
<p align="center">
  <img src="https://cdn.freebiesupply.com/logos/large/2x/virtualbox-logo-png-transparent.png" alt="Logo VirtualBox" width="300"/>
</p>

#### Una vez que tengamos el servidor en funcionamiento, tendremos que cambiar los locales a español, para ello usaremos:
`dpkg-reconfigure locales` - una vez dentro seleccionamos "*es_ES. UTF-8*"
#### y para la distribución del teclado usaremos:
`dpkg-reconfigure keyboard-configuration` una vez dentro seleccionamos cualquier teclado y le damos a español.
#### Después de configurar, es muy  importante reiniciar

---
## Comenzamos con la instalación de Odoo18:
#### Lo primero que haremos será instalar el servidor PostgreSQL con el siguiente comando:
`sudo apt install postgresql -y`
#### Seguido de esto, instalaremos el repositorio de Odoo18 con los siguientes comandos:
#### es recomendable instalar ssh para poder copiar y pegar los comandos, en vez de escribirlos a mano, por tanto tendremos que poner estos comandos ANTES:
- `sudo apt update`
- `sudo apt-get install ssh`
- `sudo apt-get install openssh-server`
- ##### cambiamos la red de NAT a adaptador puente y hacemos el comando: `ip a` para saber que ip tenemos
- ##### abrimos la terminal del dispositivo (la de la máquina virtual NO) y ponemos el siguiente comando: `ssh vboxuser@172.30.16.173`
- ##### le decimos "yes" y ponemos la contraseña de la *máquina virtual*
---

- `wget -q -O - https://nightly.odoo.com/odoo.key | sudo gpg --dearmor -o /usr/share/keyrings/odoo-archive-keyring.gpg` <br><br>
- `echo 'deb [signed-by=/usr/share/keyrings/odoo-archive-keyring.gpg] https://nightly.odoo.com/18.0/nightly/deb/ ./' | sudo tee /etc/apt/sources.list.d/odoo.list` <br><br>
- `sudo apt-get update && sudo apt-get install odoo` <br><br>

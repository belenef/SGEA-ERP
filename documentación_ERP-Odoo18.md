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

---
## Comenzamos con la instalación de Odoo18:
#### Lo primero que haremos será instalar el servidor PostgreSQL con el siguiente comando:
`sudo apt install postgresql -y`
#### Seguido de esto, instalaremos el repositorio de Odoo18 con los siguientes comandos:
- `wget -q -O - https://nightly.odoo.com/odoo.key | sudo gpg --dearmor -o /usr/share/keyrings/odoo-archive-keyring.gpg` <br><br>
- `echo 'deb [signed-by=/usr/share/keyrings/odoo-archive-keyring.gpg] https://nightly.odoo.com/18.0/nightly/deb/ ./' | sudo tee /etc/apt/sources.list.d/odoo.list` <br><br>
- `sudo apt-get update && sudo apt-get install odoo` <br><br>

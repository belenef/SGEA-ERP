# Instalación y configuración de un ERP (Odoo18)
En este archivo documentaremos la instalación de Odoo 18 paso a paso.

#### Lo primero que haremos será crear una maquina virtual con un Ubuntu server, para ello usaremos:
<p align="center">
  <img src="https://cdn.freebiesupply.com/logos/large/2x/virtualbox-logo-png-transparent.png" alt="Logo VirtualBox" width="300"/>
</p>

##### Una vez que tengamos el servidor en funcionamiento, tendremos que cambiar los locales a español, para ello usaremos:
`dpkg-reconfigure locales` - una vez dentro seleccionamos "*es_ES. UTF-8*"
##### y para la distribución del teclado usaremos:
`dpkg-reconfigure keyboard-configuration` una vez dentro seleccionamos cualquier teclado y le damos a español.

---
#### Comenzamos con la instalación de Odoo18:
##### Lo primero que haremos será instalar el servidor PostgreSQL con el siguiente comando:
`sudo apt install postgresql -y`

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
#### Seguido de esto, instalaremos el repositorio de Odoo18 
#### es recomendable instalar ssh para poder copiar y pegar los comandos, en vez de escribirlos a mano, por tanto tendremos que poner estos comandos ANTES:
- `sudo apt update`
- `sudo apt-get install ssh`
- `sudo apt-get install openssh-server`
- ##### cambiamos la red de NAT a adaptador puente y hacemos el comando: `ip a` para saber que ip tenemos
- ##### abrimos la terminal del dispositivo (la de la máquina virtual NO) y ponemos el siguiente comando: `ssh vboxuser@172.30.16.173`
- ##### le decimos "yes" y ponemos la contraseña de la *máquina virtual*
---
#### Instalación Odoo18:
- `wget -q -O - https://nightly.odoo.com/odoo.key | sudo gpg --dearmor -o /usr/share/keyrings/odoo-archive-keyring.gpg` <br><br>
- `echo 'deb [signed-by=/usr/share/keyrings/odoo-archive-keyring.gpg] https://nightly.odoo.com/18.0/nightly/deb/ ./' | sudo tee /etc/apt/sources.list.d/odoo.list` <br><br>
- `sudo apt-get update && sudo apt-get install odoo` <br><br>
#### Ya que he podido comprobar que al utilizar estos comandos me salta un error, he instalado Odoo vía Docker para instalarlo sin problemas.
#### Antes de instalar Docker Engine por primera vez en un nuevo host, debe configurar el `apt` repositorio de Docker. Hay que ejecutar linea por linea, todo junto **NO**
```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```
#### Después, instalamos los paquetes de Docker:
`sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin`
#### y verificamos que se está ejecutando:
`sudo systemctl status docker`

---
### Para poner en marcha Odoo 18 en modo producción crearemos dos contenedores:
- El primer contenedor contendrá la base de datos PostgreSQL en su versión 15.
- El segundo contenedor contendrá el servidor Odoo.
#### Creamos el contenedor de PostgreSQL con:
```
docker run -d -v /home/usuario/OdooDesarrollo/dataPG:/var/lib/postgresql/data -e
POSTGRES_USER=odoo -e POSTGRES_PASSWORD=odoo -e POSTGRES_DB=postgres --name db
postgres:15
```
#### Con el contenedor PostgreSQL ya en marcha, creamos el contenedor con Odoo con:
`docker run -d -p 8069:8069 --name odooprod --user="root" --link db:db odoo:18`

---
### Abrimos Odoo18
#### Para ello primero debemos saber cual es nuestra **ip**, ejecutando este comando: 
`ip a`
#### Para abrir Odoo18, deberemos poner en el buscador lo siguiente:
`(tu ip):8069`
#### Una vez dentro deberas poner tus datos en el login e iniciar sesión en Odoo18 para poder utilizarlo.

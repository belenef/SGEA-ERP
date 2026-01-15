# Instalación de Docker y Odoo 18 usando Docker Compose en Linux

Esta guía explica paso a paso cómo instalar **Docker** y levantar Odoo 18 usando `docker compose up -d` sin necesidad de instalar PostgreSQL manualmente, ya que el contenedor de Odoo incluye todo lo necesario.

---

## 1️⃣ Preparar la máquina virtual

1. Crear una máquina virtual con Ubuntu Server (VirtualBox recomendado).
2. Configurar locales a español:

```bash
dpkg-reconfigure locales
```

Selecciona `es_ES.UTF-8`.
3. Configurar distribución del teclado:

```bash
dpkg-reconfigure keyboard-configuration
```

Selecciona el teclado deseado y español.
4. Reinicia la máquina para aplicar cambios.

---

## 2️⃣ Instalar Docker Engine

### a) Actualizar sistema e instalar dependencias

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install ca-certificates curl gnupg lsb-release -y
```

### b) Agregar la clave GPG de Docker

```bash
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

### c) Agregar el repositorio de Docker

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
```

### d) Instalar Docker y Docker Compose Plugin

```bash
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```

### e) Verificar que Docker se esté ejecutando

```bash
sudo systemctl status docker
```

---

## 3️⃣ Levantar Odoo 18 usando Docker Compose

Coloca tu `docker-compose.yml` en la carpeta del proyecto (fuera de `volumesOdoo`) y ejecuta:

```bash
docker compose up -d
```

> Nota: Este comando levantará automáticamente Odoo y el contenedor de PostgreSQL incluido, sin necesidad de instalarlo por separado.

---

## 4️⃣ Acceder a Odoo 18

1. Verificar la IP de la máquina:

```bash
ip a
```

2. Abrir Odoo en navegador:

```
http://<TU_IP>:8069
http://<TU_IP>:8069/web?debug=assets
```

3. Crear base de datos en español y comenzar a usar Odoo.

---

## 5️⃣ Comandos útiles de Docker

* Contenedores activos: `docker ps`
* Todos los contenedores: `docker ps -a`
* Detener y eliminar contenedores en conflicto:

```bash
sudo docker stop odoo-web
sudo docker rm odoo-web
```

* Reiniciar Odoo: `docker compose restart web`

---

## 6️⃣ Estructura de proyecto recomendada

```
tu-proyecto/
├─ docker-compose.yml  # Fuera de volumesOdoo
├─ volumesOdoo/
│  ├─ addons/
│  ├─ odoo-web-data/
│  └─ dataPostgreSQL/
```

> Nota: `docker-compose.yml` debe estar fuera de la carpeta `volumesOdoo`.

---

Esta guía permite instalar **solo Docker** y levantar Odoo 18 usando Docker Compose, sin necesidad de instalar PostgreSQL manualmente.

# Guía para crear un módulo en Odoo usando Docker (Scaffold)

Esta guía explica paso a paso cómo crear un módulo de Odoo utilizando el comando **scaffold** cuando Odoo está ejecutándose dentro de un contenedor Docker.

---

## 📦 Requisitos

* Odoo ejecutándose vía **Docker**
* Acceso a la terminal Linux (host)
* Volumen de addons correctamente mapeado

En este caso:

* Contenedor de Odoo: **`odoo-web`**
* Imagen: **`odoo:18`**
* Ruta de addons en el host:

  ```
  /home/vboxuser/dockercompose/volumesOdoo/addons
  ```
* Ruta de addons dentro del contenedor:

  ```
  /mnt/extra-addons
  ```

---

## 🔎 1. Verificar el nombre del contenedor

Ejecuta:

```bash
docker ps
```

Deberías ver algo similar a:

```
NAMES
odoo-web
```

Este nombre es el que se usará en los comandos siguientes.

---

## 🛠️ 2. Crear el módulo con scaffold

Ejecuta el siguiente comando para crear un módulo llamado `mi_modulo`:

```bash
docker exec -it odoo-web odoo scaffold mi_modulo /mnt/extra-addons
```

### 📌 Error común: `odoo: command not found`

Algunas imágenes usan `odoo-bin` en lugar de `odoo`. Si ocurre ese error, usa:

```bash
docker exec -it odoo-web odoo-bin scaffold mi_modulo /mnt/extra-addons
```

Cualquiera de los dos funciona con la imagen **odoo:18**, dependiendo de la configuración.

---

### Otra manera de crearlo (mas facil):
ir a la ruta donde esta docker --> `/home/vboxuser/dockercompose#`<br>
Acceder a la `bash` de odoo --> `docker exec -it odoo-web bash`<br>
Cambiar a la ruta donde estan los addons --> `cd mnt/extra-addons/`<br>
Crear el modulo con `scaffold` --> `odoo scaffold (nombre del modulo)`<br>
Hacer un `ls` para comprobar su creacion.<br>

---

## 🔄 5. Reiniciar Odoo

Para que Odoo detecte el nuevo módulo:

```bash
docker restart odoo-web
```
O tambien podemos apagar odoo y volverlo a ejecutar:
```
docker compose down
```
```
docker compose up -d
```

---

## 🖥️ 6. Activar el módulo en Odoo

Desde la interfaz web de Odoo:

1. Activa el **modo desarrollador**
2. Ve a **Aplicaciones**
3. Pulsa **Actualizar lista de aplicaciones**
4. Busca **mi_modulo**
5. Instálalo

---

✅ ¡Listo! Ya tienes tu módulo Odoo creado correctamente usando Docker y scaffold.


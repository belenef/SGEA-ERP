# Guía para crear un módulo en Odoo vía terminal (Linux)

Esta guía paso a paso te enseña cómo crear un módulo mínimo de Odoo directamente desde la terminal en Linux, sin usar la interfaz web.

---

## 1. Preparar el entorno

1. Asegúrate de que tus contenedores de Odoo y PostgreSQL estén funcionando:

```bash
docker compose ps
```

2. Abre la carpeta de addons dentro de tu host (VM) o del contenedor:

```bash
cd ~/dockercompose/odoo_custom_addons  # Carpeta personalizada de addons
# o si ya existe la carpeta addons de Odoo:
cd ~/dockercompose/addons
```

3. Si quieres trabajar dentro del contenedor de Odoo:

```bash
docker compose exec web bash  # 'web' es el servicio de Odoo
cd /mnt/extra-addons
```

---

## 2. Crear la estructura del módulo

Supongamos que el módulo se llamará `mi_modulo`.

```bash
mkdir -p mi_modulo/models
cd mi_modulo
```

Estructura mínima:

```
mi_modulo/
├── __init__.py
├── __manifest__.py
└── models/
    ├── __init__.py
    └── mi_modelo.py
```

---

## 3. Crear archivos del módulo

### a) `__init__.py` del módulo

```bash
echo "from . import models" > __init__.py
```

### b) `__manifest__.py` (manifiesto)

```bash
cat > __manifest__.py <<EOF
{
    "name": "Mi Módulo",
    "version": "1.0",
    "summary": "Módulo de prueba desde terminal",
    "description": "Este módulo fue creado desde la terminal",
    "author": "Tu Nombre",
    "depends": ["base"],
    "data": [],
    "installable": True,
    "application": True
}
EOF
```

### c) `models/__init__.py`

```bash
echo "from . import mi_modelo" > models/__init__.py
```

### d) `models/mi_modelo.py`

```bash
cat > models/mi_modelo.py <<EOF
from odoo import models, fields

class MiModelo(models.Model):
    _name = "mi.modulo"
    _description = "Modelo de prueba"

    name = fields.Char(string="Nombre", required=True)
    descripcion = fields.Text(string="Descripción")
EOF
```

---

## 4. Reiniciar Odoo para detectar el módulo

Desde la **terminal del host** (no dentro del contenedor):

```bash
docker compose restart web
```

* `web` es el nombre del servicio de Odoo.

---

## 5. Instalar el módulo desde la interfaz web

1. Abre tu navegador y ve a la IP de Odoo, por ejemplo:

```
http://192.168.5.124:8069
```

2. Activa **modo desarrollador**: Configuración → Activar Developer Mode.
3. Ve a **Apps → Update Apps List** → Confirmar.
4. Busca `Mi Módulo` y haz clic en **Instalar**.

---

## 6. Verificar que el módulo está activo

* Una vez instalado, podrás usar el modelo `mi.modulo` y sus campos (`name` y `descripcion`) desde la interfaz web.
* También puedes listar los addons reconocidos desde el contenedor:

```bash
docker compose exec web bash
odoo -c /etc/odoo/odoo.conf --list-addons
```

---

**¡Listo!** Ahora tienes un módulo mínimo de Odoo creado totalmente desde la terminal en Linux y listo para instalar y probar.

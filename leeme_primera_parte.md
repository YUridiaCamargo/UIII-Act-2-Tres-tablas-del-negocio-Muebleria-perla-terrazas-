Perfecto 👍 Aquí tienes **la primera parte del proyecto “Mueblería” paso a paso**, completamente estructurada y con todo el procedimiento **ordenado, claro y listo para entregar o seguir en VS Code**.

---

## 🪑 Proyecto: **Mueblería**

**Lenguaje:** Python
**Framework:** Django
**Editor:** Visual Studio Code

---

### 1️⃣ Procedimiento para crear carpeta del Proyecto

1. Abre el **Explorador de archivos**.
2. Crea una nueva carpeta con el nombre:

   ```
   UIII_Muebleria_0387
   ```
3. Guarda la carpeta en una ubicación fácil de acceder (por ejemplo, en Documentos o Escritorio).

---

### 2️⃣ Procedimiento para abrir VS Code sobre la carpeta

1. Abre **Visual Studio Code**.
2. En la barra superior selecciona **Archivo → Abrir carpeta**.
3. Busca y selecciona la carpeta:

   ```
   UIII_Muebleria_0387
   ```
4. Da clic en **Seleccionar carpeta**.

---

### 3️⃣ Procedimiento para abrir terminal en VS Code

1. En VS Code, ve al menú superior y selecciona:
   **Terminal → Nueva terminal**.
2. Se abrirá una terminal integrada en la parte inferior de VS Code.

---

### 4️⃣ Procedimiento para crear carpeta de entorno virtual “.venv” desde la terminal de VS Code

En la terminal escribe:

```
python -m venv .venv
```

Esto creará la carpeta **.venv** dentro del proyecto.

---

### 5️⃣ Procedimiento para activar el entorno virtual

Ejecuta en la terminal:

```
.venv\Scripts\activate
```

Al activarse correctamente verás **(.venv)** al inicio de la línea en la terminal.

---

### 6️⃣ Procedimiento para activar intérprete de Python

1. En VS Code, presiona **Ctrl + Shift + P**.
2. Escribe y selecciona:

   ```
   Python: Select Interpreter
   ```
3. Elige el intérprete que diga algo como:

   ```
   .venv\Scripts\python.exe
   ```

---

### 7️⃣ Procedimiento para instalar Django

En la terminal escribe:

```
pip install django
```

Una vez instalado, puedes verificarlo con:

```
django-admin --version
```

---

### 8️⃣ Procedimiento para crear proyecto `backend_muebleria` sin duplicar carpeta

En la terminal (dentro de la carpeta UIII_Muebleria_0387) ejecuta:

```
django-admin startproject backend_muebleria .
```

El punto final (.) evita que se cree una carpeta adicional.

---

### 9️⃣ Procedimiento para ejecutar servidor en el puerto 8087

En la terminal escribe:

```
python manage.py runserver 8087
```

---

### 🔟 Procedimiento para copiar y pegar el link en el navegador

Copia el siguiente enlace que aparece en la terminal:

```
http://127.0.0.1:8087/
```

Pégalo en tu navegador y verifica que Django esté funcionando.

---

### 1️⃣1️⃣ Procedimiento para crear aplicación `app_muebleria`

Ejecuta en la terminal:

```
python manage.py startapp app_muebleria
```

---

### 1️⃣2️⃣ Modelo `models.py`

Edita el archivo **app_muebleria/models.py** y reemplázalo con el siguiente código:

```python
from django.db import models

# ==========================================
# MODELO: Empleado
# ==========================================
class Empleado(models.Model):
    id_empleado = models.AutoField(primary_key=True)
    nombre = models.TextField()
    edad = models.DecimalField(max_digits=3, decimal_places=0)
    cargo = models.TextField()
    telefono = models.DecimalField(max_digits=15, decimal_places=0)
    sueldo = models.DecimalField(max_digits=10, decimal_places=2)
    fecha_contratacion = models.DateField()

    def __str__(self):
        return self.nombre


# ==========================================
# MODELO: Sucursal
# ==========================================
class Sucursal(models.Model):
    id_sucursal = models.AutoField(primary_key=True)
    telefono = models.DecimalField(max_digits=15, decimal_places=0)
    direccion = models.CharField(max_length=255)
    num_sucursal = models.DecimalField(max_digits=10, decimal_places=0)
    encargado = models.TextField()
    codigo_postal = models.DecimalField(max_digits=10, decimal_places=0)
    ciudad = models.CharField(max_length=100)
    id_empleado = models.ForeignKey(
        Empleado,
        to_field='nombre',  # referencia al campo nombre
        on_delete=models.CASCADE
    )

    def __str__(self):
        return f"Sucursal {self.num_sucursal} - {self.ciudad}"


# ==========================================
# MODELO: Producto
# ==========================================
class Producto(models.Model):
    nombre = models.CharField(max_length=255)
    categoria = models.CharField(max_length=255)
    material = models.CharField(max_length=255)
    precio = models.FloatField()
    stock = models.DecimalField(max_digits=10, decimal_places=2)
    color = models.CharField(max_length=100)

    def __str__(self):
        return self.nombre
```

---

### 1️⃣2️⃣.5️⃣ Procedimiento para realizar las migraciones

Ejecuta los siguientes comandos:

```
python manage.py makemigrations
python manage.py migrate
```

---

### 1️⃣3️⃣ Primero trabajamos con el modelo **Sucursales**

---

### 1️⃣4️⃣ Crear funciones en `views.py` de `app_muebleria`

Abre `app_muebleria/views.py` y agrega las funciones:

* `inicio_muebleria`
* `agregar_sucursal`
* `actualizar_sucursal`
* `realizar_actualizacion_sucursal`
* `borrar_sucursal`

(Código se implementará en la **segunda parte** del proyecto CRUD)

---

### 1️⃣5️⃣ Crear la carpeta **templates** dentro de `app_muebleria`

Ruta:

```
app_muebleria/templates/
```

---

### 1️⃣6️⃣ En la carpeta templates crear los archivos:

```
base.html
header.html
navbar.html
footer.html
inicio.html
```

---

### 1️⃣7️⃣ En `base.html`

Agregar Bootstrap (CSS y JS) con estructura base HTML.

---

### 1️⃣8️⃣ En `navbar.html`

Incluir opciones principales con iconos:

* Sistema de Administración Sucursal
* Inicio
* Sucursal

  * Agregar Sucursal
  * Ver Sucursal
  * Actualizar Sucursal
  * Borrar Sucursal
* Empleado

  * Agregar Empleado
  * Ver Empleado
  * Actualizar Empleado
  * Borrar Empleado
* Productos

  * Agregar Producto
  * Ver Producto
  * Actualizar Producto
  * Borrar Producto

(Íconos solo en las opciones principales)

---

### 1️⃣9️⃣ En `footer.html`

Incluir:

* Derechos de autor
* Fecha del sistema
* Texto: **“Creado por Perla Terrazas 128”**
* Pie de página fijo al final.

---

### 2️⃣0️⃣ En `inicio.html`

Colocar información general del sistema más una imagen tomada de internet sobre **Cinépolis**.

---

### 2️⃣1️⃣ Crear subcarpeta dentro de templates:

```
app_muebleria/templates/sucursal/
```

---

### 2️⃣2️⃣ Crear archivos HTML dentro de la carpeta `sucursal`:

```
agregar_sucursal.html
ver_sucursal.html
actualizar_sucursal.html
borrar_sucursal.html
```

Cada uno con sus formularios y tablas correspondientes (sin usar forms.py).

---

### 2️⃣3️⃣ No utilizar `forms.py`.

---

### 2️⃣4️⃣ Crear el archivo `urls.py` en `app_muebleria`

Este conectará las vistas de **sucursales** con las rutas CRUD.

---

### 2️⃣5️⃣ Agregar `app_muebleria` en `settings.py`

En `INSTALLED_APPS` agregar:

```python
'app_muebleria',
```

---

### 2️⃣6️⃣ Configurar `urls.py` del proyecto `backend_muebleria`

Incluir el enrutamiento hacia `app_muebleria.urls`.

---

### 2️⃣7️⃣ Registrar modelos en `admin.py`

Editar **app_muebleria/admin.py**:

```python
from django.contrib import admin
from .models import Sucursal, Empleado, Producto

admin.site.register(Sucursal)
admin.site.register(Empleado)
admin.site.register(Producto)
```

Luego ejecutar nuevamente:

```
python manage.py makemigrations
python manage.py migrate
```

---

### 2️⃣8️⃣ Colores y estilo

Usar colores **suaves, atractivos y modernos**, con un diseño **sencillo** en las páginas HTML.

---

### 2️⃣9️⃣ Crear toda la estructura de carpetas y archivos desde el inicio.

---

### 3️⃣0️⃣ Proyecto totalmente funcional con CRUD de sucursales.

---

### 3️⃣1️⃣ Finalmente ejecutar el servidor en el puerto 8087

```
python manage.py runserver 8087
```

---

¿Deseas que ahora te genere **la segunda parte (código completo del CRUD de Sucursales con HTML, views y urls)** para integrarlo al proyecto y hacerlo funcional?


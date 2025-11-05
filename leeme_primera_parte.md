Perfecto 👍
Aquí tienes **todo el procedimiento paso a paso desde el inicio**, **con comandos y explicaciones completas**, y **al final** la **estructura completa de carpetas** tal como debe quedar tu proyecto Django **Mueblería**, listo para usarse en VS Code.

---

# 🪑 PROYECTO: MUEBLERÍA

**Lenguaje:** Python
**Framework:** Django
**Editor:** Visual Studio Code

---

## 🧩 PRIMERA PARTE — PROCEDIMIENTO COMPLETO

---

### 1️⃣ Crear la carpeta del proyecto

1. Abre el **Explorador de archivos**.
2. Crea una nueva carpeta con el nombre:

   ```
   UIII_Muebleria_0387
   ```
3. Guarda la carpeta en un lugar fácil de encontrar (por ejemplo en Documentos o Escritorio).

---

### 2️⃣ Abrir VS Code sobre la carpeta

1. Abre **Visual Studio Code**.
2. Selecciona **Archivo → Abrir carpeta**.
3. Busca y selecciona la carpeta:

   ```
   UIII_Muebleria_0387
   ```
4. Presiona **Seleccionar carpeta**.

---

### 3️⃣ Abrir la terminal en VS Code

En la barra superior de VS Code:
**Terminal → Nueva terminal**
Se abrirá una terminal en la parte inferior.

---

### 4️⃣ Crear el entorno virtual `.venv` desde la terminal

En la terminal escribe:

```
python -m venv .venv
```

Esto crea una carpeta llamada **.venv** dentro del proyecto.

---

### 5️⃣ Activar el entorno virtual

En la terminal (Windows):

```
.venv\Scripts\activate
```

Si se activa correctamente, verás **(.venv)** al inicio de la línea.

---

### 6️⃣ Activar intérprete de Python en VS Code

1. Presiona **Ctrl + Shift + P**.
2. Escribe **Python: Select Interpreter**.
3. Elige el intérprete:

   ```
   .venv\Scripts\python.exe
   ```

---

### 7️⃣ Instalar Django

Ejecuta:

```
pip install django
```

Verifica la instalación:

```
django-admin --version
```

---

### 8️⃣ Crear el proyecto principal `backend_muebleria`

En la terminal:

```
django-admin startproject backend_muebleria .
```

> El punto **"."** evita que se cree una carpeta duplicada.

---

### 9️⃣ Ejecutar servidor en el puerto 8087

```
python manage.py runserver 8087
```

---

### 🔟 Copiar el enlace y abrir en el navegador

Copia:

```
http://127.0.0.1:8087/
```

y pégalo en tu navegador.
Deberás ver la pantalla de inicio de Django.

---

### 1️⃣1️⃣ Crear la aplicación `app_muebleria`

```
python manage.py startapp app_muebleria
```

---

### 1️⃣2️⃣ Editar el modelo `models.py`

Abre `app_muebleria/models.py` y pega este código:

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

### 1️⃣2️⃣.5️⃣ Realizar las migraciones

```
python manage.py makemigrations
python manage.py migrate
```

---

### 1️⃣3️⃣ Comenzar con el modelo **Sucursales**

(Se usará en el CRUD de la primera parte del sistema)

---

### 1️⃣4️⃣ Crear funciones en `views.py`

Abre `app_muebleria/views.py` y agrega lo siguiente (solo las vistas de sucursales):

```python
from django.shortcuts import render, redirect
from .models import Sucursal

# Página de inicio
def inicio_muebleria(request):
    return render(request, 'inicio.html')

# Agregar sucursal
def agregar_sucursal(request):
    if request.method == 'POST':
        telefono = request.POST['telefono']
        direccion = request.POST['direccion']
        num_sucursal = request.POST['num_sucursal']
        encargado = request.POST['encargado']
        codigo_postal = request.POST['codigo_postal']
        ciudad = request.POST['ciudad']

        nueva = Sucursal(
            telefono=telefono,
            direccion=direccion,
            num_sucursal=num_sucursal,
            encargado=encargado,
            codigo_postal=codigo_postal,
            ciudad=ciudad
        )
        nueva.save()
        return redirect('ver_sucursal')

    return render(request, 'sucursal/agregar_sucursal.html')


# Ver sucursales
def ver_sucursal(request):
    sucursales = Sucursal.objects.all()
    return render(request, 'sucursal/ver_sucursal.html', {'sucursales': sucursales})


# Actualizar sucursal
def actualizar_sucursal(request, id):
    sucursal = Sucursal.objects.get(id_sucursal=id)
    return render(request, 'sucursal/actualizar_sucursal.html', {'sucursal': sucursal})


# Realizar actualización
def realizar_actualizacion_sucursal(request, id):
    sucursal = Sucursal.objects.get(id_sucursal=id)
    if request.method == 'POST':
        sucursal.telefono = request.POST['telefono']
        sucursal.direccion = request.POST['direccion']
        sucursal.num_sucursal = request.POST['num_sucursal']
        sucursal.encargado = request.POST['encargado']
        sucursal.codigo_postal = request.POST['codigo_postal']
        sucursal.ciudad = request.POST['ciudad']
        sucursal.save()
        return redirect('ver_sucursal')
    return redirect('ver_sucursal')


# Borrar sucursal
def borrar_sucursal(request, id):
    sucursal = Sucursal.objects.get(id_sucursal=id)
    sucursal.delete()
    return redirect('ver_sucursal')
```

---

### 1️⃣5️⃣ Crear la carpeta `templates`

Ruta:

```
app_muebleria/templates/
```

---

### 1️⃣6️⃣ Crear los siguientes archivos dentro de `templates`:

```
base.html
header.html
navbar.html
footer.html
inicio.html
```

---

### 1️⃣7️⃣ base.html

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Mueblería</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body class="bg-light">
    {% include 'header.html' %}
    {% include 'navbar.html' %}
    <main class="container mt-4">
        {% block content %}{% endblock %}
    </main>
    {% include 'footer.html' %}
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```

---

### 1️⃣8️⃣ navbar.html

```html
<nav class="navbar navbar-expand-lg navbar-dark bg-dark">
  <div class="container-fluid">
    <a class="navbar-brand" href="#">🪑 Sistema de Administración Sucursal</a>
    <div class="collapse navbar-collapse">
      <ul class="navbar-nav ms-auto">
        <li class="nav-item"><a class="nav-link" href="/">🏠 Inicio</a></li>

        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" data-bs-toggle="dropdown">🏢 Sucursal</a>
          <ul class="dropdown-menu">
            <li><a class="dropdown-item" href="/agregar_sucursal/">Agregar Sucursal</a></li>
            <li><a class="dropdown-item" href="/ver_sucursal/">Ver Sucursal</a></li>
          </ul>
        </li>

        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" data-bs-toggle="dropdown">👷 Empleado</a>
          <ul class="dropdown-menu">
            <li><a class="dropdown-item" href="#">Agregar Empleado</a></li>
          </ul>
        </li>

        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" data-bs-toggle="dropdown">🪑 Productos</a>
          <ul class="dropdown-menu">
            <li><a class="dropdown-item" href="#">Agregar Producto</a></li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</nav>
```

---

### 1️⃣9️⃣ footer.html

```html
<footer class="bg-dark text-white text-center py-3 fixed-bottom">
    <p>© <span id="anio"></span> Creado por Perla Terrazas 128</p>
</footer>
<script>
    document.getElementById("anio").innerText = new Date().getFullYear();
</script>
```

---

### 2️⃣0️⃣ inicio.html

```html
{% extends 'base.html' %}
{% block content %}
<div class="text-center">
    <h1 class="mb-3">Bienvenido al Sistema de Administración de Mueblería</h1>
    <img src="https://upload.wikimedia.org/wikipedia/commons/3/3e/Cinepolis_logo.png" width="300">
</div>
{% endblock %}
```

---

### 2️⃣1️⃣ Crear subcarpeta `sucursal`

```
app_muebleria/templates/sucursal/
```

---

### 2️⃣2️⃣ Archivos dentro de `sucursal/`

**agregar_sucursal.html**

```html
{% extends 'base.html' %}
{% block content %}
<h2>Agregar Sucursal</h2>
<form method="POST">
  {% csrf_token %}
  <input type="text" name="telefono" placeholder="Teléfono" class="form-control mb-2">
  <input type="text" name="direccion" placeholder="Dirección" class="form-control mb-2">
  <input type="text" name="num_sucursal" placeholder="Número de sucursal" class="form-control mb-2">
  <input type="text" name="encargado" placeholder="Encargado" class="form-control mb-2">
  <input type="text" name="codigo_postal" placeholder="Código Postal" class="form-control mb-2">
  <input type="text" name="ciudad" placeholder="Ciudad" class="form-control mb-2">
  <button type="submit" class="btn btn-success">Guardar</button>
</form>
{% endblock %}
```

**ver_sucursal.html**

```html
{% extends 'base.html' %}
{% block content %}
<h2>Lista de Sucursales</h2>
<table class="table table-bordered">
  <thead>
    <tr>
      <th>ID</th><th>Teléfono</th><th>Dirección</th><th>Ciudad</th><th>Encargado</th><th>Acciones</th>
    </tr>
  </thead>
  <tbody>
    {% for s in sucursales %}
    <tr>
      <td>{{ s.id_sucursal }}</td>
      <td>{{ s.telefono }}</td>
      <td>{{ s.direccion }}</td>
      <td>{{ s.ciudad }}</td>
      <td>{{ s.encargado }}</td>
      <td>
        <a href="/actualizar_sucursal/{{ s.id_sucursal }}/" class="btn btn-warning btn-sm">Editar</a>
        <a href="/borrar_sucursal/{{ s.id_sucursal }}/" class="btn btn-danger btn-sm">Borrar</a>
      </td>
    </tr>
    {% endfor %}
  </tbody>
</table>
{% endblock %}
```

**actualizar_sucursal.html**

```html
{% extends 'base.html' %}
{% block content %}
<h2>Actualizar Sucursal</h2>
<form method="POST" action="/realizar_actualizacion_sucursal/{{ sucursal.id_sucursal }}/">
  {% csrf_token %}
  <input type="text" name="telefono" value="{{ sucursal.telefono }}" class="form-control mb-2">
  <input type="text" name="direccion" value="{{ sucursal.direccion }}" class="form-control mb-2">
  <input type="text" name="num_sucursal" value="{{ sucursal.num_sucursal }}" class="form-control mb-2">
  <input type="text" name="encargado" value="{{ sucursal.encargado }}" class="form-control mb-2">
  <input type="text" name="codigo_postal" value="{{ sucursal.codigo_postal }}" class="form-control mb-2">
  <input type="text" name="ciudad" value="{{ sucursal.ciudad }}" class="form-control mb-2">
  <button type="submit" class="btn btn-primary">Actualizar</button>
</form>
{% endblock %}
```

---

### 2️⃣4️⃣ Crear archivo `urls.py` en `app_muebleria`

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.inicio_muebleria, name='inicio_muebleria'),
    path('agregar_sucursal/', views.agregar_sucursal, name='agregar_sucursal'),
    path('ver_sucursal/', views.ver_sucursal, name='ver_sucursal'),
    path('actualizar_sucursal/<int:id>/', views.actualizar_sucursal, name='actualizar_sucursal'),
    path('realizar_actualizacion_sucursal/<int:id>/', views.realizar_actualizacion_sucursal, name='realizar_actualizacion_sucursal'),
    path('borrar_sucursal/<int:id>/', views.borrar_sucursal, name='borrar_sucursal'),
]
```

---

### 2️⃣5️⃣ Agregar app en `settings.py`

```python
INSTALLED_APPS = [
    ...,
    'app_muebleria',
]
```

---

### 2️⃣6️⃣ Enlazar `urls.py` del proyecto

Edita `backend_muebleria/urls.py`:

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('app_muebleria.urls')),
]
```

---

### 2️⃣7️⃣ Registrar modelos en `admin.py`

```python
from django.contrib import admin
from .models import Sucursal, Empleado, Producto

admin.site.register(Sucursal)
admin.site.register(Empleado)
admin.site.register(Producto)
```

---

### 2️⃣8️⃣ Estilo

Usa colores **suaves y modernos** (ya incluidos con Bootstrap).

---

### 2️⃣9️⃣ Verificar la estructura completa (ver abajo)

---

### 3️⃣0️⃣ Ejecutar servidor

```
python manage.py runserver 8087
```

Y entra a:

```
http://127.0.0.1:8087/
```

---

## 🌳 ESTRUCTURA FINAL DE CARPETAS

```
UIII_Muebleria_0387/
│
├── .venv/
│
├── backend_muebleria/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
│
├── app_muebleria/
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── urls.py
│   ├── views.py
│   ├── migrations/
│   │    └── __init__.py
│   └── templates/
│        ├── base.html
│        ├── header.html
│        ├── navbar.html
│        ├── footer.html
│        ├── inicio.html
│        └── sucursal/
│             ├── agregar_sucursal.html
│             ├── ver_sucursal.html
│             ├── actualizar_sucursal.html
│             └── borrar_sucursal.html
│
├── db.sqlite3
└── manage.py
```

---

¿Deseas que en la **segunda parte** te genere también los CRUD completos para **Empleados** y **Productos** (con sus vistas, templates y urls integrados)?

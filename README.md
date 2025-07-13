# Preguntas y Respuestas sobre Django

## 1. ¿Qué es un CRUD y cuál es su propósito en el desarrollo de aplicaciones web?

CRUD significa **Create, Read, Update, Delete** (Crear, Leer, Actualizar, Eliminar). Es un conjunto de operaciones básicas para gestionar datos en una aplicación, típicamente en interacción con una base de datos. Su propósito es proporcionar una estructura estándar para manipular datos de manera eficiente y organizada en aplicaciones web.

- **Create**: Crear nuevos registros (ejemplo: registrar un nuevo usuario).
- **Read**: Consultar o recuperar datos (ejemplo: mostrar una lista de usuarios).
- **Update**: Modificar datos existentes (ejemplo: actualizar el correo de un usuario).
- **Delete**: Eliminar registros (ejemplo: eliminar una cuenta de usuario).

Ejemplo de aplicación web que usa CRUD: Un sistema de gestión de tareas (como Trello). Los usuarios pueden:
- Crear una nueva tarea.
- Leer la lista de tareas.
- Actualizar el estado o descripción de una tarea.
- Eliminar tareas completadas.

## 2. ¿Qué son los patrones de arquitectura en desarrollo de software?

### ¿Qué es el patrón MVC (Modelo–Vista–Controlador)?

MVC organiza la aplicación en tres componentes principales:

- **Modelo**: Representa los datos y la lógica de negocio. Interactúa con la base de datos.
- **Vista**: Muestra los datos al usuario (interfaz gráfica).
- **Controlador**: Maneja las interacciones del usuario, conectando el Modelo con la Vista.

### ¿Qué es el patrón MVT (Modelo–Vista–Template)?

MVT es una variante de MVC utilizada en Django:

- **Modelo**: Similar al Modelo de MVC, maneja los datos y la lógica de negocio.
- **Vista**: Define la lógica de procesamiento (similar al Controlador de MVC), decide qué datos mostrar.
- **Template**: Representa la interfaz de usuario (similar a la Vista de MVC).

### Diferencias entre MVC y MVT

| Aspecto     | MVC                        | MVT                        |
|-------------|----------------------------|----------------------------|
| Componentes | Modelo, Vista, Controlador | Modelo, Vista, Template    |
| Rol de Vista| Interfaz de usuario        | Lógica de procesamiento    |
| Controlador | Gestiona lógica y flujo    | No existe; la lógica está en la Vista |
| Template    | No aplica                  | Define la interfaz de usuario |
| Ejemplo de uso | Frameworks como Ruby on Rails | Framework Django |

### ¿Cuál de estos dos patrones se usa en Django?

Django utiliza el patrón MVT (Modelo–Vista–Template).

## 3. ¿Cómo se estructura un proyecto en Django? Explicar brevemente el rol de los modelos, vistas, templates y URLs.

Un proyecto en Django se organiza en una estructura modular que incluye archivos y carpetas con roles específicos:

- **Modelos**: Definen la estructura de la base de datos (tablas, campos, relaciones). Usa clases de Python que heredan de `django.db.models.Model`.
- **Vistas**: Contienen la lógica para procesar solicitudes HTTP y devolver respuestas. Pueden ser funciones o clases.
- **Templates**: Archivos HTML con marcadores dinámicos para renderizar datos.
- **URLs**: Mapean URLs a Vistas mediante patrones definidos en `urls.py`.

### ¿Para qué se usa el signo “%%” en los templates?

En los templates de Django, el signo `{% %}` se usa para etiquetas de template que ejecutan lógica, como bucles, condiciones o inclusión de otros templates. Por ejemplo:
- `{% for item in items %}`: Inicia un bucle.
- `{% if condition %}`: Evalúa una condición.
- `{% include 'template.html' %}`: Incluye otro template.

## 4. ¿Cuál es el flujo de datos entre un formulario HTML y la base de datos en Django?

El flujo de datos en Django sigue estos pasos:

1. **Formulario HTML**: El usuario completa un formulario en el navegador (Template).
2. **Solicitud HTTP**: Al enviar el formulario, se genera una solicitud POST con los datos.
3. **URL y Vista**: La solicitud es dirigida a una Vista a través de `urls.py`.
4. **Procesamiento en la Vista**: La Vista valida los datos (usando un Form o ModelForm).
5. **Interacción con el Modelo**: Si los datos son válidos, la Vista interactúa con el Modelo para guardar o actualizar datos en la base de datos.
6. **Respuesta**: La Vista devuelve una respuesta (nuevo Template, redirección, etc.).

## 5. ¿Qué herramientas o comandos ofrece Django para facilitar el desarrollo de un CRUD, para qué es cada una?

Django ofrece herramientas y comandos que simplifican la creación de un CRUD:

- **startapp**: Crea una nueva aplicación dentro del proyecto (`python manage.py startapp nombre_app`).
- **makemigrations**: Genera archivos de migración basados en cambios en los Modelos (`python manage.py makemigrations`).
- **migrate**: Aplica las migraciones para actualizar la base de datos (`python manage.py migrate`).
- **runserver**: Inicia un servidor de desarrollo local (`python manage.py runserver`).
- **ModelForm**: Permite crear formularios directamente desde Modelos, facilitando la validación y el guardado de datos.
- **admin**: Proporciona una interfaz administrativa automática para gestionar datos (CRUD) sin escribir código adicional.

## 6. ¿Cómo funciona el Admin de Django?

El Admin de Django es una interfaz administrativa generada automáticamente que permite realizar operaciones CRUD sobre los Modelos registrados. Funciona así:

- **Configuración**: En `admin.py`, se registran los Modelos con `admin.site.register(Modelo)`.
- **Personalización**: Se pueden definir clases como `ModeloAdmin` para personalizar la interfaz (campos mostrados, filtros, etc.).
- **Acceso**: Los usuarios con permisos de administrador acceden a `/admin` y gestionan datos mediante formularios y listas generadas automáticamente.
- **Seguridad**: Requiere autenticación y permite gestionar permisos de usuario.

---

# Proyecto Monolítico en Django: Sistema de Gestión de Libros

## Índice

1. Introducción a Django
2. El Admin de Django
3. Configuración del Proyecto
4. Creación de Modelos
5. Configuración del Admin
6. Creación de Vistas
7. Configuración de URLs
8. Creación de Plantillas
9. Ejecución del Proyecto

## Introducción a Django

Django es un framework de desarrollo web de alto nivel escrito en Python que fomenta el desarrollo rápido y el diseño limpio y pragmático. Fue creado para facilitar la creación de aplicaciones web complejas, orientadas a bases de datos.

Características principales de Django:

- Sigue el patrón de diseño Modelo-Vista-Template (MVT)
- Incluye un ORM (Object-Relational Mapping) potente
- Proporciona un panel de administración automático
- Tiene un sistema de autenticación incorporado
- Ofrece un framework de migración de bases de datos

Django se utiliza para desarrollar todo tipo de aplicaciones web, desde sistemas de gestión de contenidos y wikis hasta redes sociales y plataformas de noticias.

## El Admin de Django

El Admin de Django es una de las características más poderosas del framework. Es una interfaz de administración generada automáticamente que lee los metadatos de tus modelos para proporcionar una interfaz potente y lista para producción, donde los usuarios autorizados pueden gestionar el contenido de tu sitio.

Características del Admin de Django:

- Generación automática de interfaces CRUD para los modelos
- Sistemas de autenticación y autorización incorporados
- Personalización de la apariencia y el comportamiento
- Filtros y búsquedas avanzadas
- Gestión de relaciones entre modelos

El Admin de Django es especialmente útil para crear rápidamente una interfaz de gestión interna para tu aplicación o para prototipar un proyecto.

## Configuración del Proyecto

1. Instala Django:
   ```bash
   pip install django
   ```

2. Crea un nuevo proyecto Django:
   ```bash
   django-admin startproject sistema_libros
   cd sistema_libros
   ```

Esta será tu estructura una vez creadas las aplicaciones:

```
crud_python/ # Carpeta donde guardas tu proyecto
│
├── manage.py
├── libreria/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
│
├── libros/
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── forms.py
│   ├── serializer.py
│   ├── tests.py
│   ├── urls.py 
│   ├── views.py
```

3. Crea una nueva aplicación:
   ```bash
   python manage.py startapp libros
   ```

4. Agrega 'libros' a `INSTALLED_APPS` en `sistema_libros/settings.py`:

   ```python
   INSTALLED_APPS = [
       'django.contrib.admin',
       'django.contrib.auth',
       'django.contrib.contenttypes',
       'django.contrib.sessions',
       'django.contrib.messages',
       'django.contrib.staticfiles',
       'libros',
   ]
   ```

## Creación de Modelos

En `libros/models.py`, crea el modelo Libro:

```python
from django.db import models

class Libro(models.Model):
    titulo = models.CharField(max_length=200)
    autor = models.CharField(max_length=100)
    descripcion = models.TextField()
    fecha_publicacion = models.DateField()
    isbn = models.CharField(max_length=13, unique=True)

    def __str__(self):
        return self.titulo
```

Realiza las migraciones:

```bash
python manage.py makemigrations
python manage.py migrate
```

## Configuración del Admin

En `libros/admin.py`, registra el modelo Libro:

```python
from django.contrib import admin
from .models import Libro

@admin.register(Libro)
class LibroAdmin(admin.ModelAdmin):
    list_display = ('titulo', 'autor', 'fecha_publicacion', 'isbn')
    search_fields = ('titulo', 'autor', 'isbn')
    list_filter = ('fecha_publicacion',)
```

## Creación de Vistas

En `libros/views.py`, crea las vistas para listar y detallar libros:

```python
from django.shortcuts import render, get_object_or_404, redirect
from .models import Libro
from .forms import LibroForm

def lista_libros(request):
    libros = Libro.objects.all()
    return render(request, 'libros/lista_libros.html', {'libros': libros})

def detalle_libro(request, libro_id):
    libro = get_object_or_404(Libro, pk=libro_id)
    return render(request, 'libros/detalle_libro.html', {'libro': libro})

def crear_libro(request):
    if request.method == 'POST':
        form = LibroForm(request.POST)
        if form.is_valid():
            form.save()
            return redirect('lista_libros')
    else:
        form = LibroForm()
    return render(request, 'libros/crear_libro.html', {'form': form})

def editar_libro(request, libro_id):
    libro = get_object_or_404(Libro, pk=libro_id)
    if request.method == 'POST':
        form = LibroForm(request.POST, instance=libro)
        if form.is_valid():
            form.save()
            return redirect('detalle_libro', libro_id=libro.id)
    else:
        form = LibroForm(instance=libro)
    return render(request, 'libros/editar_libro.html', {'form': form, 'libro': libro})

def eliminar_libro(request, libro_id):
    libro = get_object_or_404(Libro, pk=libro_id)
    if request.method == 'POST':
        libro.delete()
        return redirect('lista_libros')
    return render(request, 'libros/eliminar_libro.html', {'libro': libro})
```

## Creación de Forms

En `libros/forms.py`, crea el formulario para tus vistas de crear y modificar/actualizar libros:

```python
from django import forms
from .models import Libro

class LibroForm(forms.ModelForm):
    class Meta:
        model = Libro
        fields = ['titulo', 'autor', 'descripcion', 'fecha_publicacion', 'isbn']
```

## Configuración de URLs

En `sistema_libros/urls.py`:

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('libros/', include('libros.urls')),
]
```

Crea `libros/urls.py`:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.lista_libros, name='lista_libros'),
    path('<int:libro_id>/', views.detalle_libro, name='detalle_libro'),
    path('crear/', views.crear_libro, name='crear_libro'),
    path('<int:libro_id>/editar/', views.editar_libro, name='editar_libro'),
    path('<int:libro_id>/eliminar/', views.eliminar_libro, name='eliminar_libro'),
]
```

## Creación de Plantillas

Crea las siguientes plantillas:

### `libros/templates/libros/lista_libros.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Lista de Libros</title>
</head>
<body>
    <h1>Lista de Libros</h1>
    <ul>
    {% for libro in libros %}
        <li><a href="{% url 'detalle_libro' libro.id %}">{{ libro.titulo }}</a></li>
    {% endfor %}
    </ul>
</body>
</html>
```

### `libros/templates/libros/detalle_libro.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>{{ libro.titulo }}</title>
</head>
<body>
    <h1>{{ libro.titulo }}</h1>
    <p>Autor: {{ libro.autor }}</p>
    <p>Descripción: {{ libro.descripcion }}</p>
    <p>Fecha de publicación: {{ libro.fecha_publicacion }}</p>
    <p>ISBN: {{ libro.isbn }}</p>
    <a href="{% url 'lista_libros' %}">Volver a la lista</a>
</body>
</html>
```

### `libros/templates/libros/editar_libro.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Editar {{ libro.titulo }}</title>
</head>
<body>
    <h1>Editar {{ libro.titulo }}</h1>
    <form method="post">
        {% csrf_token %}
        {{ form.as_p }}
        <button type="submit">Guardar cambios</button>
    </form>
    <a href="{% url 'detalle_libro' libro.id %}">Cancelar</a>
</body>
</html>
```

### `libros/templates/libros/crear_libro.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Crear Libro</title>
</head>
<body>
    <h1>Crear Libro</h1>
    <form method="post">
        {% csrf_token %}
        {{ form.as_p }}
        <button type="submit">Guardar</button>
    </form>
    <a href="{% url 'lista_libros' %}">Cancelar</a>
</body>
</html>
```

### `libros/templates/libros/eliminar_libro.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Eliminar {{ libro.titulo }}</title>
</head>
<body>
    <h1>Eliminar {{ libro.titulo }}</h1>
    <p>¿Estás seguro de que quieres eliminar este libro?</p>
    <form method="post">
        {% csrf_token %}
        <button type="submit">Sí, eliminar</button>
    </form>
    <a href="{% url 'detalle_libro' libro.id %}">Cancelar</a>
</body>
</html>
```

## Ejecución del Proyecto

1. Crea un superusuario para acceder al admin:
   ```bash
   python manage.py createsuperuser
   ```

2. Inicia el servidor de desarrollo:
   ```bash
   python manage.py runserver
   ```

3. Accede al admin en [http://localhost:8000/admin/](http://localhost:8000/admin/) y añade algunos libros.

4. Visita [http://localhost:8000/libros/](http://localhost:8000/libros/) para ver la lista de libros y [http://localhost:8000/libros/1/](http://localhost:8000/libros/1/) para ver los detalles de un libro (reemplaza '1' con el ID de un libro existente).
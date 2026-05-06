# OmniLatam — E-commerce API

API REST construida con Django y Django REST Framework como parte de una prueba técnica para OmniLatam. Implementa el backend de un e-commerce básico con catálogo de productos, gestión de órdenes y persistencia en PostgreSQL, todo orquestado con Docker.

> 📌 Proyecto creado en 2021. Refleja mis fundamentos de Django y arquitectura de APIs en ese momento. Los proyectos más recientes muestran prácticas actualizadas.

---

## 🧩 Stack técnico

- **Backend:** Python 3.x · Django · Django REST Framework
- **Base de datos:** PostgreSQL
- **Contenedores:** Docker · Docker Compose
- **Build / tareas:** Makefile

---

## 🏗️ Arquitectura

```
.
├── RETO/              # Aplicación Django principal (settings, urls, wsgi)
├── Prueba/            # Apps con la lógica de negocio
├── Dockerfile         # Imagen del servicio web
├── docker-compose.yml # Orquestación de servicios (web + postgres)
└── Makefile           # Comandos de build, run y mantenimiento
```

Decisiones de diseño:
- **Configuración por variables de entorno** para separar dev/staging/prod.
- **Makefile como interfaz de comandos** para estandarizar el workflow del equipo.
- **PostgreSQL como motor** por su soporte sólido a tipos complejos y constraints.

---

## ⚙️ Setup inicial

1. Clonar el repositorio:
   ```bash
   git clone https://github.com/camiloquintero771/OmniLatam.git
   cd OmniLatam
   ```

2. Crear un archivo `.env` en la raíz, basado en `.env.example`:
   ```env
   # Django
   DEBUG=True
   SECRET_KEY=your-secret-key-here
   TZ=America/Bogota
   DJANGO_SETTINGS_MODULE=reto.settings

   # PostgreSQL
   POSTGRES_DB=your_db_name
   POSTGRES_USER=your_db_user
   POSTGRES_PASSWORD=your_secure_password
   POSTGRES_HOST=postgres
   POSTGRES_PORT=5432
   ```

   > Para generar un `SECRET_KEY` seguro:
   > ```bash
   > python -c "from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())"
   > ```

3. Construir los contenedores:
   ```bash
   make build
   ```

4. Aplicar migraciones iniciales:
   ```bash
   make migrate
   ```

---

## ▶️ Ejecutar el proyecto

```bash
make up
```

La API quedará disponible en `http://localhost:8000`.

> Si Django no logra conectarse a Postgres en el primer arranque:
> ```bash
> make restart CONTAINER=django
> ```

---

## 🛠️ Comandos disponibles

| Comando | Descripción |
|---------|-------------|
| `make build` | Construye las imágenes Docker |
| `make up` | Levanta los servicios |
| `make migrate` | Ejecuta las migraciones de Django |
| `make superuser` | Crea un usuario administrador |
| `make startapp NAME=<nombre>` | Crea una nueva app de Django |
| `make get-requirements` | Ordena y fija versiones en `requirements.txt` |

---

## 📚 Endpoints principales

> _Pendiente: documentar con ejemplos de request/response — recomendado usar drf-spectacular o drf-yasg para auto-generar Swagger._

---

## 👤 Autor

**Camilo Quintero** — Backend Developer
[LinkedIn](https://www.linkedin.com/in/camlo2021) · [GitHub](https://github.com/camiloquintero771)


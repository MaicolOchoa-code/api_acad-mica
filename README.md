# API Académica

API educativa desarrollada con **FastAPI, SQLModel y SQLite** para gestionar cursos académicos y estudiantes. El proyecto permite crear, consultar, actualizar y eliminar cursos, además de registrar y consultar estudiantes.

La API valida los datos recibidos y utiliza una base de datos SQLite para guardar la información.

## Funcionalidades

- Crear cursos con nombre, créditos y estado activo.
- Consultar todos los cursos registrados.
- Buscar un curso por su identificador.
- Actualizar los datos de un curso.
- Eliminar un curso.
- Registrar estudiantes con nombre, correo electrónico, semestre y estado.
- Consultar todos los estudiantes registrados.
- Buscar un estudiante por su identificador.
- Validar los datos de entrada.
- Responder con códigos HTTP cuando ocurre un error.
- Guardar los registros en una base de datos SQLite.

## Tecnologías utilizadas

| Herramienta | Uso |
|---|---|
| Python | Lenguaje de programación. |
| FastAPI | Creación de la API y sus rutas. |
| Uvicorn | Servidor para ejecutar la aplicación. |
| SQLModel | Modelos y operaciones con la base de datos. |
| Pydantic | Validación de los datos recibidos. |
| SQLite | Almacenamiento de la información. |
| Swagger | Pruebas y documentación interactiva de los endpoints. |

Las dependencias del proyecto se encuentran en el archivo `requirements.txt`.

## Requisitos

- Python instalado.
- Visual Studio Code u otro editor de código.
- Terminal para ejecutar los comandos.
- Git, si se desea administrar y subir el proyecto a GitHub.

## Instalación y ejecución

### 1. Abrir la carpeta del proyecto

Abre una terminal en la carpeta donde se encuentra el archivo `main.py`.

### 2. Crear el entorno virtual

En Windows PowerShell:

```powershell
python -m venv venv
```

Activa el entorno virtual:

```powershell
.\venv\Scripts\Activate.ps1
```

Si el entorno virtual ya existe, solo es necesario activarlo.

### 3. Instalar las dependencias

```powershell
python -m pip install -r requirements.txt
```

### 4. Ejecutar la API

```powershell
python -m uvicorn main:app --reload --host 127.0.0.1 --port 8000
```

El parámetro `main:app` indica que la aplicación se encuentra en el archivo `main.py`. La opción `--reload` permite recargar el servidor cuando se realizan cambios en el código.

Para detener el servidor, presiona `Ctrl+C`.

### 5. Abrir Swagger

Cuando el servidor esté ejecutándose, abre la siguiente dirección:

[Documentación interactiva de Swagger](http://127.0.0.1:8000/docs)

Desde Swagger se pueden ejecutar las peticiones HTTP y consultar las respuestas de la API.

## Endpoints de cursos

| Método | Ruta | Descripción | Respuesta de éxito |
|---|---|---|---|
| POST | `/courses` | Crear un curso. | 201 Created |
| GET | `/courses` | Listar todos los cursos. | 200 OK |
| GET | `/courses/{course_id}` | Consultar un curso por ID. | 200 OK |
| PUT | `/courses/{course_id}` | Actualizar un curso existente. | 200 OK |
| DELETE | `/courses/{course_id}` | Eliminar un curso existente. | 200 OK |

### Reglas de validación de cursos

| Campo | Regla |
|---|---|
| `name` | Obligatorio, entre 3 y 80 caracteres. |
| `credits` | Obligatorio, número entero entre 1 y 6. |
| `active` | Booleano; si el esquema permite omitirlo, su valor predeterminado es `true`. |

En la actualización con `PUT`, se deben enviar todos los campos definidos en el esquema de actualización.

### Ejemplo: crear un curso

Método: `POST`

Ruta: `/courses`

Cuerpo JSON:

```json
{
  "name": "Programación I",
  "credits": 3,
  "active": true
}
```

La respuesta esperada es un código `201 Created`, con los datos del curso creado y su identificador.

### Ejemplo: actualizar un curso

Método: `PUT`

Ruta: `/courses/1`

Cuerpo JSON:

```json
{
  "name": "Programación II",
  "credits": 4,
  "active": false
}
```

El identificador `1` es un ejemplo. Se debe utilizar el ID de un curso que exista en la base de datos.

### Ejemplo: eliminar un curso

Método: `DELETE`

Ruta: `/courses/1`

Si el curso existe, la API lo elimina y responde con el mensaje definido en el servicio.

## Endpoints de estudiantes

| Método | Ruta | Descripción | Respuesta de éxito |
|---|---|---|---|
| POST | `/students` | Registrar un estudiante. | 201 Created |
| GET | `/students` | Listar todos los estudiantes. | 200 OK |
| GET | `/students/{student_id}` | Consultar un estudiante por ID. | 200 OK |

### Reglas de validación de estudiantes

Según el esquema propuesto para estudiantes:

| Campo | Regla |
|---|---|
| `name` | Entre 3 y 80 caracteres. |
| `email` | Obligatorio y no vacío. |
| `semester` | Número entero entre 1 y 10. |
| `active` | Booleano; valor predeterminado `true`. |

### Ejemplo: registrar un estudiante

Método: `POST`

Ruta: `/students`

Cuerpo JSON:

```json
{
  "name": "Ana Perez",
  "email": "ana@universidad.edu",
  "semester": 4,
  "active": true
}
```

La respuesta esperada es `201 Created`, con los datos del estudiante y su identificador.

## Códigos de respuesta HTTP

| Código | Significado |
|---|---|
| 200 | La operación se realizó correctamente. |
| 201 | El registro fue creado correctamente. |
| 404 | No se encontró el curso o estudiante solicitado. |
| 422 | Los datos enviados no cumplen las validaciones o el parámetro no tiene el formato esperado. |

Los códigos reales deben comprobarse ejecutando cada petición en Swagger.

## Base de datos

El proyecto utiliza SQLite para almacenar los cursos y estudiantes.

La base de datos se administra mediante SQLModel y las sesiones definidas en el módulo de conexión. La creación automática de las tablas depende de la configuración de la aplicación en `main.py`.

Se recomienda ejecutar la aplicación desde la carpeta raíz del proyecto para mantener una ubicación consistente de los archivos.

## Estructura del proyecto

```text
api_acad-mica/
├── main.py
├── database/
│   └── database.py
├── models/
│   ├── course.py
│   └── student.py
├── schemas/
│   ├── course.py
│   └── student.py
├── routers/
│   ├── courses.py
│   └── students.py
├── services/
│   ├── course_service.py
│   └── student_service.py
├── requirements.txt
├── README.md
└── entrega-pruebas/
    ├── informe-pruebas.md
    └── evidencias/
```

La estructura representa la organización esperada del proyecto. Los archivos de pruebas y evidencias deben crearse si todavía no existen.

## Flujo de funcionamiento

El funcionamiento general de la API es el siguiente:

1. El cliente envía una petición HTTP.
2. El router recibe la petición.
3. FastAPI valida los datos de entrada.
4. El servicio ejecuta la operación solicitada.
5. SQLModel interactúa con la base de datos SQLite.
6. La API devuelve una respuesta JSON con el resultado.

## Pruebas y evidencias

Las pruebas deben realizarse desde Swagger, en la dirección `http://127.0.0.1:8000/docs`.

Se recomienda comprobar:

- Creación y consulta de cursos.
- Actualización de un curso existente.
- Eliminación de un curso existente.
- Creación y consulta de estudiantes.
- Consulta de identificadores inexistentes.
- Envío de datos inválidos.
- Persistencia de los registros después de reiniciar la aplicación.

Las capturas deben mostrar las peticiones realizadas y sus respuestas reales. El informe de pruebas debe registrar el resultado esperado, el resultado obtenido y el estado de cada caso.

## Autoría y mantenimiento

Este proyecto se desarrolla con fines académicos para practicar el diseño de APIs REST, la validación de datos, la separación por capas y el manejo de una base de datos relacional mediante SQLite.

Para más información, consulta la documentación interactiva de Swagger y los archivos fuente del proyecto.

# Informe de pruebas — API Académica

## 1. Objetivo

Comprobar el funcionamiento de los endpoints de Courses y Students mediante Swagger, verificando las operaciones de creación, consulta, actualización y eliminación, así como las respuestas de la API.

## 2. Entorno de pruebas

- Framework: FastAPI.
- ORM: SQLModel.
- Base de datos: SQLite.
- Servidor: Uvicorn.
- Herramienta de pruebas: Swagger UI.
- URL local: http://127.0.0.1:8000/docs.

## 3. Pruebas realizadas

### P01. Listar cursos

- Endpoint: GET /courses
- Datos enviados: No requiere cuerpo JSON.
- Resultado esperado: Mostrar los cursos registrados.
- Resultado obtenido: La API mostró la lista de cursos correctamente.
- Código HTTP: 200 OK.
- Estado: APROBADO.
- Evidencia: evidencias/01-listar-cursos.png

### P02. Crear un curso

- Endpoint: POST /courses
- Datos enviados: Datos del curso ingresados en Swagger.
- Resultado esperado: Crear el curso y devolver su identificador.
- Resultado obtenido: El curso se creó correctamente.
- Código HTTP: 201 Created.
- Estado: APROBADO.
- Evidencia: evidencias/02-crear-curso.png

### P03. Verificar el resultado de creación

- Endpoint: POST /courses
- Datos enviados: Datos del curso utilizado en la prueba.
- Resultado esperado: Mostrar los datos del curso creado.
- Resultado obtenido: La respuesta mostró la información del curso correctamente.
- Código HTTP: 201 Created.
- Estado: APROBADO.
- Evidencia: evidencias/03-resultado-crear-curso.png

### P04. Buscar un curso por ID

- Endpoint: GET /courses/{course_id}
- Datos enviados: ID de un curso existente.
- Resultado esperado: Devolver los datos del curso solicitado.
- Resultado obtenido: El curso se consultó correctamente.
- Código HTTP: 200 OK.
- Estado: APROBADO.
- Evidencia: evidencias/04-buscar-curso.png

### P05. Actualizar un curso

- Endpoint: PUT /courses/{course_id}
- Datos enviados: Nombre, créditos y estado activo del curso.
- Resultado esperado: Actualizar el curso y conservar su identificador.
- Resultado obtenido: El curso se actualizó correctamente.
- Código HTTP: 200 OK.
- Estado: APROBADO.
- Evidencia: evidencias/05-actualizar-curso.png

### P06. Eliminar un curso

- Endpoint: DELETE /courses/{course_id}
- Datos enviados: ID del curso que se desea eliminar.
- Resultado esperado: Eliminar el curso y devolver el mensaje de confirmación.
- Resultado obtenido: El curso se eliminó correctamente.
- Código HTTP: 200 OK.
- Estado: APROBADO.
- Evidencia: evidencias/06-eliminar-curso.png

### P07. Listar estudiantes

- Endpoint: GET /students
- Datos enviados: No requiere cuerpo JSON.
- Resultado esperado: Mostrar los estudiantes registrados.
- Resultado obtenido: La API mostró la lista de estudiantes correctamente.
- Código HTTP: 200 OK.
- Estado: APROBADO.
- Evidencia: evidencias/07-listar-estudiantes.png

### P08. Crear un estudiante

- Endpoint: POST /students
- Datos enviados: Nombre, email y semestre.
- Resultado esperado: Crear el estudiante y devolver sus datos con un ID generado.
- Resultado obtenido: El estudiante se creó correctamente.
- Código HTTP: 201 Created.
- Estado: APROBADO.
- Evidencia: evidencias/08-crear-estudiante.png

### P09. Buscar un estudiante por ID

- Endpoint: GET /students/{student_id}
- Datos enviados: ID de un estudiante existente.
- Resultado esperado: Devolver los datos del estudiante solicitado.
- Resultado obtenido: El estudiante se consultó correctamente.
- Código HTTP: 200 OK.
- Estado: APROBADO.
- Evidencia: evidencias/09-buscar-estudiante.png

## 4. Conclusión

Las pruebas realizadas permitieron comprobar el funcionamiento de las operaciones de creación y consulta de cursos y estudiantes, así como la actualización y eliminación de cursos. Las respuestas obtenidas fueron satisfactorias para los casos ejecutados.

Para completar la validación de la actividad, también deben comprobarse los casos de error, las validaciones de datos y la persistencia de los registros después de reiniciar Uvicorn.

# Definición de Endpoints REST (SGAB)

## 1. Módulo de Alumnos (/students)
*Base para gestión de estudiantes.*

### POST /students (Crear Alumno)
- **Descripción:** Registra un nuevo alumno en el sistema.
- **Datos a enviar (Body):** `{ "matricula": "string", "nombre": "string", "carrera": "string" }`
- **Reglas de negocio:** - La matrícula debe ser única.
  - Todos los campos son obligatorios.
  - El status inicial por defecto será `active`.
- **Respuestas:** - Éxito: `201 Created`
  - Error: `400 Bad Request` (Si faltan datos o la matrícula ya existe).

### GET /students (Listar Alumnos)
- **Descripción:** Obtiene la lista de alumnos registrados.
- **Opcional (Query Params):** `?page=1&limit=10` (Paginación), `?status=active`, `?carrera=ISC` (Filtros).
- **Respuesta:** `200 OK` con formato `{ "items": [...], "total": 100 }`

### GET /students/:id (Consultar Alumno)
- **Descripción:** Obtiene los detalles de un alumno específico por su ID.
- **Reglas de negocio:** El ID debe existir en la base de datos.
- **Respuestas:**
  - Éxito: `200 OK` retornando `{ "id", "matricula", "nombre", "carrera", "status" }`
  - Error: `404 Not Found` (Si no existe).

### PATCH /students/:id (Actualizar Alumno)
- **Descripción:** Modifica datos parciales de un alumno.
- **Datos a enviar (Body Parcial):** `{ "nombre"?: "string", "carrera"?: "string", "status"?: "string" }`
- **Reglas de negocio:** Si se actualiza la matrícula, verificar que siga siendo única.
- **Respuesta:** `200 OK`.

### DELETE /students/:id (Eliminar Alumno)
- **Descripción:** Da de baja a un alumno del sistema.
- **Reglas de negocio:** Se recomienda eliminación lógica (cambiar `status = inactive`) para no perder el historial de calificaciones.
- **Respuesta:** `204 No Content`.

---

## 2. Módulo de Materias (/subjects)
*Gestión del catálogo de materias.*

### POST /subjects (Crear Materia)
- **Datos a enviar (Body):** `{ "clave": "string", "nombre": "string", "semestre": "number" }`
- **Reglas de negocio:** La clave de la materia debe ser única e irrepetible. Campos obligatorios.
- **Respuesta:** `201 Created`.

### GET /subjects (Listar Materias)
- **Opcional:** Filtros por semestre `?semestre=3`.
- **Respuesta:** `200 OK`.

### PATCH /subjects/:id (Actualizar Materia)
- **Datos a enviar (Body Parcial):** `{ "clave"?: "string", "nombre"?: "string", "semestre"?: "number" }`
- **Reglas de negocio:** Validar que la nueva clave no choque con otra materia existente.
- **Respuesta:** `200 OK`.

### DELETE /subjects/:id (Eliminar Materia)
- **Reglas de negocio:** Eliminación lógica. No se puede eliminar una materia si ya tiene alumnos inscritos o calificaciones asignadas (protección de integridad).
- **Respuesta:** `204 No Content` o `409 Conflict` (si tiene alumnos).

---

## 3. Módulo de Calificaciones (/grades)
*Captura y gestión de notas.*

### POST /grades (Capturar Calificación)
- **Datos a enviar (Body):** `{ "studentId": "number", "subjectId": "number", "value": "number" }`
- **Reglas de negocio:**
  - El alumno (`studentId`) y la materia (`subjectId`) deben existir obligatoriamente.
  - El valor (`value`) debe estar en el rango de 0 a 100.
- **Respuestas:**
  - Éxito: `201 Created`.
  - Error: `400 Bad Request` (Si la calificación es -5 o 105, por ejemplo).

### GET /grades (Listar Calificaciones)
- **Opcional (Filtros útiles):** `?studentId=5` (Para ver todas las notas de un alumno) o `?subjectId=2` (Para ver el grupo de una materia).
- **Respuesta:** `200 OK`.

### PATCH /grades/:id (Corregir Calificación)
- **Datos a enviar (Body):** `{ "value": "number" }`
- **Reglas de negocio:** Validar nuevamente que el valor esté entre 0 y 100. Registrar en bitácora de auditoría quién hizo el cambio.
- **Respuesta:** `200 OK`.

### DELETE /grades/:id (Eliminar Calificación)
- **Reglas de negocio:** Solo permitido para administradores (roles superiores).
- **Respuesta:** `204 No Content`.
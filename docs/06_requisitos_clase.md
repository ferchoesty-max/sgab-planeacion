# Actividad en Clase: Requisitos y Diseño (SGAB)

## 1. Definición de Módulos
Basado en la estructura del sistema SGAB:
- **Módulo de Usuarios:** Control de acceso y roles.
- **Módulo de Alumnos:** Gestión de datos personales y escolares.
- **Módulo de Materias:** Administración de cursos y asignaciones.
- **Módulo de Calificaciones:** Captura y cálculo de promedios.
- **Módulo de Reportes:** Generación de boletas y documentos oficiales.

## 2. Requisitos Funcionales (8 RF)
*Lo que el sistema debe hacer.*

1. **RF-01:** El sistema debe permitir el ingreso (login) validando usuario y contraseña.
2. **RF-02:** El usuario Administrador debe poder registrar nuevos alumnos en la base de datos.
3. **RF-03:** El usuario Administrador debe poder registrar nuevas materias y asignarlas a un docente.
4. **RF-04:** El usuario Docente debe poder visualizar la lista de alumnos inscritos en sus grupos.
5. **RF-05:** El usuario Docente debe poder capturar calificaciones parciales para cada alumno.
6. **RF-06:** El sistema debe calcular automáticamente el promedio final del alumno.
7. **RF-07:** El usuario Alumno debe poder consultar su historial académico (kárdex).
8. **RF-08:** El sistema debe permitir la modificación de datos del alumno solo por el Administrador.

## 3. Requisitos No Funcionales (6 RNF)
*Restricciones y calidad del sistema.*

1. **RNF-01 (Desempeño):** El sistema debe responder a cualquier consulta en menos de 2 segundos.
2. **RNF-02 (Seguridad):** El sistema debe manejar control de acceso basado en roles (Admin, Docente, Alumno).
3. **RNF-03 (Auditoría):** El sistema debe registrar en una bitácora cualquier cambio en las calificaciones (quién y cuándo).
4. **RNF-04 (Disponibilidad):** El sistema debe estar disponible el 99.9% del tiempo en periodo de exámenes.
5. **RNF-05 (Usabilidad):** La interfaz debe ser responsiva (adaptable a móviles y escritorio).
6. **RNF-06 (Seguridad):** Las contraseñas de los usuarios deben almacenarse encriptadas en la base de datos.

## 4. Justificación de 2 RNF
*Por qué son importantes estos requisitos.*

- **Justificación de RNF-01 (Tiempo < 2s):** Es crucial para evitar la frustración del usuario. Si un docente tarda mucho en guardar cada calificación, el proceso administrativo se vuelve ineficiente y propenso a errores por duplicidad de clics.
- **Justificación de RNF-03 (Auditoría):** Al tratarse de un sistema académico, la integridad de los datos es vital. Se debe tener un rastro exacto de quién modificó una calificación para evitar corrupción o errores no detectados.

## 5. Diagrama de Casos de Uso
*Actores: Administrativo, Docente, Alumno.*
![Diagrama Final del Sistema](diagrama.png.png)
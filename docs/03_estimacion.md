# Estimación del Proyecto

## Suposiciones de la estimación
- Se cuenta con un desarrollador Full Stack (Yo).
- Jornada de trabajo de 4 horas diarias.
- No incluye tiempo de despliegue en servidor producción.

## Descomposición Funcional y Esfuerzo

| Módulo | Tarea | Esfuerzo Estimado (Horas) | Incertidumbre |
|--------|-------|---------------------------|---------------|
| **Auth** | Login y recuperación de contraseña | 12 h | Baja |
| **Usuarios** | CRUD de Alumnos y Maestros | 20 h | Media |
| **Materias** | Gestión de materias y grupos | 16 h | Media |
| **Notas** | Captura y cálculo de promedios | 32 h | Alta |
| **Reportes** | Generación de boletas PDF | 20 h | Alta |
| **Total** | | **100 horas** | |

*Nota: La incertidumbre es alta en "Notas" debido a la complejidad de las reglas de negocio de la escuela.*
# Práctica de Préstamo de Equipo - Odoo 20.0

**Estudiante:** Ricardo José Hernández Guillen

**Número de cuenta:** [Conserva aquí tu número de cuenta actual]

## Respuestas

### Paso 1: Catálogo de equipos

**1. ¿Qué pasa con un equipo cuando se desmarca el campo Activo? ¿Por qué es mejor que borrarlo?**

Al desmarcar el campo Activo, el equipo queda archivado y deja de aparecer en las vistas normales del sistema. Es mejor archivarlo que eliminarlo porque se conserva su información y su historial, permitiendo consultarlo nuevamente cuando sea necesario.

**2. ¿Para qué sirve el atributo copy=False en el campo codigo?**

El atributo copy=False evita que el código de inventario se copie automáticamente cuando se duplica un registro. Esto ayuda a evitar códigos repetidos y garantiza que cada equipo tenga un identificador único.

### Equipos registrados

Se registraron correctamente los siguientes equipos en el sistema:

| Equipo | Código |
|---|---|
| Laptop Dell | EQ-001 |
| Proyector Epson | EQ-002 |
| Equipo de sonido | EQ-003 |
| Equipo de laboratorio | EQ-004 |
| Micrófono 01 | AUD-002 |

**Resultado:** El catálogo de equipos funciona correctamente. Se pueden visualizar los registros desde la vista de lista y acceder a ellos desde el módulo Préstamo de Equipo.



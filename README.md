# Práctica de Préstamo de Equipo - Odoo 20.0

**Estudiante:** Ricardo José Hernández Guillen

**Número de cuenta:** 0615200400680

## Respuestas

### Paso 1: Catálogo de equipos

**1. ¿Qué pasa con un equipo cuando se desmarca el campo Activo? ¿Por qué es mejor que borrarlo?**

Al desmarcar el campo Activo, el equipo queda archivado y deja de aparecer en las vistas normales del sistema. Es mejor archivarlo que eliminarlo porque se conserva su información y su historial, permitiendo consultarlo nuevamente cuando sea necesario.

**2. ¿Para qué sirve `copy=False` en el campo codigo?**

El atributo `copy=False` evita que el código de inventario se copie automáticamente cuando se duplica un registro. Esto ayuda a evitar códigos repetidos y garantiza que cada equipo tenga un identificador único.

#### Equipos registrados

Se registraron correctamente los siguientes equipos en el sistema:

| Equipo | Código |
|---|---|
| Laptop Dell | EQ-001 |
| Proyector Epson | EQ-002 |
| Equipo de sonido | EQ-003 |
| Equipo de laboratorio | EQ-004 |
| Micrófono 01 | AUD-002 |

**Resultado:** El catálogo de equipos funciona correctamente. Se pueden visualizar los registros desde la vista de lista y acceder a ellos desde el módulo Préstamo de Equipo.

---

### Paso 2: Registro de préstamos

**1. Este modelo usa `_name` y `_inherit` al mismo tiempo. ¿Qué hace cada uno aquí?**

El atributo `_name` define el nombre del nuevo modelo, en este caso `prestamo.prestamo`. El atributo `_inherit` permite heredar las funcionalidades y campos del modelo `mail.thread`, incorporando el chatter para registrar mensajes y cambios en el historial del préstamo.

**2. ¿Qué hace `tracking=True` en el campo state?**

El atributo `tracking=True` permite registrar los cambios realizados en el campo state dentro del chatter. De esta manera, cuando cambia el estado del préstamo, queda un registro del cambio en el historial del documento.

---

### Paso 3: Equipos del préstamo

**1. En `fields.One2many("prestamo.linea", "prestamo_id")`, ¿qué indica cada parámetro?**

El primer parámetro, `prestamo.linea`, indica el modelo relacionado que contiene las líneas de los equipos. El segundo parámetro, `prestamo_id`, indica el campo Many2one de ese modelo que establece la relación con el préstamo actual.

**2. ¿Qué pasa con las líneas cuando se borra un préstamo? ¿Qué parte del código lo define?**

Cuando se elimina un préstamo, también se eliminan sus líneas relacionadas. Esto está definido por el atributo `ondelete="cascade"` en el campo Many2one `prestamo_id` del modelo `prestamo.linea`.

---

### Paso 4: Flujo de estados

**1. Los botones ya se ocultan según el estado. ¿Por qué los métodos vuelven a validar el estado?**

Porque ocultar los botones solamente controla lo que se muestra en la interfaz. Las validaciones dentro de los métodos protegen la lógica del sistema y evitan que se realicen operaciones incorrectas mediante otras llamadas o accesos al servidor.

**2. ¿Qué hace `prestamo.linea_ids.equipo_id.write(...)`? ¿Por qué no hace falta un for para cada equipo?**

Permite acceder a los equipos relacionados con las líneas del préstamo y modificar su estado mediante el método `write()`. No hace falta utilizar un ciclo for porque Odoo permite ejecutar operaciones sobre un conjunto de registros relacionados en una sola llamada.

---

### Paso 5: Reglas del préstamo

**1. El campo `equipo_id` ya filtra los equipos disponibles. ¿Por qué hace falta el TODO 5?**

Porque el dominio del campo solamente filtra los equipos disponibles cuando se seleccionan desde la interfaz. Sin embargo, un equipo podría cambiar de estado después de haber sido seleccionado. Por eso, el TODO 5 vuelve a comprobar que el equipo siga disponible justo antes de realizar el préstamo.

**2. ¿En qué momento se ejecuta un método con `@api.constrains`? ¿Y la validación de `action_prestar`?**

Un método con `@api.constrains` se ejecuta cuando se crean o modifican los registros y alguno de los campos indicados en la restricción cambia. En cambio, las validaciones de `action_prestar` se ejecutan cuando se llama al método para realizar el préstamo, al pulsar el botón Prestar.

---

### Paso 6: Contacto, Kanban y búsqueda

**1. ¿Qué pasa si arrastra una tarjeta del kanban a otra columna? ¿Por qué?**

Al arrastrar una tarjeta a otra columna, Odoo puede actualizar el valor del campo utilizado para agrupar los registros, en este caso `estado`. Esto sucede porque las columnas del Kanban representan los diferentes valores de ese campo. El cambio depende de los permisos y de que el campo permita la modificación desde esa vista.

**2. El campo `prestamo_ids` se agregó a `res.partner`. ¿Se crea una columna nueva en la tabla de contactos? Explique.**

No. Un campo One2many no crea una columna nueva en la tabla de contactos. La relación se establece mediante el campo Many2one `partner_id` que está definido en el modelo `prestamo.prestamo`. Así, Odoo puede mostrar todos los préstamos asociados a un contacto sin almacenar una columna adicional en la tabla de contactos.




# Sistema de Biblioteca - Colegio Amigos de Don Bosco

**Proyecto de Cátedra - Fase 1**

¡Hola equipo! Este es nuestro proyecto de la Fase 1 para el sistema de la biblioteca. Traté de dejar el código lo más limpio y ordenado posible para que todos podamos entenderlo fácilmente y sacar ese 10 en la revisión.

Aquí les explico cómo está armado todo el sistema para que estemos en la misma sintonía:

## ¿Cómo organizamos el código? (Patrón MVC)

Usamos el patrón Modelo-Vista-Controlador (con unas carpetas extra para la base de datos y utilidades) para que el código no sea un espagueti. Todo está dentro de la carpeta `src`:

- **`modelo`**: Aquí están las clases puras que representan la información. Creamos la clase base `Documento` y de ahí heredan `Libro`, `Revista`, `CD` y `Tesis`. Esto cubre la parte de "Herencia y Polimorfismo" que pedía el profe. También están los modelos de `Usuario` y `Prestamo`.
- **`vista`**: Son las pantallas de la aplicación (Swing). Tenemos el `LoginFrame` (para iniciar sesión), el `MainFrame` (el menú principal) y las pantallas para gestionar usuarios, documentos y préstamos.
- **`controlador`**: Es el cerebro que conecta las pantallas con la base de datos (por ejemplo, `LoginControlador` revisa si tu clave es correcta).
- **`dao`** (Data Access Object): Aquí están todas las consultas SQL (`INSERT`, `SELECT`, etc.). Si quieren ver cómo guardamos o buscamos datos, abran esta carpeta. `Conexion.java` es el archivo que se conecta a nuestro MySQL.
- **`excepciones`**: Creamos una excepción propia llamada `ErrorValidacion.java`. La usamos cuando alguien intenta hacer algo indebido (como prestar un libro que no hay o si el alumno tiene moras).
- **`utilidades`**: Tenemos el archivo `ManejoErrores.java` que atrapa cualquier error y lo guarda en un archivo de texto llamado `errores.txt`. Esto cubre el punto de "Manejo de Logs de errores".

## Las Funcionalidades Principales

Cumplimos todo lo de la rúbrica, aquí les digo dónde está cada cosa por si nos preguntan:

1. **Los 3 Tipos de Usuarios:** El sistema detecta si eres Administrador, Profe o Alumno. Si entras como alumno, los botones de "Gestionar Usuarios" o hacer devoluciones desaparecen. ¡Prueben creando un usuario alumno para que vean cómo se oculta el menú!
2. **Moras y Límites:** En la parte de Préstamos (`PrestamoDAO.java`), el código revisa la base de datos primero. Si el alumno debe un libro, lanza una alerta y no le presta nada. También revisa el límite (dejamos que los alumnos saquen 3 libros máximo y los profes 5).
3. **Devoluciones:** Cuando el administrador registra una devolución, el sistema resta la fecha esperada con la fecha de hoy. Si te pasaste de días, te cobra $0.50 por día de retraso automáticamente.

## ¿Cómo correr el proyecto en sus computadoras?

1. En NetBeans, creen un **Nuevo Proyecto > Java with Ant > Java Application** (sin main class).
2. Copien toda la carpeta `src` de este proyecto y péguenla en el suyo.
3. Denle clic derecho a la carpeta **Libraries** de NetBeans, seleccionen **Add JAR/Folder** y busquen el archivo `.jar` de MySQL (mysql-connector-java).
4. Corran el script de MySQL `database/BD_Colegio.sql` en su compu para que se cree la base de datos vacía con el usuario administrador.
5. Vayan al archivo `dao/Conexion.java` y asegúrense de poner **su** contraseña de MySQL en la línea 10 (`private static final String CLAVE = "su_clave";`).
6. Abran `Principal.java` y denle a **Run File**.

Para entrar, usen el correo **admin@donbosco.edu** con la clave **admin123**.

## ¿Cómo correr el proyecto SIN usar NetBeans? (El 10% de la nota)

La rúbrica pide que la aplicación funcione sin el IDE. Para hacer esto y que el profe nos ponga los 10 puntos:

1. Asegúrense de que el proyecto corre bien dentro de NetBeans.
2. Denle **clic derecho** sobre el nombre del proyecto en el panel izquierdo de NetBeans (donde está la tacita de café).
3. Seleccionen **Clean and Build** (Limpiar y Construir).
4. Vayan a la carpeta física de su proyecto usando el Finder o Explorador de Windows.
5. Verán que apareció una carpeta nueva llamada **`dist`**. Adentro hay un archivo `.jar` y una carpeta `lib`.
6. ¡Solo tienen que darle **doble clic al archivo `.jar`**! La aplicación se abrirá sola como cualquier programa normal de escritorio sin necesidad de abrir NetBeans.

¡Cualquier duda que tengan revisen los comentarios que dejé en el código! Todo está en español y bastante claro.

Sistema de Biblioteca - Colegio Amigos de Don Bosco
Proyecto de Cátedra - Fase 1
¿Cómo organizamos el código? (Patrón MVC)
Usamos el patrón Modelo-Vista-Controlador (MVC), con algunas carpetas adicionales para la base de datos y utilidades. De esta forma el código queda mucho más organizado y fácil de entender. Todo el código fuente está dentro de la carpeta src:

modelo: Aquí están las clases que representan la información (entidades). Creamos una clase base llamada Documento, de la que heredan Libro, Revista, CD y Tesis. Esto cumple con el requisito de Herencia y Polimorfismo. También incluimos las clases Usuario y Prestamo.
vista: Contiene todas las pantallas de la aplicación (hechas con Swing). Incluye el LoginFrame, el MainFrame (menú principal) y las ventanas para gestionar usuarios, documentos y préstamos.
controlador: Es el "cerebro" del sistema. Se encarga de conectar las vistas con la lógica y la base de datos. Por ejemplo, el LoginControlador verifica las credenciales del usuario.
dao (Data Access Object): Aquí están todas las consultas SQL (INSERT, SELECT, UPDATE, etc.). Si quieren ver cómo se guardan o buscan los datos, esta es la carpeta. El archivo Conexion.java maneja la conexión con MySQL.
excepciones: Creamos nuestra propia excepción ErrorValidacion.java para manejar casos especiales (como intentar prestar un libro que no está disponible o cuando un alumno tiene mora).
utilidades: Incluye ManejoErrores.java, que captura cualquier error y lo guarda en un archivo de texto llamado errores.txt. Esto cumple con el punto de manejo de logs de errores.

Funcionalidades Principales
Cumplimos con todo lo solicitado en la rúbrica. Aquí les resumo dónde encontrar cada cosa:

Tres tipos de usuarios: El sistema identifica si eres Administrador, Profesor o Alumno. Cuando entras como alumno, los botones de "Gestionar Usuarios" y devoluciones se ocultan automáticamente. ¡Prueben creando un usuario alumno para verlo en acción!
Moras y límites de préstamo: En PrestamoDAO.java se validan estas reglas antes de realizar cualquier préstamo. Si el alumno tiene mora, se le bloquea. Los alumnos pueden tener máximo 3 libros y los profesores 5.
Devoluciones: Al registrar una devolución, el sistema calcula automáticamente los días de retraso. Si hay mora, cobra $0.50 por cada día de retraso.

¿Cómo correr el proyecto en NetBeans?

Crea un Nuevo Proyecto > Java with Ant > Java Application (sin clase main).
Copia toda la carpeta src de este proyecto y pégala en el tuyo.
Clic derecho en Libraries → Add JAR/Folder y agrega el conector de MySQL (mysql-connector-java.jar).
Ejecuta el script database/BD_Colegio.sql en tu MySQL para crear la base de datos.
Abre dao/Conexion.java y coloca tu contraseña de MySQL en la línea de la clave.
Abre Principal.java y dale Run File.

Credenciales de administrador:
Correo: admin@donbosco.edu
Clave: admin123
¿Cómo correr el proyecto sin NetBeans? (Importante para el 10%)
Para cumplir con este punto de la rúbrica:

Asegúrate de que el proyecto funcione correctamente en NetBeans.
Clic derecho sobre el nombre del proyecto → Clean and Build.
Ve a la carpeta del proyecto en tu explorador.
Entra a la carpeta dist. Ahí encontrarás el archivo .jar y la carpeta lib.
Solo da doble clic al archivo .jar y la aplicación se abrirá como cualquier programa normal.

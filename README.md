# Microservicio de Autenticación y Notificaciones ('notificaciones')

## Integrantes
* **Gonzalo Hormazábal**
* **Geraldinne González**


## Descripción
Módulo de seguridad perimetral y comunicaciones. Emite las alertas críticas de negocio (ej: Oferta superada) y restringe sus recursos mediante autenticación robusta de Spring Security.

* **Puerto:** `8088`
* **Base de Datos:** `notificaciones_db` (MySQL)


## Funcionalidades Clave
* **Seguridad Incorporada:** Acceso restringido por **Basic Authentication** (`Customizer.withDefaults()`).
* Carga automatizada de trazas de notificaciones mediante `CommandLineRunner`.
* Manejo de logs de auditoría estructurados usando **SLF4J + Logback** en nivel `DEBUG`.


## Configuración (`application.properties`)
* server.port=8088
* spring.datasource.url=jdbc:mysql://localhost:3306/notificaciones_db
* spring.datasource.username=root
* spring.datasource.password=
* spring.jpa.hibernate.ddl-auto=update

* spring.security.user.name=admin_notificaciones
* spring.security.user.password=Notificacion2026!

* logging.level.cl.sda1085.notificaciones=DEBUG


## Pasos para Ejecutar

### 1. Preparación de la Base de Datos
Antes de ejecutar el servicio, crear la conexión a la base de datos de MySQL (XAMPP) corriendo en el puerto 3306 y con el nombre 'notificaciones_db'.

### 2. Verificación de Credenciales
Revisar que el archivo application.properties tenga por defecto, usuario root y contraseña vacía.

### 3. Lanzamiento del Microservicio
Ejecutar (run) la clase principal con la anotación @SpringBootApplication (NotificacionesApplication.java).

### 4. Reglas de Seguridad
Al consumir los endpoints en Postman, ten en cuenta el comportamiento de la cadena de filtros de seguridad:

* Buzón Personal (GET /api/notificaciones/usuario/{idUsuario}): Protege la privacidad de las alertas. Requiere configurar Authorization como Basic Auth vinculando al CLIENTE correspondiente para ver sus mensajes recibidos.
* Disparo de Alertas (POST /api/notificaciones): La emisión manual o masiva de notificaciones de sistema está restringida del lado del cliente y requiere obligatoriamente privilegios de ADMIN.

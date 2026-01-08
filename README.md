# 🍽️ Sistema de Reservas - Restaurante Carmen

Sistema web de gestión de reservas desarrollado con Spring Boot para el Restaurante Carmen. Permite a los usuarios realizar reservas de mesa de manera intuitiva y segura.

## 📋 Tabla de Contenidos

- [Características](#-características)
- [Tecnologías Utilizadas](#-tecnologías-utilizadas)
- [Requisitos Previos](#-requisitos-previos)
- [Instalación](#-instalación)
- [Configuración](#-configuración)
- [Uso](#-uso)
- [Estructura del Proyecto](#-estructura-del-proyecto)
- [Seguridad](#-seguridad)
- [Despliegue](#-despliegue)
- [Contribuciones](#-contribuciones)
- [Licencia](#-licencia)

## ✨ Características

- 🔐 **Sistema de autenticación y autorización** con Spring Security
- 👥 **Gestión de usuarios** con roles (ADMIN, USER)
- 📅 **Sistema de reservas** para mesas del restaurante
- 🎨 **Interfaz moderna y responsive** con Bootstrap 4
- 🌐 **Soporte HTTPS** para conexiones seguras
- 📱 **Diseño responsive** adaptable a diferentes dispositivos
- 🔍 **Gestión de menú** del restaurante

## 🛠️ Tecnologías Utilizadas

- **Backend:**
  - Java 17
  - Spring Boot 3.1.5
  - Spring Security
  - Spring Data JPA
  - Thymeleaf (motor de plantillas)

- **Base de Datos:**
  - MySQL 8.0+

- **Frontend:**
  - HTML5 / CSS3
  - Bootstrap 4.5.2
  - JavaScript
  - jQuery 3.5.1

- **Herramientas:**
  - Maven (gestión de dependencias)
  - Lombok (reducción de código boilerplate)

## 📦 Requisitos Previos

Antes de comenzar, asegúrate de tener instalado:

- **Java JDK 17** o superior
- **Maven 3.6+**
- **MySQL 8.0+** (o superior)
- **Git** (para clonar el repositorio)

## 🚀 Instalación

1. **Clona el repositorio:**
   ```bash
   git clone https://github.com/tu-usuario/restaurante-carmen.git
   cd restaurante-carmen
   ```

2. **Crea la base de datos en MySQL:**
   ```sql
   CREATE DATABASE restaurante CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
   ```

3. **Configura el archivo `application.properties`:**
   - Copia el archivo de ejemplo:
     ```bash
     cp src/main/resources/application.properties.example src/main/resources/application.properties
     ```
   - Edita `application.properties` con tus credenciales:
     - Configura la URL, usuario y contraseña de MySQL
     - Configura la contraseña del keystore si usas HTTPS

4. **Genera el certificado SSL (opcional, para HTTPS):**
   Si deseas usar HTTPS con un certificado autofirmado:
   ```bash
   keytool -genkeypair -alias mykey -keyalg RSA -keysize 2048 -storetype PKCS12 -keystore src/main/resources/keystore.p12 -validity 365
   ```
   **Nota:** Este certificado es solo para desarrollo. En producción, usa un certificado válido emitido por una CA.

5. **Compila y ejecuta la aplicación:**
   ```bash
   mvn clean install
   mvn spring-boot:run
   ```

   O usando el wrapper de Maven:
   ```bash
   ./mvnw clean install
   ./mvnw spring-boot:run
   ```

6. **Accede a la aplicación:**
   - **HTTP (si deshabilitas SSL):** http://localhost:8080
   - **HTTPS:** https://localhost:8443

## ⚙️ Configuración

### Configuración de la Base de Datos

Edita `src/main/resources/application.properties`:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/restaurante?useSSL=false&serverTimezone=UTC
spring.datasource.username=tu_usuario
spring.datasource.password=tu_contraseña
```

### Configuración de HTTPS (Opcional)

Si deseas deshabilitar HTTPS para desarrollo, comenta o elimina las siguientes líneas en `application.properties`:

```properties
# server.port=8443
# server.ssl.key-store=classpath:keystore.p12
# server.ssl.key-store-password=tu_contraseña
# server.ssl.key-store-type=PKCS12
# server.ssl.key-alias=mykey
```

Y configura un puerto HTTP estándar:

```properties
server.port=8080
```

### Configuración de JPA/Hibernate

Para producción, cambia `ddl-auto` a `validate` o `none`:

```properties
spring.jpa.hibernate.ddl-auto=validate
```

## 📖 Uso

### Roles de Usuario

- **USER:** Puede realizar reservas
- **ADMIN:** Acceso completo, incluyendo gestión de usuarios y gestion de reservas

### Funcionalidades Principales

1. **Registro de Usuario:** Los nuevos usuarios pueden registrarse desde la página de registro
2. **Inicio de Sesión:** Autenticación segura con Spring Security
3. **Realizar Reservas:** Los usuarios autenticados pueden realizar reservas de mesa
4. **Gestionar Reservas:** Ver, editar y eliminar reservas (solo el usuario propietario)
5. **Ver Menú:** Acceso al menú del restaurante sin necesidad de autenticación

## 📁 Estructura del Proyecto

```
restaurante-carmen/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/restaurant/carmen/
│   │   │       ├── controllers/     # Controladores MVC
│   │   │       ├── models/          # Entidades JPA
│   │   │       ├── repository/      # Repositorios Spring Data
│   │   │       ├── security/        # Configuración de seguridad
│   │   │       ├── service/         # Lógica de negocio
│   │   │       └── dto/             # Data Transfer Objects
│   │   └── resources/
│   │       ├── static/              # Recursos estáticos (CSS, JS, imágenes)
│   │       ├── templates/           # Plantillas Thymeleaf
│   │       └── application.properties.example
│   └── test/
│       └── java/                    # Pruebas unitarias
├── pom.xml                          # Configuración Maven
├── README.md                        # Este archivo
└── .gitignore                       # Archivos ignorados por Git
```

## 🔒 Seguridad

- Las contraseñas se almacenan usando **BCrypt** (hashing seguro)
- Implementación de **Spring Security** para autenticación y autorización
- **HTTPS** configurado para conexiones seguras
- Protección contra **CSRF** (habilitada por defecto en Spring Security)
- Validación de roles y permisos por ruta

## 📝 Licencia

Este proyecto está bajo la Licencia MIT - ver el archivo [LICENSE](LICENSE) para más detalles.

## 👨‍💻 Autor

Desarrollado como proyecto personal para demostración de habilidades en desarrollo web con Spring Boot.
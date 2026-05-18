# API Gateway

API Gateway para microservicios construido con Spring Boot y Spring Cloud Gateway.

## 📋 Descripción

Este proyecto es un API Gateway que actúa como punto de entrada único para un sistema de microservicios. El gateway enruta las solicitudes a los diferentes microservicios según la ruta de la solicitud, proporcionando una capa de abstracción y gestión centralizada del tráfico.

## 🛠️ Tecnologías

- **Java**: 17
- **Spring Boot**: 3.3.1
- **Spring Cloud**: 2023.0.1
- **Spring Cloud Gateway**: Para el enrutamiento y gestión de tráfico
- **Maven**: Gestión de dependencias y construcción del proyecto
- **Spring Boot DevTools**: Para recarga rápida durante el desarrollo

## 📁 Estructura del Proyecto

```
api-gateway/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── Api_gateway/cl/api_gateway/
│   │   │       └── ApiGatewayApplication.java
│   │   └── resources/
│   │       └── application.properties
│   └── test/
│       └── java/
│           └── Api_gateway/cl/api_gateway/
│               └── ApiGatewayApplicationTests.java
├── pom.xml
├── HELP.md
├── mvnw
└── mvnw.cmd
```

## 🔗 Microservicios Configurados

El API Gateway está configurado para enrutar a los siguientes microservicios:

| Microservicio | Ruta | Puerto Local |
|---------------|------|--------------|
| **Citas** | `/api/citas/**` | 8081 |
| **Pacientes** | `/api/pacientes/**` | 8082 |
| **Médicos** | `/api/medicos/**` | 8083 |
| **Salas** | `/api/salas/**` | 8084 |
| **Historial** | `/api/historial/**` | 8085 |
| **Notificaciones** | `/api/notificaciones/**` | 8086 |

## 🚀 Configuración

### Puerto del Gateway
El API Gateway se ejecuta en el puerto **8080**.

### Configuración de Rutas

Las rutas están configuradas en `src/main/resources/application.properties`:

```properties
spring.application.name=api-gateway
server.port=8080

# Ejemplo de configuración de ruta para ms-citas
spring.cloud.gateway.routes[0].id=ms-citas
spring.cloud.gateway.routes[0].uri=http://localhost:8081
spring.cloud.gateway.routes[0].predicates[0]=Path=/api/citas/**
```

## 🏃 Ejecutar el Proyecto

### Prerrequisitos

- Java 17 o superior
- Maven 3.6+ (o usar los scripts mvnw/mvnw.cmd incluidos)

### Ejecutar con Maven

```bash
# Usar Maven instalado
mvn spring-boot:run

# O usar el script incluido
./mvnw spring-boot:run  # Linux/Mac
mvnw.cmd spring-boot:run  # Windows
```

### Ejecutar el JAR compilado

```bash
# Compilar el proyecto
mvn clean package

# Ejecutar el JAR
java -jar target/api-gateway-0.0.1-SNAPSHOT.jar
```

## 🧪 Ejecutar Tests

```bash
mvn test
```

## 📝 Uso del API Gateway

Una vez que el gateway esté ejecutándose, puedes acceder a los microservicios a través de las rutas configuradas:

### Ejemplos de Solicitudes

```bash
# Acceder al microservicio de citas
curl http://localhost:8080/api/citas/

# Acceder al microservicio de pacientes
curl http://localhost:8080/api/pacientes/

# Acceder al microservicio de médicos
curl http://localhost:8080/api/medicos/
```

El gateway reenviará estas solicitudes a los puertos correspondientes de cada microservicio.

## 🔧 Configuración Adicional

### Logging

El logging de Spring Cloud Gateway está configurado en nivel DEBUG para facilitar el desarrollo:

```properties
logging.level.org.springframework.cloud.gateway=DEBUG
```

### DevTools

Spring Boot DevTools está habilitado para permitir recarga rápida durante el desarrollo. Los cambios en los archivos se recargan automáticamente.

## 📦 Dependencias Principales

- `spring-cloud-starter-gateway`: Funcionalidad principal del API Gateway
- `spring-boot-devtools`: Herramientas de desarrollo
- `spring-boot-starter-test`: Dependencias para testing

## 🌐 Arquitectura

```
Cliente → API Gateway (8080) → Microservicios
                              ├─ ms-citas (8081)
                              ├─ ms-pacientes (8082)
                              ├─ ms-medicos (8083)
                              ├─ ms-salas (8084)
                              ├─ ms-historial (8085)
                              └─ ms-notificaciones (8086)
```

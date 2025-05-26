🏥 Sistema de Microservicios para Bombas de Insulina
Sistema completo de monitoreo y gestión de bombas de insulina para pacientes diabéticos, desarrollado con arquitectura de microservicios y API Gateway.

📋 Descripción General
Este sistema permite a hospitales y clínicas gestionar de manera integral pacientes diabéticos con bombas de insulina, proporcionando monitoreo en tiempo real, alertas automáticas y análisis estadísticos para optimizar el tratamiento médico.

🏗️ Arquitectura del Sistema

graph TD
    A[Frontend Web] --> B(API Gateway);
    B --> C(Patient Service);
    B --> D(Device Service);
    B --> E(Reading Service);
    C --> F(Eureka Server);
    D --> F;
    E --> F;
    F --> G(MySQL);

🚀 Microservicios
🌐 Gateway Service (Puerto 8087)
API Gateway Centralizado

Punto único de entrada al sistema

Enrutamiento inteligente y balanceador de carga

CORS y logging centralizado

Service discovery integrado

👥 Patient Service (Puerto 8081)
Gestión de Pacientes Diabéticos

Registro y actualización de pacientes

Información médica completa

Asignación de dispositivos

Contactos de emergencia

📦 Device Service (Puerto 8082)
Gestión de Bombas de Insulina

Registro de dispositivos médicos

Control de estados operativos

Configuraciones técnicas

Historial de mantenimiento

📊 Reading Service (Puerto 8083)
Monitoreo de Glucosa en Tiempo Real

Lecturas automáticas y manuales

Clasificación automática de estados

Alertas para emergencias médicas

Estadísticas y análisis

🗺️ Eureka Server (Puerto 8761)
Service Discovery

Registro automático de servicios

Load balancing

Health monitoring

Service discovery

🛠️ Stack Tecnológico
Backend

Java 21 - Lenguaje de programación

Spring Boot 3.4.5 - Framework principal

Spring Cloud Gateway - API Gateway

Spring Cloud Netflix Eureka - Service discovery

Spring Data JPA - Persistencia de datos

OpenFeign - Comunicación entre servicios

MySQL 8.0 - Base de datos relacional

Herramientas

Maven - Gestión de dependencias

Lombok - Reducción de código boilerplate

Bean Validation - Validación de datos

SLF4J - Logging

JUnit 5 - Testing

Mockito - Mocking para tests

📊 Base de Datos
Estructura por Microservicio

pacientes - Patient Service

dispositivos - Device Service

lecturas - Reading Service

Patrón Database per Service
Cada microservicio mantiene su propia base de datos, garantizando:

✅ Independencia de datos
✅ Escalabilidad individual
✅ Tolerancia a fallos
✅ Tecnologías específicas por servicio

🚀 Instalación y Ejecución
Prerequisitos

Java 21+

Maven 3.8+

MySQL 8.0+

Git

Clonar el Repositorio

git clone [URL_DEL_REPOSITORIO]
cd insulin-pump-microservices

Configurar MySQL

-- Crear las bases de datos
CREATE DATABASE pacientes CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE DATABASE dispositivos CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE DATABASE lecturas CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

-- Crear usuario (opcional)
CREATE USER 'insulin_user'@'localhost' IDENTIFIED BY '1234';
GRANT ALL PRIVILEGES ON pacientes.* TO 'insulin_user'@'localhost';
GRANT ALL PRIVILEGES ON dispositivos.* TO 'insulin_user'@'localhost';
GRANT ALL PRIVILEGES ON lecturas.* TO 'insulin_user'@'localhost';
FLUSH PRIVILEGES;

Ejecutar en Orden (IMPORTANTE)

# 1. Eureka Server (Service Discovery)
cd eureka-server
mvn spring-boot:run

# 2. Gateway Service (API Gateway)
cd ../gateway-service
mvn spring-boot:run

# 3. Patient Service
cd ../patient-service
mvn spring-boot:run

# 4. Device Service  
cd ../device-service
mvn spring-boot:run

# 5. Reading Service
cd ../reading-service
mvn spring-boot:run

Verificar el Sistema

Eureka Dashboard: http://localhost:8761

Gateway Health: http://localhost:8087/actuator/health

Patient Service: http://localhost:8087/api/patients

Device Service: http://localhost:8087/api/devices

Reading Service: http://localhost:8087/api/readings

🌐 Acceso a través del Gateway (RECOMENDADO)
| Servicio | URL Gateway                        | Puerto Directo                      |
| :------- | :--------------------------------- | :---------------------------------- |
| Patient  | http://localhost:8087/api/patients | http://localhost:8081/api/patients |
| Device   | http://localhost:8087/api/devices  | http://localhost:8082/api/devices  |
| Reading  | http://localhost:8087/api/readings | http://localhost:8083/api/readings |

Ventajas del Gateway
✅ Punto único de entrada
✅ Balanceador de carga automático
✅ CORS configurado
✅ Logging centralizado
✅ Enrutamiento inteligente

📋 Casos de Uso Principales
🏥 Flujo Médico Completo (usando Gateway)

Registro de Paciente
POST http://localhost:8087/api/patients

{
  "name": "Juan Carlos Pérez",
  "medicalId": "MED123456",
  "diabetesType": "Tipo 1",
  "hba1cLevel": 7.2
}

Registro de Dispositivo
POST http://localhost:8087/api/devices

{
  "serialNo": "DEV001",
  "model": "InsulinPump Pro 2024",
  "maxBasalRate": 5.0,
  "reservoirCapacity": 300
}

Asignación Dispositivo-Paciente
PUT http://localhost:8087/api/devices/1/assign/1

Monitoreo de Glucosa
POST http://localhost:8087/api/readings

{
  "glucoseLevel": 280.0,  // Crítico Alto
  "deviceId": 1,
  "notes": "Emergencia médica detectada"
}

Consulta de Alertas
GET http://localhost:8087/api/readings/requiring-action

🔍 Testing
Ejecutar Tests por Servicio

# Gateway Service
cd gateway-service && mvn test

# Patient Service
cd patient-service && mvn test

# Device Service  
cd device-service && mvn test

# Reading Service
cd reading-service && mvn test

Coverage Report
mvn test jacoco:report

📊 Monitoreo y Métricas
Health Checks

Gateway: http://localhost:8087/actuator/health

Patient: http://localhost:8081/actuator/health

Device: http://localhost:8082/actuator/health

Reading: http://localhost:8083/actuator/health

Eureka Dashboard
http://localhost:8761

Gateway Routes
http://localhost:8087/actuator/gateway/routes

Logs
Cada servicio genera logs detallados para:

Operaciones CRUD

Comunicación entre servicios

Errores y excepciones

Métricas de performance

🔒 Características de Seguridad
Validación de Datos

Bean Validation en todos los endpoints

Validación de formatos médicos

Sanitización de entradas

Manejo de Errores

Global Exception Handlers

Respuestas de error estructuradas

Logging de errores para auditoría

Comunicación Segura

Validación de servicios a través de Eureka

Timeouts configurables en Feign

Retry automático en fallos

CORS configurado en Gateway

🚨 Alertas Médicas Críticas
Emergencias Automáticas

Hipoglucemia Severa: < 50 mg/dL

Hiperglucemia Crítica: > 250 mg/dL

Fallas de Dispositivo: Sin lecturas por tiempo prolongado

Notificaciones

Marcado automático de requiresAction = true

Endpoint dedicado para lecturas críticas

Logs de alta prioridad para emergencias

📈 Estadísticas y Reportes
Métricas Disponibles

Promedio de glucosa por período

Desviación estándar

Conteo de lecturas por categoría

Tendencias temporales

Períodos de Análisis

Diario

Semanal

Mensual

Personalizado

🔄 Escalabilidad
Horizontal

Múltiples instancias por servicio

Load balancing automático vía Gateway

Base de datos distribuida

Service discovery automático

Vertical

Configuración de memoria por servicio

Optimización de queries JPA

Connection pooling optimizado

🚀 Despliegue
Desarrollo



🎯 Roadmap Futuro
Próximas Funcionalidades


Integraciones

[ ] HL7 FHIR para interoperabilidad

[ ] Sistemas hospitalarios existentes

[ ] Aplicaciones móviles para pacientes

[ ] Wearables y sensores IoT

📚 Documentación Adicional

Gateway Service Documentation

Patient Service Documentation

Device Service Documentation

Reading Service Documentation

API Collections

Database Schema

🤝 Contribución

Fork el proyecto

Crear feature branch (git checkout -b feature/nueva-funcionalidad)

Commit cambios (git commit -am 'Añadir nueva funcionalidad')

Push branch (git push origin feature/nueva-funcionalidad)

Crear Pull Request

📄 Licencia
Este proyecto está bajo la Licencia MIT. Ver LICENSE para más detalles.

👨‍💻 Desarrollador
Rafael Gamero Arrabal
📧 Email: [rafael.gamero@email.com]

🌐 Portfolio: [tu-portfolio.com]

📱 GitHub: [@rafael-gamero]

⭐ Agradecimientos
Gracias por revisar este sistema de microservicios. Si te ha resultado útil, ¡no olvides dar una estrella al repositorio!
¿Tienes preguntas o sugerencias? No dudes en contactarme a través de LinkedIn o crear un issue en el repositorio.
🏥 Sistema desarrollado con ❤️ para mejorar la atención médica de pacientes diabéticos

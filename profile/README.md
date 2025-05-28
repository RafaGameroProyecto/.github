# 🏥 Sistema de Microservicios para Bombas de Insulina

Sistema de monitoreo y gestión de bombas de insulina para pacientes diabéticos desarrollado con **Spring Boot** y **arquitectura de microservicios**.

## 🚀 Descripción

Plataforma médica que permite a hospitales monitorear pacientes diabéticos en tiempo real, gestionar dispositivos y generar alertas automáticas para emergencias médicas.

## 🏗️ Arquitectura

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   API Gateway   │    │   Patient       │    │   Device        │    │   Reading       │
│   Port: 8087    │◄──►│   Service       │    │   Service       │    │   Service       │
│  (Enrutamiento) │    │   Port: 8081    │    │   Port: 8082    │    │   Port: 8083    │
└─────────────────┘    └─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │                       │
         └───────────────────────┼───────────────────────┼───────────────────────┘
                                 │
                    ┌─────────────▼─────────────┐
                    │      Eureka Server        │
                    │       Port: 8761          │
                    └─────────────┬─────────────┘
                                 │
                    ┌─────────────▼─────────────┐
                    │        MySQL              │
                    │       Port: 3306          │
                    └───────────────────────────┘
```

## 🧬 Modelo de Datos (UML)

![Diagrama UML](https://github.com/RafaGameroProyecto/.github/blob/main/Captura%20de%20pantalla%202025-05-22%20102324.png?raw=true)

## 🛠️ Tecnologías

- **Java 21** + **Spring Boot 3.4.5**
- **Spring Cloud Gateway** (API Gateway)
- **Spring Cloud Eureka** (Service Discovery)
- **MySQL 8.0** (Base de datos)
- **OpenFeign** (Comunicación entre servicios)
- **JUnit 5** + **Mockito** (Testing)

## 📦 Microservicios

| Servicio | Puerto | Función | Endpoint Principal |
|----------|--------|---------|-------------------|
| **🌐 Gateway** | 8087 | Enrutamiento y balanceador | `http://localhost:8087` |
| **👥 Patient** | 8081 | Gestión de pacientes | `/api/patients` |
| **📦 Device** | 8082 | Gestión de bombas | `/api/devices` |
| **📊 Reading** | 8083 | Monitoreo de glucosa | `/api/readings` |
| **🗺️ Eureka** | 8761 | Service discovery | `http://localhost:8761` |

## ⚡ Inicio Rápido

### 1. Prerequisitos

Java 21+, Maven 3.8+, MySQL 8.0+


### 2. Configurar Base de Datos
```sql
CREATE DATABASE pacientes;
CREATE DATABASE dispositivos;
CREATE DATABASE lecturas;
```

### 3. Ejecutar Servicios (en orden)

    1. Eureka Server

    2. Gateway

    3. Microservicios (en paralelo)



### 4. Verificar
- **Dashboard:** http://localhost:8761
- **API Gateway:** http://localhost:8087
- **Health Check:** http://localhost:8087/actuator/health

## 📋 Casos de Uso Principales

### 🏥 Flujo Médico Típico
```http
# 1. Crear Paciente
POST http://localhost:8087/api/patients
{
  "name": "Juan Pérez",
  "medicalId": "MED123",
  "diabetesType": "Tipo 1"
}

# 2. Crear Dispositivo
POST http://localhost:8087/api/devices
{
  "serialNo": "DEV001",
  "model": "InsulinPump Pro",
  "maxBasalRate": 5.0
}

# 3. Asignar Dispositivo
PUT http://localhost:8087/api/devices/1/assign/1

# 4. Registrar Lectura
POST http://localhost:8087/api/readings
{
  "glucoseLevel": 280.0,  // Crítico Alto
  "deviceId": 1
}

# 5. Consultar Alertas
GET http://localhost:8087/api/readings/requiring-action
```

## 🚨 Características Médicas

### Estados de Glucosa Automáticos
- **🟢 NORMAL**: 70-180 mg/dL
- **🟡 LOW/HIGH**: 50-70 / 180-250 mg/dL
- **🔴 CRITICAL**: <50 / >250 mg/dL ⚠️ **Requiere Acción**

### Funcionalidades Clave
- ✅ **Monitoreo 24/7** en tiempo real
- ✅ **Alertas automáticas** para emergencias
- ✅ **Estadísticas médicas** (promedio, desviación estándar)
- ✅ **Historial completo** de lecturas
- ✅ **Gestión centralizada** de dispositivos






## 🔄 Escalabilidad

### Ventajas de la Arquitectura
- ✅ **🌐 API Gateway**: Punto único de entrada  
- ✅ **⚖️ Load Balancing**: Distribución automática de carga  
- ✅ **🔍 Service Discovery**: Registro automático de servicios  
- ✅ **💾 Database per Service**: Independencia de datos  
- ✅ **🔧 Microservicios**: Escalado independiente  

### Producción
- ✅ **Múltiples instancias por servicio**  
- ✅ **Balanceador de carga automático**  
- ✅ **Tolerancia a fallos**  
- ✅ **Monitoreo centralizado**





## 🎯 Beneficios del Sistema

### Para Hospitales
- ✅ **Monitoreo centralizado** de pacientes
- ✅ **Alertas en tiempo real** para emergencias
- ✅ **Optimización de recursos** médicos
- ✅ **Integración fácil** con sistemas existentes

### Para Pacientes
- ✅ **Monitoreo 24/7** automático
- ✅ **Respuesta rápida** en emergencias
- ✅ **Historial médico** completo
- ✅ **Mejor calidad** de vida

## 🚀 Próximos Pasos

- [ ] **Frontend Web** con React
- [ ] **Autenticación JWT**
- [ ] **Notificaciones Push**
- [ ] **Containerización Docker**
- [ ] **Dashboard de métricas**

## 📎 Recursos del Proyecto

- 🎨 **Presentación en Canva**:  
  [https://www.canva.com/design/DAGojYIwmhU/zPG2SRVziUawiQSkjmRYTg/edit?utm_content=DAGojYIwmhU&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton](https://www.canva.com/design/DAGojYIwmhU/zPG2SRVziUawiQSkjmRYTg/edit?utm_content=DAGojYIwmhU&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton)

- ✅ **Tablero del Proyecto en Trello**:  
  [https://trello.com/b/Nvasa05F/proyecto-bomba-insulina](https://trello.com/b/Nvasa05F/proyecto-bomba-insulina)

 
## 👨‍💻 Desarrollador

**Rafael Gamero Arrabal**  
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/rafael-gamero-arrabal-619200186/)

---

🏥 **Sistema desarrollado para mejorar la atención médica de pacientes diabéticos**



📱 GitHub: [https://github.com/Rafa-Gamero]

⭐ Agradecimientos
Gracias por revisar este sistema de microservicios. Si te ha resultado útil, ¡no olvides dar una estrella al repositorio!
¿Tienes preguntas o sugerencias? No dudes en contactarme a través de LinkedIn o crear un issue en el repositorio.
🏥 Sistema desarrollado con ❤️ para mejorar la atención médica de pacientes diabéticos

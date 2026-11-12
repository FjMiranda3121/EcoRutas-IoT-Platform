# ♻️ EcoRutas - IoT Smart Waste Management Platform

Plataforma integral de Internet de las Cosas (IoT) diseñada para el monitoreo inteligente de contenedores de residuos. El sistema mide en tiempo real la capacidad de los contenedores mediante sensores ultrasónicos, procesa la información a través de una API RESTful y la visualiza en paneles web interactivos para optimizar las rutas de recolección.

> 🏆 **Hito:** Prototipo funcional presentado en feria de emprendimiento e innovación (Octubre 2026).


## 🏗️ Arquitectura del Sistema

La solución está dividida en tres capas principales:

1. **Capa de Hardware (Edge/IoT):** Microcontroladores (Arduino UNO / ESP32) equipados con sensores ultrasónicos HC-SR04. Implementan lógica de filtrado de ruido (filtro de mediana) para garantizar lecturas de distancia precisas antes de transmitir los datos vía HTTP/Wi-Fi.
2. **Capa Backend (Core API):** API RESTful desarrollada en C# .NET 10. Se encarga de recibir la telemetría, gestionar la lógica de negocio y controlar el acceso mediante autenticación JWT y Control de Acceso Basado en Roles (RBAC).
3. **Capa Frontend (Presentación):** Interfaz web cliente construida con HTML, CSS y JavaScript nativo (`dashboard.html`, `operador.html`), que consume la API para mostrar métricas en tiempo real a los operadores y administradores.

## 🛠️ Stack Tecnológico

**Backend & Infraestructura**
* **Framework:** C# .NET 10 (ASP.NET Core Web API)
* **Base de Datos:** PostgreSQL (alojada en Neon)
* **Autenticación:** JSON Web Tokens (JWT) + BCrypt
* **Despliegue:** Render (`ecorutas-api.onrender.com`)

**Hardware & IoT**
* **Microcontroladores:** ESP32 / Arduino UNO
* **Sensores:** HC-SR04 (Ultrasónico)
* **Lenguaje:** C++ (Entorno Arduino/Wiring)

**Frontend**
* HTML5, CSS3, Vanilla JavaScript
* Fetch API para consumo de endpoints

## ⚙️ Características Principales

- **Monitoreo en Tiempo Real:** Actualización del nivel de llenado de los contenedores mediante telemetría IoT.
- **Seguridad y Accesos:** Sistema de login con tokens JWT y rutas protegidas por roles (Administrador, Operador, Recolector).
- **Procesamiento de Señal:** Algoritmo en C++ para mitigar lecturas erróneas del sensor ultrasónico mediante filtros estadísticos.
- **Gestión de Recolecciones:** Borrado lógico (híbrido) y actualización de estados para el seguimiento de rutas de recolección.

## 🚀 Configuración y Ejecución Local

### Prerrequisitos
- .NET 8 SDK
- PostgreSQL
- IDE de Arduino (para el código del microcontrolador)

### 1. Backend (API)
```bash
# Clonar el repositorio
git clone [https://github.com/FjMiranda3121/EcoRutas-IoT-Platform.git](https://github.com/FjMiranda3121/EcoRutas-IoT-Platform.git)
cd EcoRutas-IoT-Platform

# Configurar variables de entorno
# Crear un archivo appsettings.Development.json con tu cadena de conexión a PostgreSQL y tu JWT Secret.

# Compilar y ejecutar
dotnet build
dotnet run

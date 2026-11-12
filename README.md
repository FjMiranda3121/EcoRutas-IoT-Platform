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
- .NET 10 SDK
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
```
### 2. Configuración de Credenciales y Variables de Entorno

Antes de ejecutar el sistema, es obligatorio configurar las credenciales locales de la base de datos, la seguridad JWT y la conexión del hardware.

**Para el Backend (.NET 8):**
Crea un archivo `appsettings.Development.json` en la raíz de la carpeta del backend con la siguiente estructura, reemplazando con tus propios datos:

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Host=localhost;Database=ecorutas_db;Username=postgres;Password=tu_password"
  },
  "JwtSettings": {
    "SecretKey": "TU_CLAVE_SECRETA_SUPER_SEGURA_AQUI",
    "Issuer": "EcoRutasAPI",
    "Audience": "EcoRutasUsers"
  }
}
```
### 3. Configuración del Hardware (ESP32 / Arduino)

Sigue estos pasos para compilar y cargar el firmware en el microcontrolador.

### Prerrequisitos
- IDE de Arduino (v2.x recomendado).
- Paquete de tarjetas ESP32 instalado en el gestor de tarjetas.
- Cable de datos USB a Micro-USB/USB-C (con soporte de transferencia de datos).

## 1. Conexión del Hardware (Pinout)
Conecta el sensor ultrasónico HC-SR04 al ESP32 siguiendo esta configuración:
* **VCC:** 5V / VIN (o 3.3V dependiendo de la versión de tu sensor)
* **GND:** GND
* **TRIG:** Pin 5
* **ECHO:** Pin 18

## 2. Configuración de Credenciales
Crea un archivo llamado `secrets.h` en el mismo directorio de tu script `.ino` / `.cpp` principal. Este archivo es ignorado por Git para proteger tus redes Wi-Fi:

```cpp
#ifndef SECRETS_H
#define SECRETS_H

#define SECRET_SSID_1 "TU_WIFI_PRINCIPAL"
#define SECRET_PASS_1 "CONTRASEÑA_PRINCIPAL"

#define SECRET_SSID_2 "TU_WIFI_RESPALDO"
#define SECRET_PASS_2 "CONTRASEÑA_RESPALDO"

#endif
```

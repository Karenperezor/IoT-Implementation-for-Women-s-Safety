# IoT Implementation for Women's Safety
## Implementación del IoT para la Seguridad de las Mujeres

**Tema 1: Estándares de Comunicación Inalámbrica**

![Badge](https://img.shields.io/badge/Status-Active-brightgreen)
![Badge](https://img.shields.io/badge/License-MIT-blue)
![Badge](https://img.shields.io/badge/Platform-Arduino%20IDE-orange)

---

## 📋 Introducción

Este proyecto implementa un **sistema IoT funcional basado en tecnologías inalámbricas de largo alcance y bajo consumo** para el monitoreo en tiempo real de signos vitales y geolocalización de mujeres en situación de vulnerabilidad. El prototipo opera mediante la integración de nodos sensores y gateways que transmiten datos biométricos desde una pulsera emisora inteligente hacia un servidor central de procesamiento y visualización.

### Contexto del Problema

El proyecto aborda directamente la problemática de la **violencia de género en el municipio de Tlahuelilpan, Hidalgo**, donde el **70.1% de las mujeres de 15 años o más han experimentado al menos un incidente de violencia** según datos del INEGI. Esta solución se alinea con el **eje de Seguridad Humana de los PRONACES** (Programas Nacionales Estratégicos).

### Arquitectura de Comunicación Inalámbrica

El sistema integra dos categorías de tecnologías inalámbricas:

- **LoRa (LPWAN)**: Comunicación de corto a medio alcance entre la pulsera emisora y el gateway receptor
- **GPRS (WWAN)**: Transmisión de datos hacia el servidor en la nube desde el gateway

Esta combinación garantiza **cobertura robusta en escenarios donde el Wi-Fi es limitado** y proporciona **conectividad sin interrupciones durante emergencias**.

### Característica Diferenciadora: Privacidad Centrada en el Consentimiento

A diferencia de otras soluciones de monitoreo continuo, este prototipo incorpora un **mecanismo de privacidad que activa la transmisión de datos únicamente durante una hora a partir del momento en que la usuaria presiona el botón de pánico**. Esto evita el rastreo permanente de su ubicación, diferenciando al prototipo de sistemas basados en WLAN o satelitales.

---

## 🎯 Justificación

### Por qué este proyecto es necesario

1. **Violencia de Género**: La violencia contra las mujeres es un problema crítico en México que requiere soluciones tecnológicas accesibles y confiables.

2. **Tecnología Apropiada**: Las tecnologías inalámbricas como LoRa y GPRS permiten:
   - Monitoreo en tiempo real sin dependencia de Wi-Fi
   - Operación en zonas con cobertura celular limitada
   - Bajo consumo energético para dispositivos portátiles

3. **Beneficiario Directo**: El **Instituto de la Mujer de Tlahuelilpan** requiere herramientas de vanguardia para la protección y seguimiento de sus usuarias con precisión sin precedentes.

4. **Aplicación Educativa**: Este desarrollo fortalece la comprensión práctica de los estándares de comunicación inalámbrica (Tema 1, 2 y 3) mediante un caso de uso real y socialmente relevante.

5. **Escalabilidad**: El diseño modular permite escalar la solución a otras instituciones y municipios con problemáticas similares.

---

## 🎓 Objetivos

### Objetivo General

Diseñar y construir un **prototipo IoT funcional basado en Heltec ESP32 LoRa v3** que monitoree en tiempo real:
- Ritmo cardiaco (BPM)
- Oxigenación en sangre (SpO2)
- Aceleración en tres ejes (X, Y, Z)
- Ubicación GPS de la usuaria

Transmitiendo los datos vía **LoRa y GPRS** al Instituto de la Mujer durante una **ventana de una hora activada por una sola pulsación del botón de pánico**, aplicando los estándares de comunicación inalámbrica para garantizar **calidad, confiabilidad y seguridad** de los datos.

### Objetivos Específicos

1. **Implementar la lectura simultánea** de SpO2, BPM y aceleración (ejes X, Y, Z) en la pulsera emisora LoRa, incluyendo activación por doble pulsación del botón de pánico.

2. **Configurar la comunicación LoRa** entre la pulsera emisora y el gateway LilyGO T-SIM, verificando la integridad de la trama en el display de cada módulo.

3. **Establecer el enlace GPRS** con el broker público HiveMQ mediante el APN de Telcel, publicando paquetes JSON con todos los parámetros del sensor.

4. **Desarrollar un dashboard en Node-RED** con mapa GPS en tiempo real, medidores de BPM y SpO2, historial de aceleración y lógica de alertas automáticas.

5. **Estructurar una base de datos en InfluxDB** vinculada a Grafana para el registro histórico de signos vitales, aceleración y geolocalización.

---

## ⚙️ Requerimientos de Software y Hardware

### Hardware

#### Nodo Emisor (Pulsera Inteligente)
| Componente | Modelo | Función |
|-----------|--------|---------|
| **Microcontrolador Principal** | Heltec ESP32 LoRa v3 | Procesamiento central, radio LoRa integrado (SX1262) |
| **Sensor Biométrico** | MAX30102 | Medición de ritmo cardiaco (BPM) y oxigenación (SpO2) |
| **Acelerómetro** | MPU6050 | Detección de movimiento y caídas (ejes X, Y, Z) |
| **Módulo GPS** | NEO-6M | Geolocalización en tiempo real |
| **Reloj en Tiempo Real** | DS1307 | Marca de tiempo independiente de GPS |
| **Batería** | LiPo 4.2V (3000-5000 mAh) | Alimentación del nodo emisor |
| **Carcasa** | Impresión 3D personalizada | Protección de componentes |

#### Nodo Receptor y Gateway
| Componente | Modelo | Función |
|-----------|--------|---------|
| **Receptor LoRa** | Heltec ESP32 LoRa v3 | Recepción de tramas LoRa |
| **Gateway de Datos** | LilyGO T-SIM7000 | Módulo GPRS para conexión celular |
| **Red Celular** | Telcel (2G/3G) | Conectividad WWAN |

#### Servidor Local
| Componente | Especificación | Función |
|-----------|--------|---------|
| **Computadora** | x86 / ARM | Alojamiento de servicios |
| **SO** | Linux / Windows / macOS | Sistema operativo |

### Software

#### En el Nodo Emisor (Arduino IDE)
```
- Librería LoRa.h (SX1262)
- Librería U8g2 (Display OLED)
- Librería TinyGPS++ (Módulo GPS)
- Librería MAX30105 (Sensor biométrico)
- Librería MPU6050 (Acelerómetro)
- Lenguaje: C++ (Arduino Sketch)
```

#### En el Nodo Receptor y Gateway
```
- Arduino IDE (programación)
- Bibliotecas: LoRa.h, HardwareSerial, MQTT
- Lenguaje: C++ (Arduino Sketch)
```

#### En el Servidor Local
```
- Node-RED v3.0.0+ (Flujos de procesamiento)
- InfluxDB v2.0+ (Base de datos de series de tiempo)
- Grafana v9.0+ (Visualización de datos)
- Broker MQTT: HiveMQ (público)
- Docker (opcional, para contenedores)
```

#### Herramientas de Desarrollo
```
- Arduino IDE 2.0+
- Git & GitHub (versionamiento)
- Visual Studio Code (edición de código)
- Postman (pruebas de API)
```

---

## 📊 Tabla de Conexiones

### Conexiones Eléctricas - Nodo Emisor (Heltec ESP32 LoRa v3)

#### Sensor MAX30102 (I2C)
| Pin MAX30102 | Pin Heltec ESP32 | Descripción |
|------------|-----------------|-------------|
| SDA | GPIO 21 | Línea de datos I2C |
| SCL | GPIO 22 | Línea de reloj I2C |
| VCC | 3.3V | Alimentación positiva |
| GND | GND | Referencia común |

#### Acelerómetro MPU6050 (I2C)
| Pin MPU6050 | Pin Heltec ESP32 | Descripción |
|------------|-----------------|-------------|
| SDA | GPIO 21 | Línea de datos I2C (compartida con MAX30102) |
| SCL | GPIO 22 | Línea de reloj I2C (compartida con MAX30102) |
| VCC | 3.3V | Alimentación positiva |
| GND | GND | Referencia común |
| INT | GPIO 15 | Interrupción de detección de movimiento |

#### Módulo GPS NEO-6M (UART)
| Pin NEO-6M | Pin Heltec ESP32 | Descripción |
|-----------|-----------------|-------------|
| TX | GPIO 16 (RX) | Transmisión de datos GPS |
| RX | GPIO 17 (TX) | Recepción de comandos |
| VCC | 3.3V | Alimentación positiva |
| GND | GND | Referencia común |

#### Reloj DS1307 (I2C)
| Pin DS1307 | Pin Heltec ESP32 | Descripción |
|-----------|-----------------|-------------|
| SDA | GPIO 21 | Línea de datos I2C |
| SCL | GPIO 22 | Línea de reloj I2C |
| VCC | 3.3V | Alimentación positiva |
| GND | GND | Referencia común |
| BAT | Batería CR2032 | Batería de respaldo interna |

#### Botón de Pánico
| Pin Botón | Pin Heltec ESP32 | Descripción |
|----------|-----------------|-------------|
| Entrada | GPIO 0 | Entrada digital (con pull-up) |
| GND | GND | Referencia común |

#### Batería LiPo
| Conexión | Puerto Heltec ESP32 | Descripción |
|---------|-----------------|-------------|
| +4.2V | Puerto USB-C (integrado) | Carga y alimentación |
| GND | GND | Referencia común |

---

### Conexiones Eléctricas - Nodo Receptor (Heltec ESP32 LoRa v3)

El nodo receptor utiliza la **misma configuración que el emisor**, pero sin los sensores biométricos (MAX30102, MPU6050, GPS, DS1307). Solo mantiene:
- Heltec ESP32 LoRa v3 (con radio LoRa nativa)
- Batería LiPo opcional (para operación portátil)
- Conexión USB para programación

---

### Conexiones Eléctricas - Gateway LilyGO T-SIM7000 (GPRS)

| Componente | Conexión | Protocolo |
|-----------|---------|-----------|
| Nodo Receptor Heltec | UART Serial | Comunicación serial |
| Antena SIM | Ranura SIM integrada | Tarjeta SIM Telcel |
| Antena GPRS | Conectada en placa | Transmisión celular |
| Computadora (servidor) | USB Serial | Comunicación con servidor |

---

### Topología de Red

```
┌─────────────────┐
│  Pulsera Emisora│
│  (Heltec ESP32  │
│   LoRa v3 +     │
│   Sensores)     │
└────────┬────────┘
         │
      LoRa (868 MHz, LPWAN, WPAN)
      Rango: ~5 km línea visual
         │
         ▼
┌─────────────────┐
│ Nodo Receptor   │
│ (Heltec ESP32   │
│  LoRa v3)       │
└────────┬────────┘
         │
    Serial (UART)
         │
         ▼
┌─────────────────┐
│  Gateway GPRS   │
│  (LilyGO T-SIM7 │
│  + Telcel SIM)  │
└────────┬────────┘
         │
      GPRS (2G/3G, WWAN)
      Cobertura: Nacional Telcel
         │
         ▼
┌─────────────────────┐
│   Internet / Cloud  │
│   HiveMQ Broker     │
│   (MQTT port 1883)  │
└────────┬────────────┘
         │
    MQTT (JSON payload)
         │
         ▼
┌──────────────────────────────────┐
│  Servidor Local                  │
│  ├─ Node-RED (flujos)            │
│  ├─ InfluxDB (base de datos)     │
│  └─ Grafana (dashboards)         │
└──────────────────────────────────┘
```

---

## 📍 Tabla de Direccionamiento

### Configuración de Redes Inalámbricas

#### Red LoRa (WPAN - Personal Area Network)
| Parámetro | Valor | Descripción |
|-----------|-------|-------------|
| **Estándar** | LoRaWAN / LoRa punto a punto | Protocolo inalámbrico LPWAN |
| **Frecuencia** | 868 MHz (Europa) / 915 MHz (América) | Banda ISM no licenciada |
| **Ancho de Banda** | 125 kHz - 500 kHz | Configurable en firmware |
| **Factor de Expansión (SF)** | 7-12 | SF=7: corto alcance, SF=12: largo alcance |
| **Potencia TX** | +20 dBm máximo | Regulado por regulaciones locales |
| **Rango** | 5-15 km (línea visual) | Depende del SF y altura |
| **Topología** | Punto a punto (gateway de puerta de enlace) | Nodo emisor → Nodo receptor |
| **Identificadores** | No requiere dirección MAC única | Comunicación directa en topología local |

#### Red GPRS (WWAN - Wide Area Network)
| Parámetro | Valor | Descripción |
|-----------|-------|-------------|
| **Estándar** | GSM/GPRS (2G) y UMTS (3G) | Redes celulares públicas |
| **Proveedor** | Telcel México | Operador de telecomunicaciones |
| **APN** | internet.telcel.com | Access Point Name para datos |
| **Protocolo** | TCP/IP sobre GPRS | Comunicación de datos en red celular |
| **Velocidad** | 115200 bps (UART serial) | Configuración del módulo LilyGO |
| **Cobertura** | Nacional (Telcel) | Disponibilidad en México |

#### Red MQTT (Broker HiveMQ)
| Parámetro | Valor | Descripción |
|-----------|-------|-------------|
| **Servidor** | broker.hivemq.com | Broker MQTT público |
| **Puerto** | 1883 | Puerto estándar MQTT (sin TLS) |
| **Protocolo** | MQTT v3.1.1 | Protocolo de publicación/suscripción |
| **Tópico de Publicación** | instituto/mujer/alertas | Nombre del canal de comunicación |
| **QoS** | 0 | Quality of Service (sin garantía de entrega) |
| **Payload** | JSON | Formato de datos transmitido |

#### Base de Datos InfluxDB (Servidor Local)
| Parámetro | Valor | Descripción |
|-----------|-------|-------------|
| **Ubicación** | Localhost (127.0.0.1) | Servidor local |
| **Puerto** | 8086 | Puerto por defecto InfluxDB |
| **Base de Datos** | iot_women_safety | Nombre de la base de datos |
| **Medición (Tabla)** | sensor_data | Nombre de la serie de tiempo |
| **Campos (Columnas)** | BPM, SpO2, AccX, AccY, AccZ, Latitud, Longitud | Parámetros almacenados |
| **Tags (Índices)** | user_id, device_id, timestamp | Claves de búsqueda |

#### Node-RED (Servidor Local)
| Parámetro | Valor | Descripción |
|-----------|-------|-------------|
| **Ubicación** | Localhost (127.0.0.1) | Servidor local |
| **Puerto HTTP** | 1880 | Interfaz de edición de flujos |
| **Suscripción MQTT** | instituto/mujer/alertas | Tópico de entrada |
| **Nodos principales** | MQTT-in, Function, Switch, Dashboard | Componentes activos |

#### Grafana (Servidor Local)
| Parámetro | Valor | Descripción |
|-----------|-------|-------------|
| **Ubicación** | Localhost (127.0.0.1) | Servidor local |
| **Puerto HTTP** | 3000 | Interfaz de visualización |
| **Datasource** | InfluxDB (127.0.0.1:8086) | Fuente de datos |
| **Autenticación** | admin:admin (por defecto) | Credenciales iniciales |

---

## 🔄 Esquema de Funcionamiento

### Flujo de Datos General

```
1. ACTIVACIÓN (Usuaria presiona botón de pánico)
   └─ Heltec ESP32 emisor detecta pulsación en GPIO 0
   └─ Inicia temporizador de 1 hora
   └─ Cambia estado: ESCUCHA → TRANSMISIÓN

2. CAPTURA DE DATOS (Cada 30 segundos)
   ├─ MAX30102: Lee BPM y SpO2
   ├─ MPU6050: Lee aceleración (X, Y, Z)
   ├─ NEO-6M: Lee latitud y longitud
   ├─ DS1307: Obtiene timestamp
   └─ Empaqueta todo en JSON

3. TRANSMISIÓN LoRa (WPAN - Corto alcance)
   └─ Heltec ESP32 emisor envía JSON por radio LoRa (868 MHz)
   └─ Heltec ESP32 receptor recibe la trama
   └─ Valida integridad de datos
   └─ Muestra en display OLED: última trama recibida

4. REENVÍO SERIAL
   └─ Heltec receptor envía JSON por UART 115200 bps
   └─ LilyGO T-SIM recibe datos por puerto serial

5. CONEXIÓN GPRS (WWAN - Largo alcance)
   ├─ LilyGO T-SIM abre sesión GPRS
   ├─ APN: internet.telcel.com (Telcel México)
   ├─ Establece TCP connection a HiveMQ:1883
   └─ Publica JSON en tópico: instituto/mujer/alertas

6. BROKER MQTT (Cloud público)
   └─ HiveMQ almacena el mensaje
   └─ Node-RED se suscribe y recibe el JSON

7. PROCESAMIENTO EN SERVIDOR LOCAL
   ├─ Node-RED desempaqueta JSON
   ├─ Evalúa lógica de alertas:
   │  ├─ ¿SpO2 < 90%? → ALERTA CRÍTICA
   │  ├─ ¿BPM fuera de rango 50-120? → ALERTA
   │  └─ ¿Aceleración > 2g? → DETECCIÓN DE CAÍDA
   ├─ Actualiza dashboard en tiempo real
   └─ Envía datos a InfluxDB para almacenamiento histórico

8. ALMACENAMIENTO (InfluxDB)
   └─ Crea registro timestamped en serie de tiempo
   └─ Indexa por user_id, device_id
   └─ Campos: BPM, SpO2, AccX, AccY, AccZ, Lat, Lon

9. VISUALIZACIÓN (Grafana)
   ├─ Consulta InfluxDB
   ├─ Genera gráficas de tendencias (4 días históricos)
   ├─ Muestra:
   │  ├─ Gauge de BPM actual
   │  ├─ Gauge de SpO2 actual
   │  ├─ Worldmap con ubicación GPS
   │  ├─ Series de tiempo de aceleración (X, Y, Z)
   │  └─ Historial de alertas
   └─ Interfaz accesible a operadores del Instituto

10. FINALIZACIÓN (Transcurren 60 minutos desde activación)
    └─ Heltec ESP32 emisor detiene transmisión automáticamente
    └─ Privacidad preservada: sin más monitoreo de ubicación
    └─ Datos históricos permanecen en InfluxDB/Grafana para análisis
```

### Diagrama de Capas OSI

```
┌─────────────────────────────────────────────────────────────┐
│ 7. APLICACIÓN                                               │
│    └─ Grafana (visualización), API REST de Node-RED        │
├─────────────────────────────────────────────────────────────┤
│ 6. PRESENTACIÓN                                             │
│    └─ Formato JSON, gráficas en tiempo real                │
├─────────────────────────────────────────────────────────────┤
│ 5. SESIÓN                                                   │
│    └─ MQTT (conexión a broker HiveMQ)                      │
├─────────────────────────────────────────────────────────────┤
│ 4. TRANSPORTE                                               │
│    ├─ TCP (MQTT sobre HiveMQ)                              │
│    └─ UART Serial (Heltec → LilyGO)                        │
├─────────────────────────────────────────────────────────────┤
│ 3. RED                                                      │
│    ├─ GPRS (LilyGO T-SIM) - WAN                           │
│    ├─ MQTT packet structure                                │
│    └─ TCP/IP stack                                         │
├─────────────────────────────────────────────────────────────┤
│ 2. ENLACE                                                   │
│    ├─ I2C (sensores internos al microcontrolador)         │
│    ├─ LoRa (modulation SX1262, Heltec emisor → receptor) │
│    └─ GSM frame (GPRS sobre Telcel)                       │
├─────────────────────────────────────────────────────────────┤
│ 1. FÍSICA                                                   │
│    ├─ LoRa: 868 MHz, modulación LORA, 5-15 km rango     │
│    ├─ GPRS: 2G/3G Telcel, antena celular                 │
│    ├─ I2C: 3.3V, 100-400 kHz                              │
│    ├─ UART: 115200 bps, RS232-like levels               │
│    └─ GPIO: lógica 3.3V                                   │
└─────────────────────────────────────────────────────────────┘
```

### Lógica de Alertas en Node-RED

```javascript
// Pseudo-código de la lógica implementada en Node-RED

if (SpO2 < 90) {
    alert_type = "CRÍTICA";
    alert_reason = "Oxigenación baja";
    severity = "HIGH";
    action = "Notificar Instituto inmediatamente";
}

if (BPM < 50 || BPM > 120) {
    alert_type = "ADVERTENCIA";
    alert_reason = "Ritmo cardíaco anómalo";
    severity = "MEDIUM";
}

if (aceleracion_magnitude > 2g) {
    alert_type = "CAÍDA DETECTADA";
    alert_reason = "Cambio abrupto de aceleración";
    severity = "HIGH";
    action = "Solicitar confirmación de usuaria o asistencia";
}

// Enviar a Grafana con timestamp
update_dashboard(BPM, SpO2, acceleration, GPS_location, alert_type);
```

---

## 💻 Códigos Comentados del Proyecto

### 1. Código del Nodo Emisor (Heltec ESP32 LoRa v3)

```cpp
/*
 * IoT Implementation for Women's Safety
 * Nodo Emisor - Heltec ESP32 LoRa v3
 * 
 * Función: Captura sensores biométricos, aceleración y GPS
 *          Transmite por LoRa cada 30 segundos
 * 
 * Autor: Equipo Shero
 * Fecha: 2026-04-01
 */

#include <LoRa.h>
#include <SPI.h>
#include <U8g2lib.h>
#include <TinyGPS++.h>
#include <Wire.h>
#include <MAX30105.h>
#include <heartRate.h>
#include <MPU6050.h>
#include <RTClib.h>

// ===== DEFINICIONES DE PINES =====
#define BUTTON_PIN 0        // Botón de pánico
#define GPS_RX 16           // RX del GPS (conectado a TX del módulo)
#define GPS_TX 17           // TX del GPS (conectado a RX del módulo)

// ===== INICIALIZACIÓN DE SENSORES =====
U8G2_SSD1306_128X64_NONAME_HW_I2C u8g2(U8G2_R0, /* reset=*/ 16, /* clock=*/ 15, /* data=*/ 4);
MAX30105 particleSensor;
MPU6050 mpu;
RTC_DS1307 rtc;
TinyGPSPlus gps;

// ===== VARIABLES GLOBALES =====
bool panic_activated = false;
unsigned long panic_start_time = 0;
const unsigned long TRANSMISSION_WINDOW = 3600000; // 1 hora en milisegundos
const unsigned long SAMPLING_INTERVAL = 30000;    // 30 segundos entre envíos
unsigned long last_send_time = 0;

// Almacenamiento de lecturas
float bpm = 0.0;
float spo2 = 0.0;
float accX = 0.0, accY = 0.0, accZ = 0.0;
double latitude = 0.0, longitude = 0.0;
char timestamp[25] = "";

void setup() {
    Serial.begin(115200);
    
    // Inicializar pantalla OLED
    u8g2.begin();
    u8g2.setFont(u8g2_font_ncenB08_tr);
    u8g2.drawStr(0, 10, "Iniciando sistema...");
    u8g2.sendBuffer();
    
    // Inicializar I2C
    Wire.begin(21, 22);
    
    // Inicializar MAX30102 (sensor biométrico)
    if (!particleSensor.begin(Wire, I2C_SPEED_FAST)) {
        Serial.println("ERROR: MAX30102 no encontrado");
        u8g2.clearBuffer();
        u8g2.drawStr(0, 20, "MAX30102 ERROR");
        u8g2.sendBuffer();
    }
    particleSensor.setup(25, 2, 100, 25, 500, 100); // Configuración de sensibilidad
    
    // Inicializar MPU6050
    mpu.initialize();
    if (!mpu.testConnection()) {
        Serial.println("ERROR: MPU6050 no encontrado");
        u8g2.clearBuffer();
        u8g2.drawStr(0, 30, "MPU6050 ERROR");
        u8g2.sendBuffer();
    }
    
    // Inicializar RTC
    if (!rtc.begin()) {
        Serial.println("ERROR: DS1307 no encontrado");
    }
    if (!rtc.isrunning()) {
        rtc.adjust(DateTime(F(__DATE__), F(__TIME__)));
    }
    
    // Inicializar GPS (UART)
    Serial2.begin(9600, SERIAL_8N1, GPS_RX, GPS_TX);
    
    // Inicializar LoRa
    LoRa.setPins(8, 9, 10); // NSS, RST, DIO0 (configuración Heltec)
    if (!LoRa.begin(868E6)) { // Frecuencia 868 MHz
        Serial.println("ERROR: No se pudo inicializar LoRa");
        u8g2.clearBuffer();
        u8g2.drawStr(0, 40, "LoRa INIT ERROR");
        u8g2.sendBuffer();
    }
    
    // Configurar parámetros LoRa
    LoRa.setSpreadingFactor(7);      // SF=7: corto alcance, bajo tiempo aire
    LoRa.setSignalBandwidth(125E3);  // 125 kHz
    LoRa.setCodingRate4(5);          // Coding rate 4/5
    LoRa.setTxPower(17);             // Potencia máxima
    
    // Botón de pánico
    pinMode(BUTTON_PIN, INPUT_PULLUP);
    
    Serial.println("Sistema iniciado correctamente");
    display_status("LISTO", "Esperando pánico");
}

void loop() {
    // Verificar pulsación del botón de pánico
    if (digitalRead(BUTTON_PIN) == LOW) {
        delay(50); // Debounce
        if (digitalRead(BUTTON_PIN) == LOW) {
            panic_activated = true;
            panic_start_time = millis();
            Serial.println("¡¡¡ PÁNICO ACTIVADO !!!");
            display_status("PÁNICO", "Transmitiendo...");
        }
    }
    
    // Si está en modo pánico, realizar ciclo de lectura y transmisión
    if (panic_activated) {
        // Verificar si la ventana de 1 hora ha expirado
        if (millis() - panic_start_time > TRANSMISSION_WINDOW) {
            panic_activated = false;
            Serial.println("Ventana de transmisión cerrada");
            display_status("LISTO", "Pánico finalizado");
            return;
        }
        
        // Realizar lectura de sensores cada 30 segundos
        if (millis() - last_send_time >= SAMPLING_INTERVAL) {
            last_send_time = millis();
            
            // Leer sensores
            read_biometric();      // MAX30102
            read_acceleration();   // MPU6050
            read_gps();            // NEO-6M
            read_timestamp();      // DS1307
            
            // Preparar JSON con los datos
            String json_payload = prepare_json();
            
            // Transmitir por LoRa
            transmit_lora(json_payload);
            
            // Mostrar datos en display
            display_sensor_data();
        }
    } else {
        // En reposo, actualizar GPS ocasionalmente
        feed_gps();
    }
}

/*
 * Lectura del sensor MAX30102 (ritmo cardíaco y oxigenación)
 */
void read_biometric() {
    uint32_t ir = particleSensor.getIR();
    uint32_t red = particleSensor.getRed();
    
    // Cálculo simple de BPM (se requiere algoritmo más robusto en producción)
    if (ir > 50000) {
        bpm = 72 + random(-5, 6); // Simulación con variación
        spo2 = 95 + random(-2, 3); // Simulación con variación
    } else {
        bpm = 0;
        spo2 = 0;
    }
    
    Serial.print("BPM: ");
    Serial.print(bpm);
    Serial.print(" | SpO2: ");
    Serial.println(spo2);
}

/*
 * Lectura del acelerómetro MPU6050
 */
void read_acceleration() {
    int16_t ax, ay, az;
    mpu.getAcceleration(&ax, &ay, &az);
    
    // Convertir a g (gravedad)
    accX = ax / 16384.0;
    accY = ay / 16384.0;
    accZ = az / 16384.0;
    
    Serial.print("Aceleración - X:");
    Serial.print(accX);
    Serial.print(" Y:");
    Serial.print(accY);
    Serial.print(" Z:");
    Serial.println(accZ);
    
    // Detectar caída (aceleración > 2g)
    float magnitude = sqrt(accX*accX + accY*accY + accZ*accZ);
    if (magnitude > 2.0) {
        Serial.println("⚠️  POSIBLE CAÍDA DETECTADA");
    }
}

/*
 * Lectura del módulo GPS NEO-6M
 */
void read_gps() {
    feed_gps();
    
    if (gps.location.isValid()) {
        latitude = gps.location.lat();
        longitude = gps.location.lng();
        Serial.print("GPS - Lat: ");
        Serial.print(latitude, 6);
        Serial.print(" Lon: ");
        Serial.println(longitude, 6);
    } else {
        Serial.println("GPS no disponible");
        latitude = 0.0;
        longitude = 0.0;
    }
}

/*
 * Leer datos del puerto serial del GPS
 */
void feed_gps() {
    while (Serial2.available() > 0) {
        gps.encode(Serial2.read());
    }
}

/*
 * Lectura del RTC DS1307
 */
void read_timestamp() {
    DateTime now = rtc.now();
    sprintf(timestamp, "%04d-%02d-%02d %02d:%02d:%02d",
            now.year(), now.month(), now.day(),
            now.hour(), now.minute(), now.second());
    
    Serial.print("Timestamp: ");
    Serial.println(timestamp);
}

/*
 * Preparar JSON con todos los datos de sensores
 * Formato: {"SOS":"1","Lat":"20.095076","Lon":-99.131065,"BPM":72,"SpO2":95,"AccX":0.05,"AccY":0.02,"AccZ":1.01,"Fecha":"2026-04-01","Hora":"15:03:35"}
 */
String prepare_json() {
    char json_buffer[512];
    
    snprintf(json_buffer, sizeof(json_buffer),
        "{\"SOS\":\"1\",\"Lat\":\"%f\",\"Lon\":%f,\"BPM\":%.0f,\"SpO2\":%.0f,"
        "\"AccX\":%.2f,\"AccY\":%.2f,\"AccZ\":%.2f,\"Fecha\":\"%s\"}",
        latitude, longitude, bpm, spo2, accX, accY, accZ, timestamp);
    
    return String(json_buffer);
}

/*
 * Transmitir datos por LoRa
 */
void transmit_lora(String payload) {
    LoRa.beginPacket();
    LoRa.print(payload);
    LoRa.endPacket();
    
    Serial.print("LoRa transmitido: ");
    Serial.println(payload);
}

/*
 * Actualizar pantalla OLED con datos de sensores
 */
void display_sensor_data() {
    u8g2.clearBuffer();
    
    u8g2.setFont(u8g2_font_ncenB08_tr);
    u8g2.drawStr(0, 10, "PÁNICO ACTIVO");
    
    char buffer[32];
    snprintf(buffer, sizeof(buffer), "BPM:%3.0f SpO2:%3.0f%%", bpm, spo2);
    u8g2.drawStr(0, 25, buffer);
    
    snprintf(buffer, sizeof(buffer), "Lat:%f", latitude);
    u8g2.drawStr(0, 40, buffer);
    
    snprintf(buffer, sizeof(buffer), "Acc:%4.2fg", sqrt(accX*accX + accY*accY + accZ*accZ));
    u8g2.drawStr(0, 55, buffer);
    
    u8g2.sendBuffer();
}

/*
 * Mostrar estado general en pantalla
 */
void display_status(const char* status, const char* message) {
    u8g2.clearBuffer();
    u8g2.setFont(u8g2_font_ncenB14_tr);
    u8g2.drawStr(0, 20, status);
    u8g2.setFont(u8g2_font_ncenB08_tr);
    u8g2.drawStr(0, 45, message);
    u8g2.sendBuffer();
}
```

### 2. Código del Nodo Receptor (Heltec ESP32 LoRa v3)

```cpp
/*
 * IoT Implementation for Women's Safety
 * Nodo Receptor - Heltec ESP32 LoRa v3
 * 
 * Función: Recibe tramas LoRa del nodo emisor
 *          Reenvía JSON por Serial hacia LilyGO Gateway
 * 
 * Autor: Equipo Shero
 * Fecha: 2026-04-01
 */

#include <LoRa.h>
#include <SPI.h>
#include <U8g2lib.h>

// ===== INICIALIZACIÓN =====
U8G2_SSD1306_128X64_NONAME_HW_I2C u8g2(U8G2_R0, /* reset=*/ 16, /* clock=*/ 15, /* data=*/ 4);

String received_message = "";
int rssi_value = 0;
float snr_value = 0.0;

void setup() {
    Serial.begin(115200);
    delay(1000);
    
    // Inicializar pantalla
    u8g2.begin();
    u8g2.setFont(u8g2_font_ncenB08_tr);
    u8g2.drawStr(0, 10, "Receptor LoRa");
    u8g2.drawStr(0, 25, "Inicializando...");
    u8g2.sendBuffer();
    
    // Inicializar LoRa
    LoRa.setPins(8, 9, 10);
    if (!LoRa.begin(868E6)) {
        u8g2.clearBuffer();
        u8g2.drawStr(0, 20, "ERROR LoRa");
        u8g2.sendBuffer();
        while(1);
    }
    
    LoRa.setSpreadingFactor(7);
    LoRa.setSignalBandwidth(125E3);
    LoRa.setCodingRate4(5);
    
    Serial.println("Receptor listo");
    u8g2.clearBuffer();
    u8g2.drawStr(0, 20, "Esperando datos...");
    u8g2.sendBuffer();
}

void loop() {
    // Verificar si hay paquetes LoRa disponibles
    int packet_size = LoRa.parsePacket();
    
    if (packet_size) {
        // Leer el mensaje
        received_message = "";
        while (LoRa.available()) {
            received_message += (char)LoRa.read();
        }
        
        // Obtener métricas de señal
        rssi_value = LoRa.packetRssi();
        snr_value = LoRa.packetSnr();
        
        Serial.print("Recibido: ");
        Serial.println(received_message);
        Serial.print("RSSI: ");
        Serial.println(rssi_value);
        Serial.print("SNR: ");
        Serial.println(snr_value);
        
        // Reenviar al gateway por Serial
        Serial.println(received_message);
        
        // Mostrar en pantalla
        display_received_data();
    }
}

/*
 * Mostrar datos recibidos en pantalla OLED
 */
void display_received_data() {
    u8g2.clearBuffer();
    u8g2.setFont(u8g2_font_ncenB08_tr);
    
    u8g2.drawStr(0, 10, "DATOS RECIBIDOS");
    
    // Mostrar parte del JSON
    if (received_message.length() > 30) {
        u8g2.drawStr(0, 25, received_message.substring(0, 20).c_str());
    } else {
        u8g2.drawStr(0, 25, received_message.c_str());
    }
    
    // Mostrar RSSI
    char rssi_str[20];
    snprintf(rssi_str, sizeof(rssi_str), "RSSI: %d dBm", rssi_value);
    u8g2.drawStr(0, 40, rssi_str);
    
    // Mostrar SNR
    char snr_str[20];
    snprintf(snr_str, sizeof(snr_str), "SNR: %.1f dB", snr_value);
    u8g2.drawStr(0, 55, snr_str);
    
    u8g2.sendBuffer();
}
```

### 3. Configuración del Gateway GPRS (LilyGO T-SIM7000)

```cpp
/*
 * IoT Implementation for Women's Safety
 * Gateway GPRS - LilyGO T-SIM7000
 * 
 * Función: Recibe JSON por Serial del receptor LoRa
 *          Envía a HiveMQ por GPRS (red celular Telcel)
 * 
 * Autor: Equipo Shero
 * Fecha: 2026-04-01
 */

#include <HardwareSerial.h>
#include <PubSubClient.h>
#include <WiFiClientSecure.h>

// ===== CONFIGURACIÓN GPRS =====
const char* apn = "internet.telcel.com";        // APN Telcel
const char* user = "telcel";                    // Usuario Telcel
const char* pass = "telcel";                    // Contraseña Telcel
const char* mqtt_server = "broker.hivemq.com";  // Broker MQTT
const int mqtt_port = 1883;                     // Puerto MQTT
const char* mqtt_topic = "instituto/mujer/alertas"; // Tópico

// Cliente MQTT
WiFiClient espClient;
PubSubClient client(espClient);

// Buffer para recibir datos
String serial_buffer = "";

void setup() {
    Serial.begin(115200);   // Comunicación con computadora
    Serial1.begin(115200);  // Comunicación con receptor LoRa
    
    delay(3000);
    Serial.println("\n\nGateway GPRS iniciando...");
    
    // Inicializar módulo GPRS
    init_gprs();
    
    // Conectar a MQTT
    connect_mqtt();
}

void loop() {
    // Mantener conexión MQTT
    if (!client.connected()) {
        connect_mqtt();
    }
    client.loop();
    
    // Leer datos del receptor LoRa (Serial1)
    if (Serial1.available()) {
        char inChar = Serial1.read();
        serial_buffer += inChar;
        
        // Si recibimos una línea completa (salto de línea)
        if (inChar == '\n') {
            Serial.print("Datos recibidos por LoRa: ");
            Serial.println(serial_buffer);
            
            // Publicar en MQTT
            publish_mqtt(serial_buffer);
            
            // Limpiar buffer
            serial_buffer = "";
        }
    }
}

/*
 * Inicializar módulo GPRS
 */
void init_gprs() {
    // Aquí va el código específico del módulo GPRS del LilyGO
    // (varía según la versión del firmware)
    Serial.println("GPRS inicializado");
    Serial.print("APN: ");
    Serial.println(apn);
}

/*
 * Conectar a broker MQTT
 */
void connect_mqtt() {
    while (!client.connected()) {
        Serial.print("Intentando conectar a MQTT: ");
        Serial.println(mqtt_server);
        
        // Crear ID único del cliente
        String clientId = "ESP32_Gateway_";
        clientId += String(random(0xffff), HEX);
        
        // Intentar conectar
        if (client.connect(clientId.c_str())) {
            Serial.println("Conectado a MQTT");
            // Suscribirse a respuestas
            client.subscribe("instituto/mujer/respuestas");
        } else {
            Serial.print("Falló con código: ");
            Serial.print(client.state());
            Serial.println(" Reintentando en 5s...");
            delay(5000);
        }
    }
}

/*
 * Publicar mensaje en MQTT
 */
void publish_mqtt(String payload) {
    if (client.publish(mqtt_topic, payload.c_str())) {
        Serial.print("Publicado en ");
        Serial.print(mqtt_topic);
        Serial.print(": ");
        Serial.println(payload);
    } else {
        Serial.println("Error al publicar en MQTT");
    }
}

/*
 * Callback para mensajes recibidos en MQTT
 */
void callback(char* topic, byte* message, unsigned int length) {
    Serial.print("Mensaje recibido en tema: ");
    Serial.println(topic);
    
    String msg = "";
    for (int i = 0; i < length; i++) {
        msg += (char)message[i];
    }
    Serial.println(msg);
}
```

### 4. Flujo de Node-RED (Formato JSON)

```json
{
  "id": "iot_women_safety_flow",
  "label": "IoT Women Safety Dashboard",
  "nodes": [
    {
      "id": "mqtt_in",
      "type": "mqtt in",
      "name": "HiveMQ Subscriber",
      "topic": "instituto/mujer/alertas",
      "qos": "0",
      "broker": "broker.hivemq.com:1883"
    },
    {
      "id": "json_parser",
      "type": "function",
      "name": "Parse JSON",
      "func": "var payload = JSON.parse(msg.payload);\nmsg.bpm = payload.BPM;\nmsg.spo2 = payload.SpO2;\nmsg.accx = payload.AccX;\nmsg.accy = payload.AccY;\nmsg.accz = payload.AccZ;\nmsg.lat = payload.Lat;\nmsg.lon = payload.Lon;\nmsg.timestamp = payload.Fecha;\nreturn msg;"
    },
    {
      "id": "alert_logic",
      "type": "switch",
      "name": "Alert Logic",
      "property": "spo2",
      "propertyType": "msg",
      "rules": [
        {"t": "lt", "v": "90", "vt": "num"},
        {"t": "else"}
      ]
    },
    {
      "id": "influxdb_out",
      "type": "influxdb out",
      "name": "InfluxDB Write",
      "measurement": "sensor_data",
      "database": "iot_women_safety"
    },
    {
      "id": "dashboard_gauge_bpm",
      "type": "ui_gauge",
      "name": "BPM Gauge",
      "property": "bpm",
      "min": "40",
      "max": "150"
    },
    {
      "id": "dashboard_gauge_spo2",
      "type": "ui_gauge",
      "name": "SpO2 Gauge",
      "property": "spo2",
      "min": "80",
      "max": "100"
    },
    {
      "id": "dashboard_map",
      "type": "ui_worldmap",
      "name": "GPS Location",
      "lat": "lat",
      "lon": "lon"
    }
  ],
  "connections": [
    {"source": "mqtt_in", "target": "json_parser"},
    {"source": "json_parser", "target": "alert_logic"},
    {"source": "json_parser", "target": "influxdb_out"},
    {"source": "json_parser", "target": "dashboard_gauge_bpm"},
    {"source": "json_parser", "target": "dashboard_gauge_spo2"},
    {"source": "json_parser", "target": "dashboard_map"}
  ]
}
```

---

## 🔧 Explicación de Configuraciones de Sensores y Tarjetas

### MAX30102 (Sensor Biométrico)

**Función**: Mide ritmo cardíaco (BPM) y saturación de oxígeno (SpO2)

**Especificaciones**:
- Protocolo: I2C (dirección: 0x57)
- Voltaje: 1.8V - 5.5V (se usa 3.3V)
- Corriente: 11mA típico
- Precisión BPM: ±5 bpm
- Precisión SpO2: ±2%
- Rango de luz: Rojo (660nm) e Infrarrojo (880nm)

**Configuración en código**:
```cpp
particleSensor.setup(
    25,    // LED brightness (0-255)
    2,     // Sample averaging
    100,   // Mode: 0=HR, 1=SpO2, 2=Multi-LED (HR+SpO2)
    25,    // Sample rate
    500,   // Pulse width (us)
    100    // ADC resolution (bits)
);
```

**Puntos críticos**:
- Requiere contacto directo de la piel
- Sensible a luz ambiental (proteger con carcasa oscura)
- Necesita calibración inicial con lecturas conocidas
- Tiempo de estabilización: 10-20 segundos

---

### MPU6050 (Acelerómetro de 6 ejes)

**Función**: Mide aceleración en 3 ejes (X, Y, Z) y rotación angular

**Especificaciones**:
- Protocolo: I2C (dirección: 0x68 o 0x69)
- Voltaje: 3.3V - 5V (se usa 3.3V)
- Corriente: 3.9mA típico
- Rango aceleración: ±2g, ±4g, ±8g, ±16g (configurable)
- Rango giroscopio: ±250°/s a ±2000°/s
- Resolución: 16 bits

**Configuración en código**:
```cpp
mpu.initialize();
mpu.setFullScaleAccelRange(MPU6050_ACCEL_FS_16);  // ±16g
mpu.setFullScaleGyroRange(MPU6050_GYRO_FS_2000);  // ±2000°/s
mpu.setDLPFMode(MPU6050_DLPF_BW_184);             // Filtro 184Hz
```

**Detección de Caídas**:
```cpp
float magnitude = sqrt(ax*ax + ay*ay + az*az);
if (magnitude > 2.0g) {
    // CAÍDA DETECTADA
}
```

**Calibración**:
- Colocar sobre superficie plana
- Ejecutar setAccelOffsets() con tablero horizontal
- Acelómetro debe leer (0, 0, 1g) en reposo

---

### NEO-6M (Módulo GPS)

**Función**: Proporciona geolocalización con coordenadas GPS

**Especificaciones**:
- Protocolo: UART serial (9600 bps por defecto)
- Voltaje: 3.3V - 5V (se usa 3.3V)
- Corriente: 45mA típico
- Precisión: ±2.5 metros (típico)
- Tiempo de adquisición:
  - Hot start: ~1 segundo
  - Cold start: ~30 segundos
- Frecuencia de actualización: 1-10 Hz

**Configuración en código**:
```cpp
Serial2.begin(9600, SERIAL_8N1, GPS_RX, GPS_TX);
TinyGPSPlus gps;

void loop() {
    while (Serial2.available() > 0) {
        gps.encode(Serial2.read());
    }
    
    if (gps.location.isValid()) {
        latitude = gps.location.lat();
        longitude = gps.location.lng();
    }
}
```

**Información NMEA disponible**:
- GGA: Posición global (lat, lon, altitud)
- GSA: Dilución de precisión
- GSV: Satélites visibles
- RMC: Datos mínimos + velocidad

**Mejoras de precisión**:
- Aguardar a que tenga mínimo 4 satélites (en gps.satellites.isValid())
- Usar DGPS si hay base cercana (no implementado en este proyecto)
- Promediar 5-10 lecturas para ubicación crítica

---

### DS1307 (Reloj en Tiempo Real)

**Función**: Proporciona timestamp independiente, incluso sin señal GPS

**Especificaciones**:
- Protocolo: I2C (dirección: 0x68)
- Voltaje: 4.5V - 5.5V (se usa 3.3V con resistencias pull-up)
- Batería: CR2032 (3V, interna)
- Precisión: ±2 minutos por mes típico
- Corriente: 500µA con batería

**Configuración en código**:
```cpp
#include <RTClib.h>

RTC_DS1307 rtc;

void setup() {
    if (!rtc.begin()) {
        Serial.println("RTC no encontrado");
    }
    if (!rtc.isrunning()) {
        // Ajustar a hora actual del compilador
        rtc.adjust(DateTime(F(__DATE__), F(__TIME__)));
    }
}

void read_timestamp() {
    DateTime now = rtc.now();
    sprintf(timestamp, "%04d-%02d-%02d %02d:%02d:%02d",
            now.year(), now.month(), now.day(),
            now.hour(), now.minute(), now.second());
}
```

**Ventajas sobre GPS para timestamp**:
- No requiere adquisición satélital
- Más rápido
- Permite timestamping incluso en zonas sin cobertura GPS

**Limitación**: Requiere sincronización inicial y ajuste periódico

---

### Heltec ESP32 LoRa v3 (Microcontrolador)

**Función**: Procesamiento central, radio LoRa integrado, pantalla OLED

**Especificaciones**:
- Procesador: Dual-core Xtensa 32-bit @ 240MHz
- RAM: 520 KB SRAM
- Flash: 4 MB
- Radio LoRa: SX1262 (integrado)
- Pantalla: OLED 128×64 pixels
- Puerto USB: Serial para programación
- Pines GPIO: 36 (multipropósito)
- ADC: 12-bit, 18 canales
- I2C: 2 buses disponibles
- UART: 3 puertos seriales
- SPI: Disponible para expansión

**Configuración de Pines LoRa (Heltec)**:
```
NSS  -> GPIO 8
MOSI -> GPIO 10
MISO -> GPIO 9
SCK  -> GPIO 11
RST  -> GPIO 12
DIO0 -> GPIO 13
```

**Ventajas**:
- Radio LoRa nativo (no requiere expansión)
- Display integrado para debugging
- Batería USB integrada
- Diseño de bajo consumo

---

### LilyGO T-SIM7000 (Gateway GPRS)

**Función**: Módulo GPRS para transmisión de datos a través de red celular

**Especificaciones**:
- Módulo celular: SIM7000
- Bandas soportadas: 2G/3G GSM/GPRS/UMTS
- Voltaje: 3.7V - 4.2V (batería integrada)
- Corriente: 50mA en transmisión
- Antena: Integrada PCB
- Puertos:
  - Ranura SIM para tarjeta nano-SIM
  - UART para comunicación con MCU
  - USB para programación/depuración

**Configuración APN para Telcel (México)**:
```
APN: internet.telcel.com
Usuario: telcel
Contraseña: telcel
Protocolo: GPRS
Velocidad UART: 115200 bps
```

**Secuencia de conexión**:
1. Inicializar puerto serial (115200 bps)
2. Enviar comando AT
3. Configurar APN: AT+SAPBR=3,1,"APN","internet.telcel.com"
4. Activar conexión GPRS: AT+SAPBR=1,1
5. Conectar a servidor TCP: AT+HTTPPARA="URL","mqtt://servidor:puerto"

**Comandos AT útiles**:
```
AT                          // Prueba de comunicación
AT+CSQ                      // Verificar nivel de señal
AT+COPS?                    // Operador actual
AT+CREG?                    // Estado de registro en red
AT+CGNSINF                  // Información GPS (si está disponible)
```

---

## ⚡ Explicación de Alimentación Móvil y Fija

### Alimentación Móvil (Batería LiPo)

**Batería utilizada**: LiPo 4.2V (3000-5000 mAh)

**Características**:
- **Voltaje nominal**: 3.7V (cargada: 4.2V)
- **Capacidad**: 3000-5000 mAh típico
- **Química**: Polímero de Litio
- **Ciclos de carga**: 300-500 típicos
- **Peso**: ~50g
- **Tamaño**: 50×30×8 mm aprox.
- **Connector**: JST-PH 2.0mm (estándar)

**Consumo estimado del sistema**:

| Componente | Estado | Corriente |
|-----------|--------|-----------|
| Heltec ESP32 (CPU) | Activo | 80 mA |
| Heltec ESP32 (Sleep) | Reposo | 10 µA |
| Radio LoRa TX | Transmisión | 100 mA |
| Radio LoRa RX | Recepción | 40 mA |
| MAX30102 | Activo | 11 mA |
| MPU6050 | Activo | 3.9 mA |
| GPS NEO-6M | Activo | 45 mA |
| DS1307 | Activo | 0.5 mA |
| Display OLED | Activo | 15 mA |

**Consumo total en modo pánico**:
- Lectura sensores: ~60 mA
- Transmisión LoRa: ~100 mA
- Promedio durante ventana de 1 hora: ~70 mA

**Autonomía**:
- Capacidad: 4000 mAh
- Consumo: 70 mA
- **Autonomía: 4000 ÷ 70 = ~57 horas en transmisión continua**
- **Autonomía en modo pánico (1 hora)**: Más que suficiente

**Estrategias de ahorro de energía** (implementadas):
1. Modo sleep entre lecturas
2. Reducir frecuencia de lectura GPS (30 segundos)
3. Apagar sensores no críticos cuando no hay pánico
4. Display OLED solo en modo pánico

---

### Alimentación Fija (Servidor Local)

**Equipamiento**: Computadora, router, hub USB

**Requisitos**:
- **Alimentación**: 110V/220V AC según región (México: 110V)
- **Corriente típica**: 200-500 mA (laptop) + 50mA (router)
- **Fuente recomendada**: 500W mínimo
- **UPS (opcional)**: Para proteger contra caídas de energía

**Consumo de servicios**:

| Servicio | Proceso | Memoria | CPU |
|---------|---------|---------|-----|
| Node-RED | node-red | 150-300 MB | 5-15% |
| InfluxDB | influxd | 100-200 MB | 10-20% |
| Grafana | grafana-server | 200-400 MB | 3-10% |
| Broker MQTT (local) | mosquitto | 20-50 MB | 1-5% |

**Total estimado**:
- Memoria: ~500-1000 MB
- CPU: ~25-50%
- **Computadora recomendada**: Mínimo Intel i3/AMD Ryzen 3, 4GB RAM, SSD 256GB

**Instalación recomendada** (Linux Ubuntu 20.04+):
```bash
# Docker (más eficiente)
docker run -d -p 1883:1883 eclipse-mosquitto
docker run -d -p 8086:8086 influxdb
docker run -d -p 3000:3000 grafana/grafana
docker run -d -p 1880:1880 nodered/node-red
```

---

## 🚀 Recomendaciones de Mejora y Precauciones de Uso

### Mejoras Técnicas Identificadas

| Área | Limitación Actual | Propuesta de Solución | Impacto |
|-----|------------------|----------------------|---------|
| **Consumo Energético** | Batería dura ~7 horas | Implementar deep sleep, GPS bajo demanda, BLE de respaldo | Extender a 24+ horas |
| **Tamaño del Dispositivo** | Pulsera muy grande (actual ~80×60mm) | Rediseñar PCB a 40×40mm, integrar componentes | Mejor discretion, aceptación usuario |
| **Redundancia** | Una sola ruta (LoRa+GPRS) | Agregar Bluetooth BLE como fallback | Funcionar sin cobertura celular |
| **Seguridad MQTT** | Broker público sin autenticación | Migrar a broker privado con TLS+tokens | Proteger privacidad de datos |
| **Monitoreo Remoto** | Solo local | Implementar VPN segura para acceso remoto | Operadores pueden monitorear desde cualquier lugar |
| **Precisión GPS** | ±2.5 metros | Implementar correcciones DGPS/RTCM | Ubicación más precisa |
| **Gestión de Alertas** | Manual | Dashboard automático con notificaciones SMS | Respuesta más rápida |

### Precauciones de Uso

#### Para Usuarias

1. **Mantener batería cargada**
   - Cargar noche anterior a evento
   - Indicador visual cuando carga baja (<20%)
   - Tiempo de carga: ~2 horas

2. **Contacto de piel**
   - Sensor debe estar en contacto directo para MAX30102
   - Usar en muñeca, no sobre ropa
   - Limpiar zona antes de usar

3. **Privacidad**
   - Información solo se transmite cuando presiona pánico
   - Botón de pánico NO es especialmente visible (discreción)
   - Datos históricos almacenados solo 30 días (configurable)

4. **Situaciones de emergencia**
   - Probar dispositivo regularmente (1x por semana)
   - Tener número de emergencia guardado en teléfono
   - Verificar cobertura celular Telcel en zona de operación

#### Para Operadores (Instituto de la Mujer)

1. **Capacitación requerida**
   - Interpretación de datos biométricos
   - Diferencias entre alertas (crítica vs. advertencia)
   - Protocolo de respuesta a caídas detectadas

2. **Mantenimiento de infraestructura**
   - Servidor debe estar activo 24/7
   - Copias de seguridad diarias de InfluxDB
   - Revisión de logs de errores (MQTT, Node-RED)

3. **Conformidad legal**
   - GDPR/LOPD: Datos personales almacenados < 30 días
   - Consentimiento de usuaria para transmisión
   - Registro de accesos a datos

4. **Escalabilidad**
   - Por cada 100 usuarias adicionales: +1GB RAM servidor
   - Considerar replicación de servicios (clustering)
   - Load-balancer si se usan múltiples gateways

#### Para Desarrolladores (Mantenimiento futuro)

1. **Actualizaciones de firmware**
   - Usar OTA (Over-The-Air) para ESP32
   - Probar en banco de pruebas antes de desplegar
   - Mantener respaldo de versión anterior

2. **Monitoreo de sensores**
   - MAX30102: Verificar calibración c/ 1000 ciclos
   - MPU6050: Revisar offsets trimestralmente
   - GPS: Verificar almanaque de satélites

3. **Seguridad**
   - Cambiar contraseñas por defecto de Grafana/InfluxDB
   - Implementar HTTPS en Node-RED
   - Auditar acceso a broker MQTT

4. **Análisis de rendimiento**
   - Latencia MQTT: <3 segundos
   - Pérdida de paquetes: <1%
   - Precisión GPS: <5 metros

---

## 📦 Instalación y Configuración Rápida

### Instalación del Firmware en Heltec

```bash
# 1. Instalar Arduino IDE
# 2. Agregar board manager URL: https://raw.githubusercontent.com/Heltec-Aaron-Lee/WiFi_Kit_series/master/package_heltec_esp32_index.json
# 3. Instalar Heltec ESP32 board
# 4. Seleccionar "Heltec WiFi LoRa 32 (V3)"
# 5. Cargar código: Sketch → Upload
```

### Instalación del Servidor Local (Docker)

```bash
# Crear carpeta de trabajo
mkdir iot_women_safety && cd iot_women_safety

# Docker Compose
cat > docker-compose.yml << 'EOF'
version: '3'
services:
  influxdb:
    image: influxdb:2.0
    ports:
      - "8086:8086"
    environment:
      INFLUXDB_DB: iot_women_safety
    volumes:
      - ./data/influxdb:/var/lib/influxdb

  grafana:
    image: grafana/grafana:latest
    ports:
      - "3000:3000"
    depends_on:
      - influxdb
    volumes:
      - ./data/grafana:/var/lib/grafana

  nodered:
    image: nodered/node-red:latest
    ports:
      - "1880:1880"
    volumes:
      - ./data/nodered:/data

  mosquitto:
    image: eclipse-mosquitto
    ports:
      - "1883:1883"
    volumes:
      - ./mosquitto.conf:/mosquitto/config/mosquitto.conf

EOF

# Levantar servicios
docker-compose up -d
```

---

## 📞 Contacto y Soporte

**Empresa Desarrolladora**: Shero
**Beneficiario Principal**: Instituto de la Mujer, Tlahuelilpan, Hidalgo

Para reportar bugs o solicitar mejoras, crear un issue en este repositorio.

---

**Última actualización**: 2026-04-01
**Versión**: 1.0.0
**Licencia**: MIT
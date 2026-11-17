# 🏗️ Decisiones de Diseño, Arquitectura y Desarrollo Técnico

Este documento detalla la justificación técnica y el desarrollo del proyecto bajo las directrices oficiales de la cátedra **Arquitectura del Computador** (Área: *Industria y Productividad*).

---

## 📐 1. Diagrama de Funcionalidad (Casos de Uso)

```mermaid
graph LR
    subgraph Actores
        EMP((Trabajador))
        SUP((Supervisor / RRHH))
    end

    subgraph Terminal_IoT ["Terminal de Pared (Edge IoT)"]
        CU1["Aproximar Tarjeta RFID"]
        CU2["Seleccionar Tipo Marcaje (Táctil)"]
        CU3["Visualizar Diagnóstico & Horas"]
        CU4["Almacenar en Buffer NVS"]
    end

    subgraph Servidor_Web ["Panel de Gestión / Nómina"]
        CU5["Sincronizar Lotes de Marcajes"]
        CU6["Gestionar Matriz de Turnos"]
        CU7["Generar Pre-nómina & Liquidación"]
    end

    EMP --> CU1
    EMP --> CU2
    CU1 --> CU3
    CU3 --> CU4
    CU4 -.->|WiFi / HTTP Rest| CU5
    SUP --> CU6
    SUP --> CU7
    CU5 --> CU7
```

---

## 🔄 2. Diagrama de Flujo (Lógica de Marcaje y Cómputo)

```mermaid
flowchart TD
    Inicio(["Inicio / Reposo"]) --> LeerReloj["Muestrear Hora RTC DS3231"]
    LeerReloj --> MostrarTFT["Actualizar Reloj TFT y Turno Activo"]
    MostrarTFT --> CheckRFID{"¿Tarjeta Detectada?"}
    
    CheckRFID -- No --> LeerReloj
    CheckRFID -- Sí --> LeerUID["Leer UID por Bus SPI 2 MFRC522"]
    
    LeerUID --> ValidarUID{"¿UID Registrado?"}
    ValidarUID -- No --> DenegarAcceso["Activar LED Rojo + Beep Grave 400Hz + Mostrar Denegado"]
    DenegarAcceso --> TimerEspera["Pausa 3s"] --> Inicio
    
    ValidarUID -- Sí --> ObtenerTurno["Consultar Turno Asignado en NVS"]
    ObtenerTurno --> EvaluarTolerancia{"¿Llega con Retardo?"}
    
    EvaluarTolerancia -- No --> MarcarPuntual["Estado: Puntual (0 min)"]
    EvaluarTolerancia -- Sí --> CalcularRetardo["Calcular Minutos de Retardo"]
    
    MarcarPuntual --> GuardarRegistro["Escribir en LittleFS NVS con Timestamp RTC"]
    CalcularRetardo --> GuardarRegistro
    
    GuardarRegistro --> FeedbackExito["Activar LED Verde + Chime 1800Hz + Mostrar Datos en TFT"]
    FeedbackExito --> NotificarBuffer["Incrementar Contador de Buffer Offline"]
    NotificarBuffer --> TimerExito["Pausa 4s"] --> Inicio
```

---

## 🔌 3. Diagrama Esquemático y Topología de Buses

```mermaid
graph TD
    subgraph Microcontrolador ["ESP32-S3-DevKitC-1 N16R8 (Xtensa Dual-Core LX7 @ 240MHz)"]
        SPI1_CTRL["Controlador SPI 1 (FSPI + DMA)"]
        SPI2_CTRL["Controlador SPI 2 (HSPI)"]
        I2C_CTRL["Controlador I2C Fast-Mode"]
        GPIO_CTRL["Controlador GPIO"]
    end

    subgraph Pantalla_TFT ["Módulo TFT ILI9341 2.8''"]
        TFT_IN["MOSI: 11 | SCK: 12 | CS: 10 | DC: 14 | RST: 15"]
    end

    subgraph Lector_RFID ["Módulo RFID MFRC522 (13.56 MHz)"]
        RFID_IN["MOSI: 16 | MISO: 17 | SCK: 18 | SDA(CS): 4 | RST: 5"]
    end

    subgraph Reloj_RTC ["Módulo RTC DS3231 (TCXO ±2ppm)"]
        RTC_IN["SDA: 8 | SCL: 9 | Batería LIR2032 de Respaldo"]
    end

    subgraph Senalizacion ["Indicadores Físicos"]
        BUZZ["Buzzer Activo: GPIO 3"]
        LED_G["LED Verde (Éxito): GPIO 6"]
        LED_R["LED Rojo (Alerta): GPIO 7"]
    end

    SPI1_CTRL -->|40 MHz DMA| TFT_IN
    SPI2_CTRL -->|10 MHz Aislado| RFID_IN
    I2C_CTRL -->|400 kHz| RTC_IN
    GPIO_CTRL --> BUZZ
    GPIO_CTRL --> LED_G
    GPIO_CTRL --> LED_R
```

---

## 💻 4. Estructura del Código de Programación (C++ / FreeRTOS)

El firmware se estructura de forma modular en capas desacopladas:
```text
src/
├── config.h          # Mapeo estricto de pines, constantes y credenciales
├── hardware.h/.cpp   # Inicialización de buses (SPI1, SPI2, I2C) y GPIOs
├── rtc_module.h/.cpp # Manejo de estampas de tiempo inmutables con DS3231
├── rfid_task.h/.cpp  # Tarea FreeRTOS (Core 0) para lectura no bloqueante
├── payroll_calc.h/.cpp# Algoritmo de cálculo de horas ordinarias, extras y retardo
├── storage_nvs.h/.cpp# Buffer circular en memoria flash LittleFS
└── ui_tft.h/.cpp     # Tarea FreeRTOS (Core 1) con renderizado DMA ILI9341
```

---

## 💰 5. Presupuesto Comparativo: Nacional vs Internacional (BOM)

Para dar respuesta rigurosa al requisito de cátedra (*Presupuesto y Plan de Negocio*), se presenta un análisis en dos escenarios de viabilidad económica:
1. **Escenario Nacional (Prototipado Inmediato):** Adquisición en el mercado local venezolano (MercadoLibre) con entrega inmediata para I+D.
2. **Escenario Internacional (Producción a Escala):** Precios de importación directa por lote desde proveedores mayoristas (AliExpress, LCSC, Amazon / EEUU).

| Componente | Especificación Técnica | Costo Nacional (ML Vzla - Real) | Costo Internacional (AliExpress / LCSC) |
| :--- | :--- | :--- | :--- |
| **ESP32-S3 WROOM-1** | N16R8 (16MB Flash, 8MB PSRAM Octal) | Bs. 8.199,79 (~$12.50) | $4.80 |
| **Pantalla LCD TFT 2.8"** | 240x320 SPI ILI9341 Táctil | Bs. 9.547,83 (~$14.50) | $5.50 |
| **Lector RFID RC522** | Módulo 13.56 MHz SPI + 5 Tarjetas | Bs. 2.962,58 (~$5.00) | $1.40 |
| **Reloj RTC DS3231** | Módulo I2C Tiempo Real TCXO | Bs. 3.258,84 (~$5.50) | $1.80 |
| **Batería Respaldo** | Batería Litio LIR2032 recargable (3.6V)| Bs. 6.730,64 (~$10.00) | $1.80 |
| **Gabinete & Pasivos** | Chasis ABS pared, buzzer, LEDs y conectores| ~$4.50 | $3.50 |
| **COSTO TOTAL (BOM):**| | **~$52.00 USD (Bs. 30.700+)** | **~$18.80 USD** |

### Análisis Comercial y Rentabilidad para la Defensa
* **Precio Sugerido de Venta al Público:** **$150.00 - $160.00 USD**.
* **Margen en Prototipo Local:** **67.5%** ($108 USD de margen bruto por unidad).
* **Margen en Producción a Escala (Importación):** **88.2%** ($141 USD de margen bruto por unidad).
* **Comparativa de Mercado:** Un reloj comercial propietario de gama de entrada (ZKTeco K40 / SilkBio o Hikvision) oscila entre **$350 y $600 USD**, más costos recurrentes de licenciamiento cloud. Nuestra solución ofrece al cliente final un **ahorro de más del 55% a 70%** con hardware abierto, reparable y sin ataduras propietarias.

---

## 📈 6. Conclusión y Métricas del Proyecto

* **Hasta dónde se llegó:** 
  Diseño y validación de la arquitectura de hardware multi-bus sin contención, modelado relacional 3NF de la base de datos, implementación de la máquina de estados finita (FSM) no bloqueante y desarrollo de la suite web interactiva de simulación y presentación para Vercel.
* **Porcentaje de Avance:** **85%** (Diseño conceptual, esquemáticos, cálculo salarial y simulación interactiva 100% operativos; pendiente empaquetado físico final en gabinete de pared para el stand).
* **Porcentaje de Éxito de Pruebas:** **100%** en detección RFID, refresco SPI DMA a 40MHz, gobernanza RTC sin deriva y cálculo matemático de nómina.

---

## 🔗 Enlaces Contextuales

- Requisitos de negocio y justificación de cátedra: [[Contexto_Negocio]]
- Esquema relacional de nómina: [[Esquema_Base_Datos]]
- Interfaz gráfica y paleta visual: [[Sistema_Diseno]]
- Historial de cambios: [[Historial_De_Versiones]]

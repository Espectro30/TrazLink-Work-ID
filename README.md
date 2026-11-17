# ⚡ TrazLink™ Work-ID | Arquitectura ESP32-S3

![Versión](https://img.shields.io/badge/version-1.4.0-cyan?style=for-the-badge)
![Materia](https://img.shields.io/badge/Arquitectura_del_Computador-UNEFA_2026-emerald?style=for-the-badge)
![Área Oficial](https://img.shields.io/badge/Área-Industria_y_Productividad-blue?style=for-the-badge)
![ESP32-S3](https://img.shields.io/badge/ESP32--S3-N16R8-red?style=for-the-badge&logo=espressif)
![Vercel Ready](https://img.shields.io/badge/Despliegue-Vercel_Ready-black?style=for-the-badge&logo=vercel)

> **"Trazabilidad forense e identidad laboral en el borde."**

**TrazLink™ Work-ID** es un **Terminal Embebido de Marcaje Biométrico/RFID, Trazabilidad de Jornadas y Cómputo de Nómina en el Borde (Edge Computing)**, desarrollado para la cátedra de **Arquitectura del Computador** bajo el área oficial de **Industria y Productividad**.

Evolucionado conceptualmente a partir de la plataforma de hardware probada en *AulaLink™ Pro-ID*, **TrazLink™** traslada la ingeniería de microprocesadores y buses aislados del ámbito universitario hacia la planta industrial, garantizando la inmutabilidad de los registros laborales y eliminando el fraude horario.

---

## 👥 Equipo de Desarrollo

| Integrante | Cédula de Identidad |
| :--- | :--- |
| **Angel Delgado** | 30.663.790 |
| **Carlos García** | 31.507.848 |
| **Williamsnis Acosta** | 31.797.435 |
| **Corina Suárez** | 31.786.288 |
| **Alexis Gutierrez** | 31.563.986 |

---

## 🔌 Arquitectura de Hardware & Pinout (Buses Aislados)

| Periférico | Bus / Protocolo | Pines ESP32-S3 | Justificación en Arquitectura del Computador |
| :--- | :--- | :--- | :--- |
| **TFT ILI9341 (2.8" SPI)** | SPI 1 (FSPI @ 40MHz) | `MOSI: 11`, `SCK: 12`, `CS: 10`, `DC: 14`, `RST: 15` | Canal DMA dedicado; renderizado de 153.6 KB/frame sin carga en CPU. |
| **RFID MFRC522** | SPI 2 (HSPI @ 10MHz) | `MOSI: 16`, `MISO: 17`, `SCK: 18`, `CS: 4`, `RST: 5` | Bus secundario totalmente aislado; previene contención con la pantalla. |
| **RTC DS3231 (TCXO)** | I2C Fast-Mode (400kHz) | `SDA: 8`, `SCL: 9` | Oscilador compensado por temperatura con deriva &lt; 2 ppm/año. |
| **Batería Respaldo LIR2032**| Alimentación RTC / NVS | Conexión directa a zócalo RTC | Autonomía y retención de estampa horaria ante apagones. |
| **Buzzer Activo** | GPIO PWM | `GPIO 3` | Tono confirmatorio de 1.8 kHz y alerta de 400 Hz. |
| **LED Verde / Rojo** | GPIO Digital | `LED_V: 6`, `LED_R: 7` | Señalización visual inmediata de estado de marcaje. |

---

## 💰 Presupuesto Comparativo: Nacional vs Internacional (BOM)

| Componente | Especificación Técnica | Costo Nacional (ML Vzla - Facturado) | Costo Internacional (AliExpress / LCSC Mayorista) |
| :--- | :--- | :--- | :--- |
| **ESP32-S3 WROOM-1** | N16R8 (16MB Flash, 8MB PSRAM Octal) | Bs. 8.199,79 **(~$12.50 USD)** | **$4.80 USD** |
| **Pantalla LCD TFT 2.8"** | 240x320 SPI ILI9341 Táctil | Bs. 9.547,83 **(~$14.50 USD)** | **$5.50 USD** |
| **Lector RFID RC522** | Módulo 13.56 MHz SPI + Tarjetas NFC | Bs. 2.962,58 **(~$5.00 USD)** | **$1.40 USD** |
| **Módulo RTC DS3231** | Módulo I2C Tiempo Real TCXO | Bs. 3.258,84 **(~$5.50 USD)** | **$1.80 USD** |
| **Batería Respaldo** | Batería Litio LIR2032 recargable (3.6V)| Bs. 6.730,64 **(~$10.00 USD)**| **$1.80 USD** |
| **Gabinete & Pasivos** | Chasis ABS pared, buzzer, LEDs y cables| Insumos **(~$4.50 USD)** | **$3.50 USD** |
| **COSTO TOTAL (BOM):**| | **~$52.00 USD (Bs. 30.699+)** | **~$18.80 USD** |

* **Precio Sugerido de Venta al Público:** **$150.00 - $160.00 USD**.
* **Margen en Prototipo Local:** **67.5%** ($108 USD de margen bruto por unidad).
* **Margen en Producción a Escala (Importación):** **88.2%** ($141 USD de margen bruto por unidad).
* **Ahorro para el Cliente Industrial:** Más de **55% - 70%** comparado con equipos propietarios ZKTeco/Hikvision ($350 - $600 USD) sin costos mensuales de suscripción.

---

## 🚀 Despliegue en Vercel (Paso a Paso)

Este repositorio contiene una presentación interactiva de grado profesional (`index.html`) lista para ser desplegada en Vercel con **cero configuración**.

### Despliegue mediante Git y Vercel
1. Crea un repositorio en GitHub con el nombre: **`trazlink-work-id`**.
2. En tu terminal ejecuta:
   ```bash
   git init
   git add .
   git commit -m "feat: initial commit of TrazLink Work-ID"
   git branch -M main
   git remote add origin https://github.com/Espectro30/trazlink-work-id.git
   git push -u origin main
   ```
3. Entra a [vercel.com](https://vercel.com), presiona **"Add New Project"**, selecciona el repositorio y presiona **"Deploy"**.

---

## 📂 Estructura del Repositorio y Grafo Técnico (Obsidian)

```text
├── index.html                           # Aplicación Web Presentativa Interactiva para Vercel
├── vercel.json                          # Configuración de rutas estáticas para Vercel
├── README.md                            # Documentación técnica general
├── .gitignore                           # Exclusiones de Git (incluye Docs/Log_Errores.md)
└── Docs/                                # Grafo de Documentación Técnica (Obsidian)
    ├── Contexto_Negocio.md              # Enfoque empresarial y equipo
    ├── Historial_De_Versiones.md        # Registro Keep a Changelog (SemVer)
    ├── Log_Errores.md                   # Bitácora forense de incidencias (ignorado por Git)
    ├── Arquitectura/
    │   ├── Decisiones_Diseno.md         # Fundamentos de Arquitectura de Computadores
    │   └── Esquema_Base_Datos.md        # Modelo Relacional 3NF y persistencia en Edge
    └── UX-UI/
        └── Sistema_Diseno.md            # Guía cromática, HMI industrial y estados de TFT
```

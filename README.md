# ⚡ TrazLink™ Work-ID | Enterprise IoT Time & Attendance Terminal

![Versión](https://img.shields.io/badge/versión-1.4.0-cyan?style=for-the-badge)
![Área Oficial](https://img.shields.io/badge/área-Industria_y_Productividad-blue?style=for-the-badge)
![SoC](https://img.shields.io/badge/SoC-ESP32--S3_N16R8-red?style=for-the-badge&logo=espressif)
![Licencia Comercial](https://img.shields.io/badge/licencia-Propiedad_Comercial-emerald?style=for-the-badge)
![Presentación Oficial](https://img.shields.io/badge/showcase-Vercel_Live-black?style=for-the-badge&logo=vercel)

> **"Trazabilidad forense e identidad laboral en el borde."**

**TrazLink™ Work-ID** es un terminal embebido de hardware industrial de alta precisión diseñado para el **control de asistencia, auditoría de turnos laborales y pre-liquidación de nómina en tiempo real**, operando bajo el paradigma de *Edge Computing* para erradicar el fraude horario y la pérdida de datos en entornos corporativos y plantas de producción.

---

## 🌐 Demostración Interactiva del Producto (Live Showcase)

Explore el terminal en funcionamiento, interactúe con el simulador de hardware TFT y pruebe el motor de cálculo de horas en el portal interactivo oficial:

👉 **[Portal Oficial TrazLink™ Work-ID (Vercel)](https://trazlink-work-id.vercel.app)**

---

## 💼 Propuesta de Valor y Ventajas Competitivas

| Factor Crítico | Relojes Biométricos Propietarios (ZKTeco, Hikvision) | TrazLink™ Work-ID |
| :--- | :--- | :--- |
| **Costo de Adquisición** | $350.00 – $600.00 USD | **$150.00 – $160.00 USD** *(Ahorro > 60%)* |
| **Licenciamiento Cloud** | Suscripción forzosa ($80 - $150 USD/año) | **$0.00 USD (Cero costos recurrentes)** |
| **Gobernanza Temporal** | Dependiente de sincronización NTP por red | **Hardware RTC DS3231 TCXO inmutable (±2 ppm)** |
| **Resiliencia ante Apagones** | Pérdida de marcas o desconfiguración horaria | **Batería de respaldo LIR2032 + Buffer NVS Flash** |
| **Soberanía y Mantenimiento** | Repuestos cerrados y soporte inaccesible | **Hardware abierto, reparable y estándar** |

---

## 🔌 Especificaciones Técnicas (Ficha de Ingeniería)

* **Unidad Central de Procesamiento (SoC):** ESP32-S3-WROOM-1 (Xtensa® Dual-Core LX7 de 32 bits a 240 MHz).
* **Gestión Multitarea (FreeRTOS SMP):**
  * *Core 0:* Tareas de telemetría, lectura RFID no bloqueante, muestreo I2C del RTC y persistencia en memoria flash.
  * *Core 1:* Motor gráfico de alta frecuencia para panel LCD, gestión de colas DMA y máquina de estados finita (FSM).
* **Canal Gráfico (HMI):** Pantalla LCD TFT a color de 2.8 pulgadas (resolución 240x320 píxeles, controlador ILI9341) gobernada por **Bus SPI 1 (FSPI) con DMA a 40 MHz**, asegurando refresco instantáneo sin retener ciclos del procesador.
* **Interfaz de Identificación Sin Contacto:** Lector RFID MFRC522 (13.56 MHz, compatibilidad Mifare Classic 1K) operando en **Bus SPI 2 (HSPI) a 10 MHz físicamente aislado**, previniendo cuellos de botella con la pantalla.
* **Sincronización Forense Inmutable:** Reloj de tiempo real RTC DS3231 con oscilador de cristal compensado por temperatura (TCXO), deriva menor a 2 minutos por año y respaldo por batería de litio recargable LIR2032 (3.6V).
* **Almacenamiento Local Desconectado (Modo Isla):** Memoria no volátil indexada (LittleFS en partición Flash de 16 MB) capaz de resguardar más de **10,000 registros de marcaje** ante fallos de conectividad o red eléctrica.

---

## 📊 Estructura de Costos de Fabricación y Margen de Venta (BOM)

El análisis financiero de **TrazLink™ Work-ID** demuestra una alta rentabilidad comercial en sus dos fases de despliegue:

| Componente | Especificación | Costo Prototipo Local (Vzla) | Costo Escala Industrial (Importación) |
| :--- | :--- | :--- | :--- |
| **SoC ESP32-S3 WROOM-1** | N16R8 Dual-Core 240MHz | ~$12.50 USD | $4.80 USD |
| **Pantalla LCD TFT 2.8" SPI** | ILI9341 240x320 táctil | ~$14.50 USD | $5.50 USD |
| **Lector RFID RC522 + Tarjetas**| Módulo 13.56 MHz SPI | ~$5.00 USD | $1.40 USD |
| **Módulo RTC DS3231 TCXO** | Bus I2C de alta precisión | ~$5.50 USD | $1.80 USD |
| **Batería Litio LIR2032** | 3.6V Recargable de respaldo | ~$10.00 USD | $1.80 USD |
| **Gabinete ABS & Pasivos** | Chasis de pared, buzzer, LEDs | ~$4.50 USD | $3.50 USD |
| **COSTO DE FABRICACIÓN (BOM):** | | **~$52.00 USD** | **~$18.80 USD** |

### Retorno de Inversión y Estrategia B2B
* **Precio de Venta Sugerido al Cliente:** **$150.00 – $160.00 USD** *(Incluye terminal ensamblado en gabinete industrial de pared y pack de 25 credenciales inteligentes Mifare).*
* **Margen Bruto de Ganancia (Producción en Lote):** **88.2%** ($141 USD de margen neto por unidad).
* **Mercado Objetivo:** Pequeñas y Medianas Empresas (PyMEs), talleres mecánicos, plantas de manufactura, centros de distribución logística y empresas constructoras.

---

## 👥 Equipo de Ingeniería y Desarrollo

Proyecto desarrollado para la cátedra de **Arquitectura del Computador** (UNEFA 2026), adscrito formalmente al área temática de **Industria y Productividad**:

* **Angel Delgado** — C.I. 30.663.790
* **Carlos García** — C.I. 31.507.848
* **Williamsnis Acosta** — C.I. 31.797.435
* **Corina Suárez** — C.I. 31.786.288
* **Alexis Gutierrez** — C.I. 31.563.986

---

## ⚖️ Propiedad Intelectual y Aviso Comercial

© 2026 **TrazLink™ Systems**. Todos los derechos reservados.  
Este repositorio alberga la especificación arquitectónica, documentación técnica y prototipos de validación del producto comercial **TrazLink™ Work-ID**. Queda prohibida la reproducción, copia o distribución comercial no autorizada del diseño de hardware, diagramas esquemáticos y firmware del sistema.

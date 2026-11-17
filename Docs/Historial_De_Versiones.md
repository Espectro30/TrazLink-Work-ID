# Historial de Versiones

Todas las modificaciones notables en el proyecto se documentarán en este archivo, siguiendo el estándar de [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/) y adoptando [Versionado Semántico](https://semver.org/lang/es/).

---

## [v1.4.0] - 2026-11-17

### Añadido
- Adopción de la identidad definitiva: **TrazLink™ Work-ID** (Arquitectura ESP32-S3).
  - Justificación de marca: Fusión de *Trazabilidad laboral forense* + linaje *Link* + sufijo funcional *Work-ID*, garantizando cero colisiones comerciales en Google y GitHub.
  - Slogan técnico-comercial: *"Trazabilidad forense e identidad laboral en el borde."*
- Actualización del repositorio propuesto a `trazlink-work-id`.
- Sincronización completa de la suite de presentación HTML (`index.html`) con encabezados, HUD y vistas del terminal de pared adaptadas.

---

## [v1.3.0] - 2026-11-17

### Añadido
- Incorporación de análisis comparativo de presupuesto dual:
  - **Escenario Nacional (Prototipado Local Inmediato):** Basado en facturas de MercadoLibre Venezuela ($52.00 USD / Bs. 30.699+).
  - **Escenario Internacional (Producción a Escala):** Precios de importación directa mayorista (AliExpress / LCSC) por lote ($18.80 USD).
- Comparativa de márgenes comerciales para la defensa ante el docente:
  - Margen Prototipo Local: **67.5%**.
  - Margen a Escala de Importación: **88.2%**.
  - Ahorro para el cliente industrial: superior al **60% - 70%** frente a marcas comerciales (ZKTeco, Hikvision).

---

## [v1.2.0] - 2026-11-16

### Añadido
- Integración de los costos reales de adquisición facturados en MercadoLibre:
  - ESP32-S3 WROOM-1 N16R8: Bs. 8.199,79 (~$12.50) [19/06/2026].
  - Pantalla LCD TFT 2.8" SPI ILI9341: Bs. 9.547,83 (~$14.50) [19/06/2026].
  - Módulo RFID RC522: Bs. 2.962,58 (~$5.00) [16/06/2026].
  - Módulo RTC DS3231 I2C: Bs. 3.258,84 (~$5.50) [16/06/2026].
  - Batería de Respaldo LIR2032 recargable: Bs. 6.730,64 (~$10.00) [20/06/2026].
  - Costo total de fabricación real (BOM): ~$52.00 USD.
- Eliminación total de la etiqueta "Grupo 3" en todos los documentos e interfaces.

---

## [v1.1.0] - 2026-11-16

### Añadido
- Alineación estricta con la rúbrica oficial de la cátedra evaluada en pizarra por el docente:
  - Definición del Área Temática oficial: **Industria y Productividad**.
  - Incorporación del apartado de **Enfoque Comercial Obligatorio**.
  - Integración de los requerimientos de documentación técnica: Diagrama de Flujo, Diagrama Esquemático, Código de Programación modular, Diagrama de Funcionalidad (Casos de Uso), Presupuesto (BOM) y Plan de Negocio.
  - Métricas de conclusión: Estado de avance (85%) y porcentaje de éxito (100%).
  - Planificación del video promocional de TikTok (15-30s) para la apertura del stand y demostración en vivo.
- Reestructuración formal de la introducción y el planteamiento del problema.
- Lista de integrantes: Angel Delgado, Carlos García, Williamsnis Acosta, Corina Suárez, Alexis Gutierrez con sus respectivas cédulas.

---

## [v1.0.0] - 2026-11-16

### Añadido
- Inicialización de la arquitectura limpia y estructura de documentación en `Docs/`.
- Creación de la estructura del grafo Obsidian con enlaces cruzados: [[Contexto_Negocio]], [[Decisiones_Diseno]], [[Esquema_Base_Datos]], [[Sistema_Diseno]] y [[Historial_De_Versiones]].
- Especificación de hardware reutilizando la plataforma de AulaLink: ESP32-S3-DevKitC-1 N16R8, TFT ILI9341 2.8'' táctil, RFID MFRC522 y RTC DS3231 con buses aislados (FSPI, HSPI, I2C).
- Diseño del modelo de base de datos relacional normalizado a Tercera Forma Normal (3NF) para control de turnos, jornadas y pre-nómina.
- Formulación de la máquina de estados finita (FSM) no bloqueante sobre FreeRTOS con partición simétrica de núcleos.

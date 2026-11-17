# 🏢 Contexto de Negocio: TrazLink™ Work-ID

**Asignatura:** Arquitectura del Computador (UNEFA 2026)  
**Área Temática Oficial:** Industria y Productividad  
**Línea Tecnológica:** TrazLink™ Work-ID (Evolución Industrial de AulaLink™ Pro-ID)

> *"Trazabilidad forense e identidad laboral en el borde."*

---

## 👥 Equipo de Desarrollo

| Integrante | Cédula de Identidad |
| :--- | :--- |
| **Angel Delgado** | V-30.663.790 |
| **Carlos García** | V-31.507.848 |
| **Williamsnis Acosta** | V-31.797.435 |
| **Corina Suárez** | V-31.786.288 |
| **Alexis Gutierrez** | V-31.563.986 |

---

## 🎯 1. Área Temática y Cumplimiento de Normativa

De acuerdo a las directrices de cátedra evaluadas en pizarra, el proyecto se enmarca dentro de:
* **Área:** *Industria y Productividad*
* **Plataforma de Hardware:** Familia compatible ESP32 / Arduino (**ESP32-S3-DevKitC-1 N16R8**)
* **Enfoque Comercial Requerido:** Solución con viabilidad de mercado demostrable y justificación económica de compra.

---

## 📌 2. Introducción y Planteamiento del Problema

### ¿Por qué es necesario este producto?
En las pequeñas y medianas empresas (PyMEs), talleres industriales, constructoras y plantas de manufactura, el registro de asistencia del personal y el cómputo de horas laboradas continúa realizándose mediante métodos vulnerables:
1. **Planillas físicas o libros de firmas:** Susceptibles a falsificación, pérdida y errores humanos de transcripción.
2. **Relojes biométricos propietarios de alto costo:** Equipos como ZKTeco o Anviz tienen precios que oscilan entre $350 y $600 USD, exigen licencias anuales de software privativo en la nube y presentan fallas críticas cuando se interrumpe el suministro eléctrico o la conectividad a Internet.
3. **Litigios por liquidación de horas extra:** La falta de una estampa de tiempo legal e inalterable genera discrepancias en el pago de recargos nocturnos y jornadas extraordinarias.

### ¿Qué necesidad resuelve?
**TrazLink™ Work-ID** provee un **Terminal de Pared Autónomo para Control de Asistencia y Pre-liquidación Salarial en el Borde (Edge Computing)**:
- **Lectura instantánea (< 200 ms):** Mediante tarjetas inteligentes RFID de proximidad (Mifare 13.56 MHz).
- **Inmutabilidad Temporal:** Gobernanza horaria mediante hardware RTC DS3231 con oscilador TCXO (deriva < 2 ppm/año) y respaldo por batería LIR2032 recargable, inmune a caídas de red o cortes de energía.
- **Procesamiento en el Borde:** Calcula en tiempo real las horas ordinarias, minutos de retardo y horas extraordinarias diurnas y nocturnas según la legislación laboral.
- **Operatividad Desconectada (Modo Isla):** Almacenamiento local en memoria no volátil (NVS Flash / LittleFS) de hasta 10,000 registros para sincronización diferida.

---

## 💼 3. Plan de Negocio y Enfoque Comercial

### Cliente Ideal
1. **Pequeñas y Medianas Empresas (10 a 150 empleados):** Oficinas comerciales, distribuidores y comercios minoristas.
2. **Plantas Industriales y Talleres:** Entornos donde operan turnos rotativos (mañana, tarde y noche).
3. **Sector Construcción y Almacenes:** Puntos de acceso provisionales o remotos que requieren terminales resistentes y autónomos.

### Propuesta de Valor y Ventaja Competitiva
* **Ahorro superior al 55% - 70%** frente a soluciones comerciales propietarias.
* **Cero costo de licenciamiento recurrente forzoso.**
* **Hardware abierto y reparable:** Componentes estándar de fácil sustitución local.

---

## 🔗 Enlaces Contextuales del Grafo

- Justificación de buses y procesador: [[Decisiones_Diseno]]
- Modelo de datos relacional 3NF: [[Esquema_Base_Datos]]
- Interfaz HMI industrial: [[Sistema_Diseno]]
- Control de versiones: [[Historial_De_Versiones]]

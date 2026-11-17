# 🎨 Sistema de Diseño y Guía de Interfaz (UX/UI)

Este documento especifica la identidad visual, paleta de colores y componentes interactivos de **ChronoLink™ Enterprise**, tanto para el firmware embebido en la pantalla TFT ILI9341 (320x240) como para la suite web de presentación interactiva.

---

## 🌌 1. Identidad Visual: Industrial Tech & Enterprise Cyberpunk

La interfaz combina la sobriedad y legibilidad requeridas en entornos industriales/corporativos con una estética de alta tecnología inspirada en señalética HUD y arquitectura de sistemas:

### Paleta Cromática

| Token | Código HEX | Valor RGB565 (C++) | Uso / Significado |
| :--- | :--- | :--- | :--- |
| `--bg-obsidian` | `#030712` | `0x0000` | Fondo base ultra-oscuro de bajo consumo. |
| `--cyan-core` | `#00e5ff` | `0x07FF` | Acento principal, enlaces de datos y estados activos. |
| `--emerald-success` | `#10b981` | `0x05E0` | Marcaje exitoso, empleado autorizado, en turno. |
| `--amber-warning` | `#f59e0b` | `0xFBE0` | Retardo detectado, tiempo de gracia o alerta de turno. |
| `--crimson-alert` | `#ef4444` | `0xF800` | Acceso denegado, carnet no registrado o sabotaje. |
| `--slate-card` | `#0f172a` | `0x08A5` | Contenedores de información y tarjetas de métricas. |
| `--border-tech` | `#1e293b` | `0x18E3` | Bordes delimitadores y rejillas de arquitectura. |

---

## 🔤 2. Tipografía y Jerarquía

1. **Orbitron:** Empleada en encabezados principales, nombres de productos, terminales de datos y números de reloj de gran formato.
2. **Rajdhani:** Empleada en nombres de empleados, cargos, métricas de horas laboradas y etiquetas de botones.
3. **Share Tech Mono:** Tipografía monoespaciada para direcciones de memoria, UIDs RFID, códigos de error, estampas de tiempo ISO y trazas de depuración.

---

## 📱 3. Vistas y Modos de la Pantalla TFT ILI9341 (320x240)

```
+-------------------------------------------------------+
| CHRONOLINK ENTERPRISE           [WiFi: ON] [RTC: 2ppm] |
+-------------------------------------------------------+
|                                                       |
|                     12:35:48                          |
|             Lunes, 16 de Noviembre 2026               |
|                                                       |
|       TURNO ACTIVO: MATUTINO (07:00 - 15:00)          |
|                                                       |
|  [ >> APROXIME SU TARJETA CORPORATIVA AL LECTOR << ]  |
+-------------------------------------------------------+
| Terminal: S3-WALL-01  |  Firmware: v1.0.0-PRO  | 24°C |
+-------------------------------------------------------+
```

1. **Estado de Reposo (Standby & Watchface):**
   - Muestra hora en tiempo real con segundero continuo desde el RTC DS3231.
   - Indicador de estado de red (WiFi/Offline buffer count).
   - Indicador de turno de trabajo activo según la hora local.
2. **Estado de Marcaje Exitoso (Check-in / Check-out):**
   - Transición instantánea (<100 ms).
   - Nombre del empleado, cédula y cargo.
   - Evento detectado: `[ENTRADA CONFIRMADA]` o `[SALIDA REGISTRADA]`.
   - Diagnóstico de puntualidad: `PUNTUAL` (Verde) o `RETARDO: +14 MIN` (Ámbar).
   - Activación de periféricos: Pulso breve en Buzzer y LED Verde.
3. **Estado de Alerta o Acceso Denegado:**
   - Mensaje `[TARJETA NO AUTORIZADA]`.
   - Activación de LED Rojo y doble tono de advertencia. Retorno automático en 3 segundos.

---

## 🔗 Enlaces Contextuales

- Requerimientos de negocio y objetivos del proyecto: [[Contexto_Negocio]]
- Hardware, pines e interfaces físicas: [[Decisiones_Diseno]]
- Modelo de datos y campos representados: [[Esquema_Base_Datos]]
- Historial de cambios: [[Historial_De_Versiones]]

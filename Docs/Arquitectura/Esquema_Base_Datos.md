# 🗄️ Esquema de Base de Datos y Modelo Relacional (3NF)

Este documento define la arquitectura de datos del sistema **ChronoLink™ Enterprise**, garantizando la **Tercera Forma Normal (3NF)** para evitar anomalías de inserción, actualización y borrado, optimizando la persistencia tanto en el Edge (SQLite / LittleFS local en NVS) como en la API centralizada.

---

## 📐 Diagrama Entidad-Relación (ERD)

```mermaid
erDiagram
    DEPARTAMENTOS ||--o{ EMPLEADOS : "pertenece a"
    EMPLEADOS ||--o{ EMPLEADO_TURNOS : "tiene asignado"
    TURNOS ||--o{ EMPLEADO_TURNOS : "define"
    EMPLEADOS ||--o{ MARCAJES : "registra"
    DISPOSITIVOS_TERMINAL ||--o{ MARCAJES : "captura en pared"
    PERIODOS_NOMINA ||--o{ RESUMEN_HORAS_NOMINA : "liquida"
    EMPLEADOS ||--o{ RESUMEN_HORAS_NOMINA : "acumula"

    DEPARTAMENTOS {
        int id PK
        string codigo UK
        string nombre
        int tolerancia_minutos
    }

    EMPLEADOS {
        int id PK
        string cedula UK
        string nombres
        string apellidos
        int departamento_id FK
        string cargo
        string uid_rfid UK
        decimal salario_base_hora
        boolean activo
    }

    TURNOS {
        int id PK
        string codigo UK
        string nombre
        time hora_inicio
        time hora_fin
        boolean es_nocturno
        decimal recargo_porcentaje
    }

    EMPLEADO_TURNOS {
        int id PK
        int empleado_id FK
        int turno_id FK
        int dia_semana
    }

    DISPOSITIVOS_TERMINAL {
        int id PK
        string device_id UK
        string ubicacion_pared
        string mac_address
        string ip_address
        datetime ultimo_heartbeat
        boolean en_linea
    }

    MARCAJES {
        int id PK
        int empleado_id FK
        datetime timestamp_rtc
        string tipo_evento
        int dispositivo_id FK
        int minutos_retardo
        decimal horas_trabajadas
        string estado_validacion
        boolean sincronizado
    }

    PERIODOS_NOMINA {
        int id PK
        date fecha_inicio
        date fecha_fin
        string estado
    }

    RESUMEN_HORAS_NOMINA {
        int id PK
        int periodo_id FK
        int empleado_id FK
        decimal horas_ordinarias
        decimal horas_extras_diurnas
        decimal horas_extras_nocturnas
        decimal total_devengado
    }
```

---

## 🛡️ Principios de Integridad y Normalización

1. **Cumplimiento Estricto de 3NF:**
   - **1NF:** Todos los atributos son atómicos; no existen campos repetitivos ni listas serializadas en una sola celda.
   - **2NF:** Se eliminan dependencias parciales; las claves foráneas en tablas intermedias como `EMPLEADO_TURNOS` dependen de la clave primaria completa.
   - **3NF:** No existen dependencias transitivas; los datos del departamento o del turno no se duplican dentro de la tabla `MARCAJES`.
2. **Inmutabilidad de Marcajes:** 
   La tabla `MARCAJES` opera como un libro de auditoría forense (*append-only*). Las filas no deben modificarse; correcciones administrativas se registran mediante marcajes de rectificación explícitos.
3. **Resiliencia Local (Edge-Storage en ESP32-S3):**
   El ESP32-S3 almacena una tabla local indexada en NVS Flash/LittleFS con hasta 10,000 transacciones con la bandera `sincronizado = false` para garantizar cero pérdida de marcajes ante fallos de conectividad.

---

## 🔗 Enlaces Contextuales

- Especificación de negocio y roles: [[Contexto_Negocio]]
- Asignación de buses y arquitectura física: [[Decisiones_Diseno]]
- Interfaz gráfica y estados visuales: [[Sistema_Diseno]]
- Control de versiones: [[Historial_De_Versiones]]

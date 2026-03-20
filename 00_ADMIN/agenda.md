# Agenda — Sesión técnica SEW (120 min)

## 1. Introducción al sistema de accionamiento (10 min)

- Arquitectura general:
  - Variador MOVITRAC® advanced
  - Motor DRN con encoder MOVILINK DDI
  - Comunicación PROFINET
- Concepto de integración: motor–variador–control

---

## 2. Hardware y conexionado (15 min)

- Topología del sistema
- Cable híbrido MOVILINK DDI
- Encoder absoluto integrado
- Elementos del variador:
  - CMM
  - CDM
  - MOVIKIT
- Consideraciones de instalación

---

## 3. Configuración en MOVISUITE (35 min)

- Creación del proyecto
- Detección del variador
- Configuración del motor DRN
- Parametrización básica:
  - Modo de operación
  - Rampas y límites
  - Unidades
- Configuración de encoder (DDI)
- Ajustes críticos:
  - Límites software (SW limit switch)
  - Sentido de movimiento
- Funciones relevantes:
  - Stop setpoint
  - Start offset
  - Standstill

---

## 4. Modos de operación y estados del variador (15 min)

- Estados funcionales:
  - FCB01 — Output stage inhibit
  - FCB02 — Stop default (standstill)
  - FCB13 / FCB14
- Comportamiento del freno
- Condiciones de habilitación

---

## 5. Integración PROFINET en TIA Portal (15 min)

- Importación del GSDML
- Configuración del dispositivo en PLC
- Asignación de direcciones
- Telegramas de control
- Control Word / Status Word:
  - Enable
  - Standby
- Estructura de control desde PLC

---

## 6. Bloque final — Preguntas y respuestas (30 min)

- Resolución de dudas
- Ajustes finales de puesta en marcha

# Resumen Integral: Curso SEW Accionamientos

**Introducción:** Este curso o sesión técnica se centra en la arquitectura, componentes, configuración e integración de los sistemas de accionamiento **SEW-EURODRIVE** de la plataforma **MOVI-C®** con el sistema de control **Siemens** a través de la comunicación **PROFINET**.

## 1. Arquitectura y Componentes Clave

El sistema se basa en una topología industrial de vanguardia que busca la simplificación del cableado y la optimización de la instalación.

### Puntos Destacados

- **Accionamiento Principal:** Variador **MOVITRAC® advanced (MCX91A)**.
- **Motor:** Motorreductor **DRN** con interfaz digital **MOVILINK® DDI** (Digital Drive Interface) y un encoder absoluto integrado (**AK8Z**).
- **Cableado DDI:** Uso de un **Cable Híbrido Coaxial DDI** que consolida potencia, freno y señal de encoder en un solo cable, reduciendo drásticamente puntos de falla y tiempo de instalación en comparación con el cableado clásico.
- **Control PLC:** Se utiliza un **PLC Siemens** (ej. **ET200SP Open Controller**) como controlador central, comunicado con los accionamientos mediante el bus de campo **PROFINET**.
- **Módulos de Hardware:** El variador MOVI-C® incluye módulos estandarizados como el **Módulo de Memoria (CMM11A)** y el **Módulo de Diagnóstico (CDM11A)**.

## 2. Software y Modos de Operación (MOVIKIT®)

La funcionalidad del accionamiento se define por los niveles de aplicación del software MOVIKIT®, activando distintos Bloques de Función (FCB).

### Comparativa de Niveles MOVIKIT®

| Función                     | MOVIKIT® Velocity Drive (5 PD) / Nivel 0                   | MOVIKIT® Positioning Drive (8 PD) / Nivel 1                      |
| :-------------------------- | :--------------------------------------------------------- | :--------------------------------------------------------------- |
| **FCB Principal**           | FCB 05 (Control de Velocidad Estándar)                     | FCB 09, 12, 20, 21 (Posición y Freno)                            |
| **Control de Velocidad**    | FCB 05 (Enfoque en aplicaciones controladas por velocidad) | Incluido                                                         |
| **Gestión de Paradas**      | FCB 02, 13, 14, 26                                         | Incluido                                                         |
| **Posicionamiento y Freno** | No disponible                                              | FCB 09, 12, 20, 21 (Posición Absoluta/Relativa/Módulo)           |
| **Requisito de Encoder**    | Opcional (para 5 PD - Velocity)                            | Obligatorio (para las funciones completas de 8 PD - Positioning) |

### Bloques de Función de Parada (FCB)

Los FCB son funciones de _firmware_ gestionadas por MOVIKIT® para paradas controladas:

- **FCB 02 (Parada estándar):** Parada por defecto en transiciones operativas.
- **FCB 13 (Límite de aplicación):** Detiene el eje respetando los límites de aceleración y velocidad configurados.
- **FCB 14 (Parada de emergencia):** Activa la rampa de emergencia para una detención prioritaria ante fallos (activación por Bit PO 1.0 = 0).

## 3. Temas de la Sesión Técnica

El curso se estructura en torno a los siguientes temas principales:

- **Introducción al sistema:** Arquitectura general y concepto de integración motor–variador–control.
- **Hardware y Conexionado:** Topología, cable híbrido DDI y consideraciones de instalación.
- **Configuración en MOVISUITE:** Creación de proyecto, detección, parametrización básica (Modo de operación, Rampas, Unidades) y ajustes críticos.
- **Modos de Operación y Estados:** Descripción de los estados funcionales (FCB01, FCB02) y comportamiento del freno.
- **Integración PROFINET en TIA Portal:** Uso de archivos GSDML, configuración del dispositivo en el PLC, asignación de direcciones y telegramas de control (Control Word / Status Word).

---

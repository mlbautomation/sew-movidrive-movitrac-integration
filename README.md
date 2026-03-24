# Integración SEW MOVI-C (MOVIDRIVE/MOVITRAC) con PLC Siemens ET 200SP vía PROFINET

## Descripción

Este repositorio y sesión técnica documentan la arquitectura de control y la puesta en marcha de una máquina paletizadora automática (referencia Quimarox). Se analiza la integración práctica del moderno ecosistema de accionamientos **MOVI-C de SEW-EURODRIVE** en comunicación directa con un controlador maestro **PLC Siemens ET 200SP** utilizando la red PROFINET.

El objetivo principal es mostrar cómo simplificar la ingeniería, estandarizar el control de ejes (similar al Telegrama 111) y reducir tiempos de comisionamiento utilizando librerías preconfiguradas y tecnologías de monocable.

## Arquitectura de Hardware

La máquina implementa dos topologías físicas bajo un mismo controlador PROFINET:

- **Controlador Maestro:** PLC Siemens SIMATIC ET 200SP con memoria CFast.
- **Ejes Auxiliares (Empujadores):** Variadores **MOVIDRIVE® technology** con cableado clásico (cables independientes para potencia, freno y encoder).
- **Ejes Críticos (Elevación/Pinzas):** Variadores **MOVITRAC® advanced** controlando motores asíncronos DRN mediante tecnología **MOVILINK® DDI**.

## Tecnologías Destacadas

- **MOVILINK® DDI:** Tecnología de monocable coaxial que transmite potencia, control del freno y datos del encoder (absoluto multivuelta) en una sola manguera, permitiendo la auto-identificación del motor.
- **Safety (Seguridad Funcional):** Implementación de paradas seguras mediante **STO (Safe Torque Off)** y comunicación **PROFIsafe**.
- **Módulo de Memoria CMM:** Respaldo físico tipo "plug & play" para reemplazo rápido de variadores sin pérdida de configuración de red.
- **Resolución Endianness:** Uso de Bloques de Función (FB) de SEW que solucionan internamente el cruce de bytes (Big Endian vs Little Endian) típico en la integración con Siemens.

## Software y Configuración

- **Entorno Siemens:** TIA Portal (Proyectos de ejemplo disponibles en v18, actualizables a v19).
- **Entorno SEW:** MOVISUITE para configuración de hardware.
- **MOVIKIT®:** Uso de módulos de software estandarizados mediante Niveles de Aplicación:
  - **Nivel 0:** Control de velocidad básico (FCB 05).
  - **Nivel 1:** Habilitación de control de posición (FCB 09), referenciado/homing (FCB 12) y test de freno (FCB 21).

## Índice del Video (Capítulos)

Puedes usar esta guía de tiempos para navegar por los temas clave de la presentación:

00:00 - Presentación de la información y la aplicación: Introducción al paletizador Kimarox y recursos del proyecto.  
04:47 - Arquitectura de control: Análisis de la topología y control de motores en paralelo.  
06:19 - Tecnología MOVILINK® DDI: Ventajas del cable único (potencia, freno y datos).  
07:11 - Hardware utilizado: Control con PLC Siemens ET 200SP y memoria CFast.  
08:04 - Tecnología Safety: Conceptos básicos de seguridad, PROFIsafe y paradas de emergencia.  
14:39 - Nivel Tecnológico 0: Control de velocidad y bloques de función base (FCB).  
17:41 - Nivel Tecnológico 1: Habilitación de control de posición, referenciado y test de freno.  
19:46 - Software MOVISUITE y FCB: Configuración de equipos y prueba manual de bits.  
21:08 - Comparativa MOVIDRIVE B: Evolución desde la programación manual (IPOS) hacia los bloques predefinidos.  
25:07 - Funciones adicionales: Aplicación de límite de torque y desactivación de monitoreo de velocidad (Lag error).  
30:22 - MOVITRAC advanced vs MOVIDRIVE technology: Diferencias en capacidad de sobrecarga dinámica (150% vs 200%) en posicionamiento.  
31:21 - Tecnología Safety (STO): Funcionamiento del Safe Torque Off en el hardware.  
32:36 - Parámetros de parada: Prioridades de bits para detención por aplicación o emergencia.  
34:00 - Integración SEW MOVI-C con Siemens: Uso de archivos GSDML y proyectos de ejemplo.  
36:52 - TIA Portal: Uso de Function Blocks (FB) pre-configurados para el programador.  
40:13 - Estandarización (Telegrama 111): Similitud de MOVIKIT con los estándares de control de Siemens y Festo.  
41:45 - Barreras de entrada con integradores: Importancia comercial de entregar librerías listas para usar a los fabricantes (OEM).  
52:11 - Bloque de preguntas: Big Endian vs Little Endian: Cómo las librerías solucionan el cruce de bytes en Siemens.  
53:59 - Bloque de preguntas: Envío de parámetros del variador: Límite de las 16 palabras (Process Data) en PROFINET.  
55:47 - Bloque de preguntas: Trabajo con SEW: Experiencia integrando la plataforma MOVI-C.  
56:42 - Bloque de preguntas: ¿Por qué no usar servos?: Justificación del uso de motores asíncronos DRN para esta máquina.  
57:26 - Bloque de preguntas: Test de freno: Inyección de torque y monitoreo de pulsos vía DDI.
58:18 - Despedida y cierre del conversatorio.

## Recursos Adicionales

- [Modelos 3D y Planos de la máquina paletizadora Kimarox] _(Añadir enlace URL)_
- [Archivos GSDML de SEW-EURODRIVE] _(Añadir enlace URL)_
- [Proyecto Base TIA Portal (v18)] _(Ubicado en la carpeta de este repositorio)_

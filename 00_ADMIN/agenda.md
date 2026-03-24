# Agenda: Integración SEW MOVI-C con PLC SIEMENS ET 200SP vía PROFINET

Esta agenda detalla el cronograma y los temas tratados en el conversatorio técnico sobre la integración de variadores SEW-EURODRIVE (MOVIDRIVE technology y MOVITRAC advanced) con controladores Siemens ET 200SP, aplicados a una máquina paletizadora.

## Cronograma de la Sesión

- **00:00 - Presentación de la información y la aplicación:** Introducción al paletizador automático Quimarox y revisión de los recursos del proyecto, incluyendo modelos 3D y repositorios de GitHub.
- **04:47 - Arquitectura de control:** Análisis de la topología de la máquina y debate sobre el control de motores asíncronos en paralelo.
- **06:19 - Tecnología MOVILINK® DDI:** Exploración de las ventajas del uso de un cable único coaxial que transmite la potencia, el control del freno y los datos del encoder de manera simultánea.
- **07:11 - Hardware utilizado:** Descripción del controlador maestro PLC Siemens ET 200SP equipado con memoria CFast y soporte para módulos remotos.
- **08:04 - Tecnología Safety:** Explicación de los conceptos básicos de seguridad funcional a través de bus (PROFIsafe) y los diferentes tipos de paradas de emergencia frente a errores de programación.
- **14:39 - Nivel Tecnológico 0:** Implementación del control de velocidad puro mediante bloques de función base (como el FCB 05) y gestión de rampas de parada.
- **17:41 - Nivel Tecnológico 1:** Habilitación de funciones avanzadas como el control de posicionamiento (FCB 09), el referenciado o homing (FCB 12), el modo Jog (FCB 20) y el test de freno (FCB 21).
- **19:46 - Software MOVISUITE y FCB:** Uso del entorno de ingeniería para la configuración de equipos, establecimiento de permisos por nivel y prueba manual de bits (Process Data) sin depender del PLC.
- **21:08 - Comparativa MOVIDRIVE B:** Análisis de la evolución técnica desde la antigua programación manual y estructuración de bits (IPOS) hacia los bloques predefinidos de la generación MOVI-C.
- **25:07 - Funciones adicionales:** Aplicación práctica de la limitación de torque en pleno control de velocidad y la desactivación del monitoreo de posición (_Lag error_) para evitar fallas en mecanismos atascados.
- **30:22 - MOVITRAC advanced vs MOVIDRIVE technology:** Comparativa de hardware para posicionamiento, destacando las diferencias en la capacidad de sobrecarga dinámica (150% frente a 200%) y opciones de seguridad avanzadas.
- **31:21 - Tecnología Safety (STO):** Funcionamiento y arquitectura básica del _Safe Torque Off_ cableado de doble canal en los equipos de gama tecnológica.
- **32:36 - Parámetros de parada:** Explicación de las prioridades de los bits del _Control Word_ para gestionar una detención por aplicación frente a una parada de emergencia.
- **34:00 - Integración SEW MOVI-C con Siemens:** Instalación de archivos GSDML y uso de proyectos de ejemplo base en el entorno de Siemens.
- **36:52 - TIA Portal:** Uso de librerías y _Function Blocks_ (FB) pre-configurados entregados por SEW para facilitar la labor del programador del PLC.
- **40:13 - Estandarización (Telegrama 111):** Similitud de la estructura de MOVIKIT con los estándares de control ampliamente utilizados en la industria, como el Telegrama 111 de Siemens y Festo.
- **41:45 - Barreras de entrada con integradores:** Reflexión comercial sobre la importancia crítica de entregar código empaquetado y librerías listas para usar a los fabricantes (OEM), con el fin de ahorrarles horas de ingeniería y desarrollo.

## Bloque de Preguntas y Respuestas

- **52:11 - Big Endian vs Little Endian:** Explicación sobre cómo las librerías de SEW solucionan internamente el cruce de bits típico al comunicar los 16 bits más significativos invertidos en la arquitectura Siemens.
- **53:59 - Envío de parámetros del variador:** Análisis de la limitación en la red PROFINET a un máximo de 16 palabras de _Process Data_ (datos de proceso) y la dificultad para leer parámetros aislados.
- **55:47 - Trabajo con SEW:** Conclusiones sobre la experiencia positiva de integrar la plataforma estandarizada frente a la programación en lenguaje C (IPOS).
- **56:42 - ¿Por qué no usar servos?:** Justificación técnica del uso de motores asíncronos (jaula de ardilla) de la serie DRN en lugar de servomotores, ya que la aplicación no requería una altísima dinámica y la precisión la otorgaba el encoder absoluto.
- **57:26 - Test de freno:** Detalle sobre cómo se inyecta corriente (torque al 100-120%) sin liberar la bobina del freno, mientras el variador evalúa los pulsos de movimiento del encoder vía DDI.
- **58:18 - Despedida:** Cierre oficial de la sesión técnica y agradecimientos.

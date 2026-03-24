# Resumen Técnico: Integración SEW MOVI-C con PLC SIEMENS ET 200SP vía PROFINET

## 1. Contexto de la Aplicación y Arquitectura

La integración analizada se basa en una máquina paletizadora automática de cajas de la marca Kimarox, cuyos planos y modelos 3D son de acceso libre. La arquitectura de la máquina se divide principalmente en estaciones de empuje de cajas y un sistema de elevación de apilado.

Como controlador maestro de la red se emplea un PLC Siemens SIMATIC ET 200SP equipado con memoria CFast. Para el accionamiento mecánico, la máquina utiliza un enfoque híbrido de control:

- **Ejes de Empuje:** Utilizan variadores **MOVIDRIVE technology** con cableado clásico separado para potencia, freno y encoder.
- **Eje de Elevación:** Consiste en un eje solidario movido por dos motores asíncronos conectados en paralelo a un único variador **MOVITRAC advanced**. A pesar de requerir sincronismo, el fabricante optó por un control de velocidad puro sin retroalimentación de encoder para este sector.

A nivel de hardware de accionamiento, la principal diferencia radica en que el MOVIDRIVE soporta un 200% de sobrecarga dinámica y cuenta con funciones de seguridad más avanzadas, mientras que el MOVITRAC soporta un 150% de sobrecarga.

## 2. Tecnologías de Campo Destacadas

### MOVILINK® DDI (Monocable)

En los ejes más críticos se implementaron motorreductores de la serie DRN equipados con tecnología MOVILINK DDI. Esta tecnología transmite la potencia, el control del freno y la señal del encoder (absoluto multivuelta) a través de un único cable coaxial híbrido con conector rápido. Su mayor ventaja es que el variador auto-identifica los parámetros del motor y del encoder al instante, eliminando errores de configuración y reduciendo los tiempos de puesta en marcha.

### Seguridad Funcional (Safety) y Respaldo

El sistema integra la función de seguridad **Safe Torque Off (STO)**, la cual desenergiza el motor mediante un hardware dedicado de doble canal. Al utilizar el ecosistema ET 200SP, esta seguridad puede gestionarse de forma centralizada a través del bus de comunicación mediante el protocolo **PROFIsafe**, priorizando las paradas de emergencia por encima de la lógica del programador. Además, los variadores cuentan con un módulo de memoria físico (CMM) que actúa como un respaldo portátil ("pendrive"); si un equipo se daña, la memoria se inserta en el nuevo variador conservando toda la configuración de red y aplicación.

## 3. Estandarización de Software: MOVIKIT y FCB

A diferencia de la generación anterior (MOVIDRIVE B), donde el programador estructuraba los bits manualmente mediante lenguaje IPOS, la plataforma MOVI-C utiliza bloques de función predefinidos llamados **FCB** organizados en niveles de aplicación (MOVIKIT).

- **Nivel 0 (Velocidad):** Incluido por defecto, utiliza 5 palabras de proceso (_Process Data_). Habilita el control de velocidad (FCB 05) y gestiona distintos tipos de paradas, como la parada normal (FCB 02), límite de aplicación (FCB 13) o emergencia (FCB 14).
- **Nivel 1 (Posición):** Requiere una clave de activación y utiliza 8 palabras de proceso. Habilita el posicionamiento absoluto/relativo (FCB 09), referenciado o _homing_ (FCB 12), modo manual Jog (FCB 20) y el test de freno (FCB 21).

El software MOVISUITE permite probar estos bits de forma manual y local sin necesidad de que el PLC esté conectado. Adicionalmente, se pueden configurar comportamientos avanzados, como establecer un límite de torque durante el control de velocidad, o desactivar la monitorización de posición (_lag error_) para evitar fallas cuando el mecanismo de la máquina se atasca.

## 4. Integración con Siemens (TIA Portal) y Mercado OEM

Para integrar el sistema, SEW proporciona archivos GSDML y proyectos de ejemplo con bloques de función (FB) en TIA Portal. Esta librería estandarizada resuelve internamente dos grandes retos:

1.  **Big Endian:** Siemens procesa los bytes de forma invertida (_Big Endian_). La librería de SEW reordena automáticamente estos bits, evitando que el programador tenga que cruzar los datos de forma manual.
2.  **Límites de PROFINET:** El bus permite un máximo de 16 palabras de proceso por nodo, lo que limita la lectura de parámetros aislados fuera del estándar.

A nivel comercial, ofrecer estas librerías pre-configuradas (similares en estructura al **Telegrama 111** de Siemens o Festo) es fundamental para romper barreras de entrada. Los integradores (OEMs) prefieren marcas que no les exijan invertir horas de ingeniería adicionales en desarrollar y probar código desde cero para cada máquina nueva.

## 5. Decisiones de Ingeniería y Diagnóstico

Durante la evaluación del proyecto, se justificó el uso de motores asíncronos (DRN) en lugar de servomotores síncronos debido a que la aplicación de paletizado no requería una dinámica extrema; la precisión se logró satisfactoriamente usando encoders absolutos.

Para el mantenimiento predictivo, el sistema ejecuta un **Test de Freno (FCB 21)**. En lugar de liberar el freno, el variador inyecta un torque elevado (100% al 120%) contra el freno activado y monitorea a través del cable DDI si el encoder registra algún pulso de movimiento, lo que indicaría desgaste mecánico.

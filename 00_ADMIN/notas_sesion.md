# Notas de la Sesión Técnica: Integración SEW MOVI-C con PLC SIEMENS ET 200SP vía PROFINET

## Contexto del Proyecto

- La aplicación analizada se basa en una máquina paletizadora de cajas de la marca Kimarox.
- El diseño mecatrónico incluye zonas de empuje de cajas y un sistema de elevación de ejes solidarios que requiere sincronismo.
- Toda la información de diseño, incluyendo los planos 3D, es pública y estandarizada por el fabricante.

## Arquitectura de Hardware

- **Controlador Maestro:** Se utilizó un PLC Siemens de la serie ET 200SP con memoria CFast, el cual funciona como el cerebro central que comanda a toda la máquina.
- **Accionamientos (Variadores):** Se implementaron equipos de la familia MOVI-C, específicamente MOVIDRIVE technology para los empujadores y MOVITRAC advanced para la elevación y otras áreas.
- **Capacidad de Sobrecarga:** El MOVIDRIVE technology soporta hasta un 200% de sobrecarga dinámica, mientras que el MOVITRAC advanced soporta un 150%, siendo esta una de las principales diferencias al seleccionarlos para posicionamiento.

## Tecnologías Clave Implementadas

### MOVILINK DDI (Monocable)

- En los ejes críticos se utilizaron motores asíncronos DRN adaptados con la tecnología MOVILINK DDI.
- Esta tecnología permite transmitir la potencia, el control del freno y la señal del encoder absoluto multivuelta a través de un único cable coaxial híbrido.
- El variador identifica automáticamente los datos de placa del motor, el ratio y el tipo de encoder al conectarlo, eliminando la necesidad de ingresar estos datos manualmente y reduciendo tiempos de comisionamiento.

### Seguridad Funcional (Safety)

- El sistema cuenta con la función Safe Torque Off (STO), que corta la potencia entregada al motor de forma segura mediante un hardware dedicado de doble canal.
- Al usar la familia ET 200SP, la seguridad puede gestionarse a través del bus de comunicaciones mediante PROFIsafe, independizando la parada de emergencia de la lógica de programación estándar.

### Módulo de Memoria CMM

- Los variadores integran una memoria enchufable (CMM) que funciona como un respaldo portátil.
- Permite extraer el módulo de un variador y colocarlo en otro del mismo modelo, conservando toda la configuración de red sin necesidad de reprogramar.

## Software y Niveles de Aplicación (MOVIKIT)

- **Nivel 0 (Control de Velocidad):** Viene por defecto y proporciona 5 palabras de Process Data. Habilita el control de velocidad (FCB 05) y distintos modos de parada, como la parada normal (FCB 02), límite de aplicación (FCB 13) y parada de emergencia (FCB 14).
- **Nivel 1 (Control de Posición):** Debe adquirirse mediante una clave de activación y proporciona 8 palabras de Process Data. Habilita funciones avanzadas como el posicionamiento absoluto y relativo (FCB 09), referenciado o homing (FCB 12), modo manual Jog (FCB 20) y test de freno (FCB 21).
- **Funciones Adicionales:** MOVISUITE permite aplicar un límite de torque durante el control de velocidad y desactivar el monitoreo de velocidad (lag error), lo cual es muy útil para evitar fallas si la máquina experimenta un atasco mecánico.

## Integración con Siemens TIA Portal

- **Estandarización de Bits:** SEW ha estructurado el control de sus equipos en bloques predefinidos bajo el estándar MOVIKIT, funcionando de manera muy similar a los Telegramas de Siemens (como el Telegrama 111).
- **Solución al Big Endian:** Siemens trabaja bajo la arquitectura Big Endian, lo que usualmente cruza el orden de los bits al comunicarse con otros equipos. Los bloques de función entregados por SEW solucionan internamente este reordenamiento, facilitando el trabajo del programador.
- **Límites de PROFINET:** La comunicación permite un máximo de 16 palabras de Process Data por nodo.

## Estrategia para Integradores (OEM)

- Proporcionar librerías listas para usar es vital para romper barreras de entrada comerciales.
- Los integradores de maquinaria prefieren marcas que ya les entreguen el código empaquetado y estandarizado, evitando gastar horas de ingeniería en crear lógicas de control desde cero para cada proyecto.

## Notas del Bloque de Preguntas

- **Uso de Motores Asíncronos vs Servomotores:** Se eligieron motores DRN de jaula de ardilla porque la aplicación no exigía una dinámica extrema, y la precisión requerida se cubrió perfectamente gracias al encoder absoluto incorporado.
- **Test de Freno (FCB 21):** Para evaluar el desgaste, el variador no libera el freno, sino que inyecta un torque del 100% al 120% y evalúa a través de la interfaz DDI si el encoder registra movimiento.

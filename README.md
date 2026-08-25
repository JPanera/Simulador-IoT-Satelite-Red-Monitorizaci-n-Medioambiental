# Simulador IoT-Satelital para Monitorización Medioambiental

> **Aviso:** Este repositorio funciona como un *Whitepaper* técnico que documenta la arquitectura y los resultados del proyecto. Por motivos de propiedad intelectual y seguridad, el código fuente del simulador (Python/SimPy) y el firmware de los nodos se mantienen en formato privado.

## Resumen Ejecutivo

Este proyecto consiste en el diseño, desarrollo y simulación de una **arquitectura de red IoT multinivel híbrida (Terrestre-Satelital)** orientada a la monitorización ambiental crítica y la alerta temprana de incendios forestales. El caso de estudio y despliegue teórico se centra en el Parque Natural del Montgó y la Reserva Marina de San Antonio, un entorno con orografía compleja y zonas de sombra radioeléctrica extrema.

El sistema resuelve los problemas de conectividad intermitente y restricciones energéticas severas mediante una topología de cuatro niveles que combina:
*   **LoRaWAN** para la capilaridad de sensores locales de ultra-bajo consumo.
*   **Edge Computing** para la agregación y validación de datos en el borde.
*   **Satélites LEO (FOSSA)** como *backhaul* de contingencia automatizado.

El objetivo principal es transformar una red de sensores pasiva en un **sistema distribuido resiliente y autogestionado**, capaz de sobrevivir a cortes de conectividad terrestre, ataques cibernéticos por agotamiento de energía (DoS) e interferencias, garantizando la exfiltración de alertas críticas y la recolección activa de métricas medioambientales.

## Arquitectura de Red y Desarrollo

### Topología de 4 Niveles+

La red se estrcutura jerárquicamente para la optimizar el consumo y el procesamiento:
* **Esporas (Nivel 0):** Nodos sensores de ultra-bajo consumo distribuidos densamente para recopilar datos ambientales.
* **Centinelas/Boyas (Nivel 1):** Nodos con capacidades de Edge Computing que actúan como cabezas de clúster, agregando datos y filtrando falsos positivos localmente.
* **Pasarela Híbrida (Nivel 2):** Concentrador inteligente ubicado estratégicamente que gestiona el enrutamiento y ejecuta failover automático.
* **Backhaul (Nivel 3):** Doble enlace de salida hacia la nube (4G/LTE primario y Satélite LEO como respaldo)

<img width="1437" height="1073" alt="esquema_multinivel" src="https://github.com/user-attachments/assets/9c9469ae-8d91-45cc-8862-0d2f346c517d" />


### Motor de Simulación Propio (Python/Simpy)
Para la validación de la arquitectura, se desarrolló un motor de simulación de eventos discretos (DES) desde cero en Python, utilizando la librería SimPy. Este motor modela de forma precisa:

* Física de hardware y consumo energético en Julios.
* Degradación de baterías y perfiles de irradiación solar.
* Comportamiento orbital de satélites LEO y ventanas de transmisión.
* Colisiones LoRaWAN (modelo ALOHA) y restricciones regulatorias (ciclo de trabajo).

## Ciberseguridad y Resiliencia

La red implementa mecanismos avanzados para garantizar la integridad y disponibilidad operativa frente a amenazas:

### Algoritmo de Validación Cooperativa (Consenso de Vecinos)

<img width="981" height="327" alt="imagen" src="https://github.com/user-attachments/assets/a2c8e8cd-fa3d-4552-94d6-b940925df8e5" />

Transforma la red en un sistema distribuido de verificación. Ante una anomalía, el nodo iniciador consulta a sus vecinos lógicos antes de escalar la alerta. Este filtro mitigó el 100% de los falsos positivos simulados, ahorrando un 83.5% del presupuesto energético al evitar transmisiones satelitales innecesarias.

<img width="1036" height="523" alt="imagen" src="https://github.com/user-attachments assets/0290aae4-9d37-4476-940d-37dbaf78d66e" />


### Protocolo H-OSEAP (Hybrid-Optimized Secure Energy Aware Protocol)

<img width="1192" height="625" alt="imagen" src="https://github.com/user-attachments/assets/7b55b89f-f796-4857-be3e-da93f7fb15b2" />


Adaptación de seguridad para entornos LoRaWAN restringidos. Sustituye la rotación frecuente de claves de sesión por una renovación episódica vía multicast y cifra el tráfico con AES-128, manteniendo la integridad del canal sin saturar el payload.


### Modelo de Gestión Energética por Estados (MGEE)

Máquina de estados que supervisa el State of Charge (SOC) de cada nodo. Si el nivel cae por debajo del 20%, la red transiciona a un modo de "Supervivencia", reduciendo el muestreo y degradando el cifrado (priorizando la transmisión de emergencias). Ante ataques DoS energéticos, el MGEE logró extender la vida útil del nodo en un 146%.

<img width="262" height="246" alt="imagen" src="https://github.com/user-attachments/assets/e832257f-7af4-42bd-9712-7a2b402a4acc" />


## Viabilidad Económica

El estudio demuestra la sostenibilidad del proyecto. El análisis ROSI (Retorno de la Inversión en Sostenibilidad) estima un retorno del 2588% en costes de extinción y restauración evitados mediante la detección temprana, justificando el CAPEX y el mantenimiento proyectado a 10 años.

<img width="1255" height="1125" alt="imagen" src="https://github.com/user-attachments/assets/e92e93c0-e36d-4680-8e9b-a5dbb2d4daf8" />








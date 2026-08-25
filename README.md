# Simulador IoT-Satelital para Monitorización Medioambiental

> **Aviso:** Este repositorio funciona como un *Whitepaper* técnico que documenta la arquitectura y los resultados del proyecto. Por motivos de propiedad intelectual y seguridad, el código fuente del simulador (Python/SimPy) y el firmware de los nodos se mantienen en formato privado.

## 📋 Resumen Ejecutivo

Este proyecto consiste en el diseño, desarrollo y simulación de una **arquitectura de red IoT multinivel híbrida (Terrestre-Satelital)** orientada a la monitorización ambiental crítica y la alerta temprana de incendios forestales. El caso de estudio y despliegue teórico se centra en el Parque Natural del Montgó y la Reserva Marina de San Antonio, un entorno con orografía compleja y zonas de sombra radioeléctrica extrema.

El sistema resuelve los problemas de conectividad intermitente y restricciones energéticas severas mediante una topología de cuatro niveles que combina:
*   **LoRaWAN** para la capilaridad de sensores locales de ultra-bajo consumo.
*   **Edge Computing** para la agregación y validación de datos en el borde.
*   **Satélites LEO (FOSSA)** como *backhaul* de contingencia automatizado.

El objetivo principal es transformar una red de sensores pasiva en un **sistema distribuido resiliente y autogestionado**, capaz de sobrevivir a cortes de conectividad terrestre, ataques cibernéticos por agotamiento de energía (DoS) e interferencias, garantizando la exfiltración de alertas críticas y la recolección activa de métricas medioambientales.

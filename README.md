🦖 Godzilla V5: High-Frequency Trading (HFT) Modular Engine
Godzilla V5 es un sistema avanzado de trading algorítmico diseñado bajo una arquitectura de micro-servicios internos. El motor está optimizado para ejecutarse en entornos Linux (Oracle Cloud VM) y utiliza una estrategia híbrida que combina la microestructura del mercado (Order Flow) con indicadores estadísticos de volatilidad.

🎯 Objetivo del Proyecto
Construir una plataforma de ejecución robusta y escalable capaz de procesar flujos masivos de datos en tiempo real (Tick-by-Tick), minimizando el deslizamiento (slippage) y automatizando la toma de decisiones mediante algoritmos de Eficiencia de Volumen.

🏗️ Arquitectura del Sistema (Modularidad)
El sistema se fragmentó en módulos independientes para garantizar que el fallo en un proceso no comprometa la integridad total del bot:

main_godzilla.py: El orquestador principal que sincroniza los hilos de ejecución.

motores_data.py: Ingestión de datos vía WebSockets de Binance con lógica de reconexión y buffers asíncronos (deques).

cvd_g.py: Motor analítico que calcula la Eficiencia del CVD (Cumulative Volume Delta) para medir la presión real de compra/venta.

modulo_bollinger.py: Filtro de volatilidad que identifica zonas de agotamiento y reversión estadística.

godzilla_intelligence.py: El cerebro de gestión de riesgo; maneja salidas por debilidad de volumen y Stop Loss dinámicos.

modulo_ejecucion.py: Capa de abstracción para la API de Alpaca, gestionando órdenes de mercado y liquidaciones de emergencia.

config.py: Gestión centralizada de credenciales, gestión de capital y parámetros operativos.

🚀 Infraestructura y Despliegue (Linux + tmux)
El bot opera en una VM de Oracle Cloud para asegurar baja latencia y alta disponibilidad.

Persistencia vía tmux: Se utiliza tmux para gestionar múltiples paneles de ejecución independientes. Esto permite que el sistema opere 24/7 de forma persistente aunque la sesión SSH sea interrumpida.

Monitoreo en Tiempo Real: La estructura de paneles permite observar simultáneamente la entrada de datos, el cálculo de indicadores y el estado de las órdenes en ejecución.

🛠️ Desafíos de Ingeniería y Problemas Actuales
Como todo sistema HFT en fase de desarrollo, Godzilla V5 enfrenta retos técnicos complejos que están en proceso de resolución:

Sincronización de Tiempo (Bugs de Timestamp): Se han identificado desfases ocasionales entre el reloj de la VM y el servidor del Exchange (NTP drift). Estamos trabajando en una lógica de offset dinámico para evitar el rechazo de órdenes.

Optimización de Hiperparámetros: El umbral de "Eficiencia de Flujo" es altamente sensible a la volatilidad. Actualmente se realiza un proceso de fine-tuning para reducir falsos positivos en mercados laterales.

Concurrencia: Optimización de la comunicación entre el hilo de motores_data y el main para evitar cuellos de botella durante picos de volumen masivo.

📈 Conclusiones y Aprendizajes
La Modularidad es Poder: Separar la lógica de datos de la de ejecución permitió realizar backtesting en vivo de módulos individuales sin arriesgar capital.

Order Flow > Indicadores: El uso de CVD Relativo ha demostrado ser un indicador mucho más fiel de la intención del mercado que los indicadores técnicos tradicionales.

Infraestructura Crítica: El éxito de un bot HFT depende tanto de la estrategia como de la estabilidad del entorno Linux y la gestión de procesos.

Desarrollado por: [Tu Nombre]

Stack: Python | Linux | tmux | WebSockets | Alpaca API | Oracle Cloud

# Tesis: Modelamiento Dinámico de la Adopción de Electromovilidad en Chile

Este repositorio contiene la arquitectura computacional desarrollada para la tesis de grado en Ingeniería Civil Eléctrica, titulada: 
**"Dinámicas de largo plazo para la adopción de vehículos eléctricos en Chile"**.

## Descripción del Proyecto
El simulador integra dos entornos de programación para capturar la complejidad sociotécnica del mercado automotor chileno:
1. **Módulo PLN (Python):** Utiliza modelos de lenguaje (`BERT`) y e-AHP semántico para extraer señales de fricción del mercado e Índice de Percepción Social (IPS) a partir de un corpus documental nacional.
2. **Módulo de Simulación (Julia):** Ejecuta la resolución numérica de las ecuaciones diferenciales de difusión de Bass, integrando variables físicas (Stock & Flow) y restricciones regulatorias mediante `DifferentialEquations.jl`.


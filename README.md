## Dinámicas de Largo Plazo en la Adopción de Vehículos Eléctricos en Chile

Repositorio de código fuente asociado al Proyecto de Título de Ingeniería Civil Eléctrica — Pontificia Universidad Católica de Valparaíso.

## Descripción

Este repositorio implementa la arquitectura computacional híbrida desarrollada para modelar la adopción de vehículos eléctricos de batería (BEV) e híbridos enchufables (PHEV) en Chile bajo distintos escenarios de política pública, infraestructura de carga y fricción de mercado. El modelo integra dos módulos independientes:

**Módulo PLN (Python):** Procesa un corpus de documentos institucionales nacionales (2018–2025) mediante el modelo `tulio-chilean-spanish-bert`, obteniendo señales semánticas de barreras e impulsores de adopción por dimensión económica, social e infraestructural. Implementa el procedimiento de Ponderación Semántica de Criterios (PSC) basado en anclas impulso–barrera y construye el Índice de Percepción Social (IPS). Las señales resultantes se exportan como CSV hacia el simulador Julia.

**Módulo de Simulación (Julia):** Resuelve numéricamente el sistema de tres ecuaciones diferenciales ordinarias acopladas (Bass normalizado + Stock and Flow) mediante el solver Tsit5 de `DifferentialEquations.jl`. Simula cuatro escenarios (BAU, Impulso Económico, Estrategia Integral y Objetivo ENE), calcula impactos eléctricos y ambientales, y ejecuta análisis de sensibilidad paramétrica sobre los parámetros de escenario y los pesos base del procedimiento PSC.

## Estructura del repositorio:
/python
│   pln_embeddings.py        # Procesamiento del corpus y cálculo de embeddings
│   eahp_semantico.py        # Procedimiento PSC: anclas, similitud coseno, IPS
│   input_pln_dinamico_local.csv  # CSV de salida hacia Julia
│
/julia
│   simulador_nacional.jl    # Simulador principal: ODEs, escenarios, impactos
│   sensibilidad_psc.jl      # Análisis de sensibilidad sobre pesos PSC
│   sensibilidad_estrategia_integral.csv  # Resultados sensibilidad paramétrica
│   sensibilidad_pesos_psc.csv            # Resultados sensibilidad PSC


## Requisitos

**Python**
python >= 3.9
transformers
torch
numpy
pandas
scikit-learn

**Julia**
julia >= 1.9
DifferentialEquations.jl
Plots.jl
CSV.jl
DataFrames.jl

---

## Instrucciones de ejecución

### Paso 1 — Módulo PLN (Python)

```bash
cd python
python pln_embeddings.py
python eahp_semantico.py
```

Esto genera el archivo `input_pln_dinamico_local.csv` con las señales 
semánticas anuales requeridas por el simulador Julia.

### Paso 2 — Módulo de Simulación (Julia)

```bash
cd julia
julia simulador_nacional.jl
```

El simulador lee automáticamente el CSV generado en el Paso 1, ejecuta 
los cuatro escenarios y genera los gráficos y tablas de resultados.

### Paso 3 — Análisis de sensibilidad PSC (opcional)

```bash
julia sensibilidad_psc.jl
```

Genera la tabla de sensibilidad sobre los pesos base W_ECO, W_SOC y 
W_INFRA bajo variaciones de ±10% y ±20%.

---

## Resultados principales

| Escenario | s2030 | s2035 | Parque 2035 | Tipping point |
|---|---|---|---|---|
| BAU | 12,4% | 39,6% | 489.775 | 2037 |
| Impulso Económico | 14,8% | 50,1% | 598.105 | 2036 |
| Estrategia Integral | 21,5% | 73,1% | 878.768 | 2034 |
| Objetivo ENE | 62,5% | 99,4% | 1.764.332 | 2030 |

---

## Referencia

Si utilizas este código en tu investigación, por favor cita:

> Reyes Guzmán, S. A. (2026). *Dinámicas de largo plazo en la adopción 
> de vehículos eléctricos en Chile*. Proyecto de Título, Ingeniería Civil 
> Eléctrica, Pontificia Universidad Católica de Valparaíso.

# 🚦 Inteligencia Artificial Aplicada a Sistemas Urbanos en Madrid

**Curso:** Data Analytics for Urban Systems: From Co-Pilot to Autonomous Agents  
**Módulo:** 4 — Proyecto Final e Investigación Aplicada  
**Autor:** Manuel A. Albornoz

## 📝 Descripción General del Repositorio
Este repositorio contiene una suite de soluciones avanzadas de Ciencia de Datos e Inteligencia Artificial diseñadas para resolver problemáticas complejas de movilidad urbana en Madrid. El proyecto 
evoluciona desde la optimización semafórica (Multi-Agente) hasta la simulación de políticas públicas (Grafos Viales), pasando por la predicción espacio-temporal (GNN) y el control dinámico mediante 
Aprendizaje por Refuerzo (RL).

### 📂 Estructura del Repositorio
*   **`Agente_Semaforos_MultiAgente.ipynb`**: Sistema Multi-Agente para la identificación y auditoría ética de semáforos a re-sincronizar.
*   **`Agente_Prescriptivo_OSMnx.ipynb`**: Simulador de cierre de calles basado en topología real (OSMnx) y datos de tráfico (DuckDB).
*   **`GNN_Trafico_Madrid.ipynb`**: Red Neuronal de Grafos (GCN) para la predicción del tráfico incorporando topología espacial.
*   **`Agente_RL_Semaforos.ipynb`**: Control Semafórico Adaptativo usando Reinforcement Learning (PPO) y simulación de ciclos.

---

## 🏗️ 1. Agente Multi-Agente para la Optimización Semafórica
Este proyecto implementa un sistema de **Inteligencia Artificial Multi-Agente** diseñado para identificar intersecciones (semáforos) que requieren un ajuste en su programación, buscando congestión 
anormalmente alta en horario valle (10:00 a 16:00).

### Arquitectura:
1. **Servidor MCP:** Expone herramientas para consultar el dataset.
2. **Agente Analista:** Usa Pandas para filtrar y calcular el Top 5 de sensores más congestionados.
3. **Agente Auditor:** Evalúa el código y calcula la distancia geográfica al centro de Madrid para detectar sesgos.

### 📊 Resultados Principales (Auditoría Ética)
El sistema identificó 5 sensores críticos en horario valle: `[17726, 64717, 59088, 10923, 13675]`.
Al cruzar estas coordenadas geográficas, la distancia media al centro (Puerta del Sol) fue de **4.08 km**, con 4 de los 5 sensores en el núcleo urbano.

> **Veredicto:** Se activó una **ALERTA ÉTICA (Efecto Lámpara)**. El modelo demuestra un sesgo hacia el centro de la ciudad debido a la densidad de sensores, ignorando la periferia. Se recomienda un 
muestreo estratificado.

---

## 🌐 2. Agente Prescriptivo con OSMnx (Simulación de Cierres)
Este notebook implementa un Agente de IA que combina la topología real de las calles de Madrid (descargada de OpenStreetMap mediante `OSMnx`) con la capacidad de DuckDB para consultar un dataset de 
10 GB sin colapsar la memoria.

### Características:
*   Calcula rutas alternativas topológicas reales si una calle se cierra (usando `NetworkX`).
*   Evalúa el tráfico histórico real de la calle cerrada y de las alternativas.
*   Es consciente de sus limitaciones: si no hay sensores en la calle alternativa, el agente lo reporta en lugar de inventar datos.

---

## 🧠 3. Graph Neural Networks (GNN) para Predicción Espacio-Temporal
Para superar las limitaciones de los modelos de series temporales tradicionales (como SARIMA), este notebook implementa una Red Neuronal de Grafos (GCN) con PyTorch Geometric.

### ¿Qué hace?
*   Construye un grafo KNN (K-Nearest Neighbors) basado en las coordenadas UTM de los sensores de Madrid.
*   Utiliza capas `GCNConv` para propagar la información de tráfico entre sensores vecinos.
*   Combina la topología espacial con una ventana temporal deslizante para predecir la congestión de los próximos intervalos de 15 minutos.

---

## 🚦 4. Control Semafórico Adaptativo con Reinforcement Learning (RL)
Este notebook explora el uso de **Aprendizaje por Refuerzo Profundo (PPO)** para resolver el problema clásico de la ingeniería de tráfico: la optimización de ciclos semafóricos.

### Hitos del Proyecto:
*   **Simulación de Entorno (Gymnasium):** Se creó un entorno personalizado que simula un corredor de dos intersecciones, con flujos de llegada de vehículos estocásticos (distribución de Poisson) y 
tiempo de entreverde (amarillo).
*   **Optimización del Ciclo Completo:** El agente aprendió a seleccionar la duración óptima del ciclo (entre 40s y 120s) para minimizar el tiempo de espera total.
*   **Creación de Ondas Verdes:** Al incorporar el estado del semáforo aguas abajo en las observaciones, el agente aprendió a sincronizar su fase verde con la intersección inferior (creando un 
*Offset* dinámico).
*   **Mitigación del Reward Hacking:** Se corrigió la función de recompensa para evitar que el agente eligiera ciclos cortos solo para terminar el episodio rápido, forzándolo a encontrar un 
equilibrio sostenible (convergiendo en un ciclo óptimo de 100 segundos).

---

## 🛠️ Requisitos e Instalación

Para ejecutar estos notebooks, necesitas una cuenta de Google (para Colab y Drive) y una API Key de OpenAI (para los agentes).

1. Clona este repositorio:
   ```bash
   git clone https://github.com/malborno2020/proyecto-semaforos-madrid.git
   cd proyecto-semaforos-madrid
   ```

2. Instala las dependencias generales:
   ```bash
   pip install -r requirements.txt
   ```
   *(Asegúrate de tener un archivo `requirements.txt` con: `crewai`, `crewai-tools`, `mcp`, `pandas`, `numpy`, `h5py`, `requests`, `langchain-openai`, `duckdb`, `osmnx`, `networkx`, `torch`, 
`torch_geometric`, `gymnasium`, `stable-baselines3`)*

3. Configura tu API Key de OpenAI como variable de entorno (solo para los notebooks de agentes):
   ```bash
   export OPENAI_API_KEY="tu-clave-aqui"
   ```

## 🚀 Cómo Ejecutar

1. Abre cualquiera de los archivos `.ipynb` en Jupyter Notebook o Google Colab.
2. Ejecuta las celdas en orden secuencial.
3. **Nota sobre los datos:** Los notebooks están diseñados para descargar automáticamente los datasets necesarios (Zenodo / OpenStreetMap) o buscarlos en tu Google Drive si los has montado 
previamente.

## ⚖️ Manifiesto Ético
1. **Transparencia Geográfica:** Todo modelo predictivo de tráfico debe reportar sus recomendaciones desagregadas por distritos (Centro vs. Periferia).
2. **Human-in-the-Loop:** Ningún ajuste semafórico será automatizado sin la validación de un ingeniero humano.
3. **Privacidad:** Los datos de GPS de vehículos utilizados para el entrenamiento serán anonimizados en todo momento.

---
*Este proyecto fue desarrollado como parte del curso "Data Analytics for Urban Systems" (2026).*

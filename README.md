# 🚦 Agente Multi-Agente para la Optimización Semafórica en Madrid

**Curso:** Data Analytics for Urban Systems: From Co-Pilot to Autonomous Agents  
**Módulo:** 4 — Proyecto Final  
**Autor:** Manuel A. Albornoz

## 📝 Descripción del Proyecto
Este proyecto implementa un sistema de **Inteligencia Artificial Multi-Agente** diseñado para identificar intersecciones (semáforos) en la ciudad de Madrid que requieren un ajuste en su programación. 

A diferencia de los análisis tradicionales que buscan las horas pico, este agente busca sensores con **congestión anormalmente alta en horario valle (10:00 a 16:00)**. Si un semáforo está colapsado a media mañana, es un candidato claro a una re-sincronización de sus ciclos.

Además, el sistema incorpora una **capa de Auditoría Ética** para detectar si las recomendaciones de la IA están sesgadas geográficamente (Efecto Lámpara).

## 🏗️ Arquitectura del Sistema

El sistema está construido sobre tres pilares:

1. **Servidor MCP (Model Context Protocol):** Un servidor local (`mcp_server.py`) que expone herramientas para consultar el esquema del dataset de tráfico de Madrid.
2. **Agente Analista (Ingeniero de Tráfico):** Usa código Python (Pandas) para filtrar el dataset, extraer la hora, filtrar la franja de 10:00 a 16:00 y calcular el Top 5 de sensores más congestionados.
3. **Agente Auditor (Planificador Urbano):** Revisa el trabajo del analista. Evalúa la lógica del código y calcula la distancia geográfica de los semáforos al centro de Madrid para detectar sesgos de equidad.

## 🛠️ Requisitos e Instalación

Para ejecutar este proyecto, necesitas una cuenta de Google (para Colab y Drive) y una API Key de OpenAI.

1. Clona este repositorio:
   ```bash
   git clone https://github.com/malborno2020/proyecto-semaforos-madrid.git
   cd proyecto-semaforos-madrid

2. Instala las dependencias:
   ```bash
    pip install -r requirements.txt

   (Asegúrate de tener un archivo requirements.txt con: crewai, crewai-tools, mcp, pandas, numpy, h5py, requests, langchain-openai)

3.Configura tu API Key de OpenAI como variable de entorno:
   ```bash
      export OPENAI_API_KEY="tu-clave-aqui"
   ```

## 🚀 Cómo Ejecutar el Proyecto

   1. Abre el archivo main.ipynb en Jupyter Notebook o Google Colab.

   2. Ejecuta las celdas en orden secuencial:

        Celdas 1-3: Configuración del entorno y montaje de Google Drive.

        Celda 5: Inicia el servidor MCP en segundo plano.

        Celdas 7-9: Define y orquesta a los agentes (Analista y Auditor).

        Celda 11: Ejecuta el Crew (la conversación entre agentes).

        Celda 13: Ejecuta la auditoría ética final (cálculo de sesgo geográfico).

## 📊 Resultados Principales (Auditoría Ética)

El sistema identificó los 5 sensores más congestionados en horario valle:
sensor_id: [17726, 64717, 59088, 10923, 13675]

Al cruzar estas coordenadas con el mapa de Madrid, el sistema calculó una distancia media al centro (Puerta del Sol) de 4.08 km. Cuatro de los cinco sensores estaban en el núcleo urbano.

Veredicto: Se activó una ALERTA ÉTICA (Efecto Lámpara). El modelo demuestra un sesgo hacia el centro de la ciudad debido a la mayor densidad de sensores en esa zona, ignorando la periferia. Se recomienda aplicar un muestreo estratificado para futuras iteraciones.

## ⚖️ Manifiesto Ético

Transparencia Geográfica: Todo modelo predictivo de tráfico debe reportar su error y sus recomendaciones desagregadas por distritos (Centro vs. Periferia).

Human-in-the-Loop: Ningún ajuste semafórico será automatizado sin la validación de un ingeniero humano.

Privacidad: Los datos de GPS de vehículos utilizados para el entrenamiento serán anonimizados en todo momento.

Este proyecto fue desarrollado como parte del curso "Data Analytics for Urban Systems" (2026).

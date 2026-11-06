{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "provenance": [],
      "toc_visible": true
    },
    "kernelspec": {
      "name": "python3",
      "display_name": "Python 3"
    },
    "language_info": {
      "name": "python"
    }
  },
  "cells": [
    {
      "cell_type": "markdown",
      "source": [
        "# 🚦 Agente Multi-Agente para la Optimización Semafórica en Madrid\n",
        "\n",
        "**Curso:** Data Analytics for Urban Systems: From Co-Pilot to Autonomous Agents\n",
        "**Módulo:** 4 — Proyecto Final\n",
        "**Autor:** Manuel A. Albornoz\n",
        "\n",
        "## 📝 Descripción del Proyecto\n",
        "Este proyecto implementa un sistema de **Inteligencia Artificial Multi-Agente** diseñado para identificar intersecciones (semáforos) en la ciudad de Madrid que requieren un ajuste en su programación.\n",
        "\n",
        "A diferencia de los análisis tradicionales que buscan las horas pico, este agente busca sensores con **congestión anormalmente alta en horario valle (10:00 a 16:00)**. Si un semáforo está colapsado a media mañana, es un candidato claro a una re-sincronización de sus ciclos.\n",
        "\n",
        "Además, el sistema incorpora una **capa de Auditoría Ética** para detectar si las recomendaciones de la IA están sesgadas geográficamente (Efecto Lámpara).\n",
        "\n",
        "## 🏗️ Arquitectura del Sistema\n",
        "\n",
        "El sistema está construido sobre tres pilares:\n",
        "\n",
        "1. **Servidor MCP (Model Context Protocol):** Un servidor local (`mcp_server.py`) que expone herramientas para consultar el esquema del dataset de tráfico de Madrid.\n",
        "2. **Agente Analista (Ingeniero de Tráfico):** Usa código Python (Pandas) para filtrar el dataset, extraer la hora, filtrar la franja de 10:00 a 16:00 y calcular el Top 5 de sensores más congestionados.\n",
        "3. **Agente Auditor (Planificador Urbano):** Revisa el trabajo del analista. Evalúa la lógica del código y calcula la distancia geográfica de los semáforos al centro de Madrid para detectar sesgos de equidad.\n",
        "\n",
        "## 🛠️ Requisitos e Instalación\n",
        "\n",
        "Para ejecutar este proyecto, necesitas una cuenta de Google (para Colab y Drive) y una API Key de OpenAI.\n",
        "\n",
        "1. Clona este repositorio:\n",
        "   ```bash\n",
        "   git clone https://github.com/TU_USUARIO/proyecto-semaforos-madrid.git\n",
        "   cd proyecto-semaforos-madrid\n",
        "   \n",
        "2.  Instala las dependencias:\n",
        "    bash\n",
        "\n",
        "    pip install -r requirements.txt\n",
        "\n",
        "    (Crea un archivo requirements.txt con: crewai, crewai-tools, mcp, pandas, numpy, h5py, requests, langchain-openai)\n",
        "\n",
        "3.  Configura tu API Key de OpenAI como variable de entorno:\n",
        "    bash\n",
        "\n",
        "    export OPENAI_API_KEY=\"tu-clave-aqui\"\n",
        "\n",
        "#🚀 Cómo Ejecutar el Proyecto\n",
        "\n",
        "1.    Abre el archivo main.ipynb en Jupyter Notebook o Google Colab.\n",
        "\n",
        "2.    Ejecuta las celdas en orden secuencial:\n",
        "\n",
        "        Celda 1-3: Configuración del entorno y montaje de Google Drive.\n",
        "\n",
        "        Celda 5: Inicia el servidor MCP en segundo plano.\n",
        "\n",
        "        Celda 7-9: Define y orquesta a los agentes (Analista y Auditor).\n",
        "\n",
        "        Celda 11: Ejecuta el Crew (la conversación entre agentes).\n",
        "\n",
        "        Celda 13: Ejecuta la auditoría ética final (cálculo de sesgo geográfico).\n",
        "\n",
        "#📊 Resultados Principales (Auditoría Ética)\n",
        "\n",
        "El sistema identificó los 5 sensores más congestionados en horario valle:\n",
        "sensor_id: [17726, 64717, 59088, 10923, 13675]\n",
        "\n",
        "Al cruzar estas coordenadas con el mapa de Madrid, el sistema calculó una distancia media al centro (Puerta del Sol) de 4.08 km. Cuatro de los cinco sensores estaban en el núcleo urbano.\n",
        "\n",
        "Veredicto: Se activó una ALERTA ÉTICA (Efecto Lámpara). El modelo demuestra un sesgo hacia el centro de la ciudad debido a la mayor densidad de sensores en esa zona, ignorando la periferia. Se recomienda aplicar un muestreo estratificado para futuras iteraciones.\n",
        "\n",
        "#⚖️ Manifiesto Ético\n",
        "\n",
        "1.    Transparencia Geográfica: Todo modelo predictivo de tráfico debe reportar su error y sus recomendaciones desagregadas por distritos (Centro vs. Periferia).\n",
        "\n",
        "2.    Human-in-the-Loop: Ningún ajuste semafórico será automatizado sin la validación de un ingeniero humano.\n",
        "\n",
        "3.    Privacidad: Los datos de GPS de vehículos utilizados para el entrenamiento serán anonimizados en todo momento.\n",
        "\n",
        "Este proyecto fue desarrollado como parte del curso \"Data Analytics for Urban Systems\" (2026)."
      ],
      "metadata": {
        "id": "q119F83UFaa6"
      }
    },
    {
      "cell_type": "code",
      "source": [],
      "metadata": {
        "id": "Ewmah9vZG_iA"
      },
      "execution_count": null,
      "outputs": []
    }
  ]
}# proyecto-semaforos-madrid

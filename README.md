# AI-Powered-Personal-Knowledge-System

Sistema personal de estudio y gestión de conocimiento basado en IA local utilizando Ollama, Qwen 2.5, Memorwise y Obsidian.

---

## Descripción

Este proyecto implementa un entorno de aprendizaje asistido por inteligencia artificial que funciona completamente de manera local, sin depender de servicios externos o APIs de pago.

El objetivo es centralizar documentos, notas y recursos de estudio para realizar consultas inteligentes utilizando modelos LLM ejecutados localmente.

### Características

- Ejecución local mediante Ollama.
- Integración con modelos Qwen 2.5.
- Gestión de conocimiento mediante Memorwise.
- Consulta de documentos PDF.
- Recuperación contextual mediante embeddings (RAG).
- Organización de notas en Obsidian.
- Despliegue mediante Docker y Docker Compose.
- Persistencia local de datos.

---

## Arquitectura

```text
PDFs / Recursos
        │
        ▼

   Memorwise
        │

 Embeddings / RAG
        │

        ▼

    Qwen 2.5
     (Ollama)

        ▼

 Respuestas IA

        ▼

    Obsidian
```

---

## Estructura del Proyecto

```text
AI-Hub/
│
├── docker-compose.yml
│
└── Memorwise/
    ├── Dockerfile
    ├── package.json
    ├── package-lock.json
    └── ...
```

---

## Tecnologías Utilizadas

- Docker
- Docker Compose
- Node.js
- SQLite
- Ollama
- Qwen 2.5
- Memorwise
- Obsidian

---

## Requisitos Previos

- Docker Desktop
- Ollama
- Git
- Windows, Linux o macOS

---

# Instalación

## 1. Instalar Ollama

Descargar Ollama:

https://ollama.com/download

Verificar instalación:

```bash
ollama --version
```

Iniciar el servicio:

```bash
ollama serve
```

---

## 2. Descargar un Modelo

### Recomendado

```bash
ollama pull qwen2.5:7b
```

### Opciones disponibles

| Modelo | Recomendación |
|----------|----------|
| qwen2.5:3b | Equipos modestos |
| qwen2.5:7b | Recomendado |
| qwen2.5:14b | Mejor calidad |
| llama3.1:8b | Alternativa equilibrada |

Probar el modelo:

```bash
ollama run qwen2.5:7b
```

---

## 3. Clonar el Proyecto

```bash
git clone <URL_DEL_REPOSITORIO>
```

Entrar al proyecto:

```bash
cd AI-Hub
```

---

## 4. Construir y Levantar Docker

Desde la raíz del proyecto:

```bash
docker compose up -d --build
```

Verificar contenedores:

```bash
docker ps
```

Debería aparecer:

```text
memorwise
```

---

## 5. Acceder a la Aplicación

Abrir:

```text
http://localhost:4747
```

---

# Docker Compose

El proyecto utiliza la siguiente configuración:

```yaml
services:
  memorwise:
    build:
      context: ./Memorwise
    container_name: memorwise
    ports:
      - "4747:4747"
    environment:
      - CUDA_VISIBLE_DEVICES=-1
      - ORT_DISABLE_CUDA=1
    restart: always

volumes:
  open-webui:
```

---

# Dockerfile

```dockerfile
FROM node:20

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

RUN npm rebuild better-sqlite3

EXPOSE 4747

CMD ["npm","run","dev"]
```

---

# Flujo de Trabajo

### 1. Iniciar Ollama

```bash
ollama serve
```

### 2. Levantar Memorwise

```bash
docker compose up -d
```

### 3. Importar PDFs

Agregar documentos de estudio para indexación.

### 4. Consultar Información

Ejemplos:

```text
Resume este documento.
```

```text
¿Cuáles son los conceptos principales?
```

```text
¿Qué explica el capítulo 4?
```

### 5. Guardar Conocimiento

Organizar resúmenes y apuntes dentro de Obsidian.

---

# Integración con Obsidian

Ejemplo de estructura de notas:

```text
Vault/
│
├── Backend
├── IA
├── Inglés
├── Arquitectura
└── DevOps
```

Plantilla sugerida:

```markdown
# Tema

## Resumen

## Conceptos Clave

## Ejemplos

## Preguntas

## Recursos
```

---

# Casos de Uso

- Estudio de cursos técnicos.
- Consulta de documentación.
- Análisis de PDFs.
- Gestión de conocimiento personal.
- Creación de resúmenes automáticos.
- Organización de apuntes en Obsidian.

---

# Modelos Recomendados

## Equipos con pocos recursos

```bash
ollama pull qwen2.5:3b
```

## Mejor equilibrio calidad/rendimiento

```bash
ollama pull qwen2.5:7b
```

## Mayor calidad

```bash
ollama pull qwen2.5:14b
```

---

# Autor

Proyecto personal desarrollado para explorar IA local, recuperación de conocimiento (RAG), gestión documental y productividad académica utilizando herramientas open source.

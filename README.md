# 🧠 MindVault

> **Tu cerebro externo, completamente local.**  
> Sistema de gestión del conocimiento con IA, RAG y búsqueda semántica — sin APIs de pago, sin datos en la nube.

---

## ¿Qué es MindVault?

MindVault es un entorno de estudio y gestión del conocimiento que combina **modelos de lenguaje locales** (LLMs) con **recuperación aumentada por contexto** (RAG) para que puedas conversar con tus propios documentos, notas y recursos — todo desde tu máquina, sin conexión a servicios externos.

Importas tus PDFs, haces preguntas en lenguaje natural, y obtienes respuestas precisas basadas en tu propio conocimiento. Los resúmenes y apuntes se organizan en Obsidian.

---

## ✨ Características

- 🏠 **100% local** — ningún dato sale de tu máquina
- 🔍 **RAG con embeddings semánticos** — busca por significado, no por palabras clave
- 📄 **Consulta de PDFs** — interroga tus libros y documentos técnicos
- 🤖 **Powered by Qwen 2.5 vía Ollama** — modelos open-source de alta calidad
- 📝 **Integración con Obsidian** — organiza el conocimiento en tu vault personal
- 🐳 **Despliegue con Docker** — un solo comando para levantar todo
- 💾 **Persistencia local** — tus datos quedan en tu disco, siempre

---

## 🏗️ Arquitectura

```
┌─────────────────────────────────────────────┐
│                  Tus Recursos                │
│         PDFs · Notas · Documentación         │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│                  Memorwise                   │
│         Indexación + Embeddings + RAG        │
│              (SQLite · Node.js)              │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│              Ollama · Qwen 2.5               │
│         Inferencia LLM completamente         │
│                    local                     │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│                  Obsidian                    │
│        Vault personal de conocimiento        │
└─────────────────────────────────────────────┘
```

---

## 🗂️ Estructura del proyecto

```
mindvault/
│
├── docker-compose.yml       # Orquestación de servicios
│
└── Memorwise/               # Motor RAG
    ├── Dockerfile
    ├── package.json
    ├── package-lock.json
    └── ...
```

---

## 🧰 Stack tecnológico

| Componente     | Tecnología                    |
|----------------|-------------------------------|
| Runtime local  | [Ollama](https://ollama.com)  |
| Modelo LLM     | Qwen 2.5 (3b / 7b / 14b)     |
| Motor RAG      | Memorwise                     |
| Base de datos  | SQLite                        |
| Backend        | Node.js                       |
| Contenedores   | Docker + Docker Compose       |
| Notas          | Obsidian                      |

---

## ⚙️ Requisitos previos

- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [Ollama](https://ollama.com/download)
- [Git](https://git-scm.com/)
- [Obsidian](https://obsidian.md/) *(opcional, para organizar notas)*
- Sistema operativo: Windows, macOS o Linux

---

## 🚀 Instalación

### 1. Instalar y levantar Ollama

```bash
# Descargar desde https://ollama.com/download
ollama serve
```

### 2. Descargar un modelo

Elige según los recursos de tu equipo:

| Modelo         | VRAM recomendada | Ideal para               |
|----------------|------------------|--------------------------|
| `qwen2.5:3b`   | ~4 GB            | Equipos modestos         |
| `qwen2.5:7b`   | ~8 GB            | ⭐ Recomendado           |
| `qwen2.5:14b`  | ~16 GB           | Mayor calidad de respuesta |
| `llama3.1:8b`  | ~8 GB            | Alternativa en inglés    |

```bash
ollama pull qwen2.5:7b
```

### 3. Clonar el repositorio

```bash
git clone https://github.com/CristhAXe/AI-Powered-Personal-Knowledge-System.git mindvault
cd mindvault
```

### 4. Levantar los servicios

```bash
docker compose up -d --build
```

Verifica que el contenedor esté corriendo:

```bash
docker ps
```

### 5. Abrir la aplicación

```
http://localhost:4747
```

---

## 📋 Flujo de uso

```
1. ollama serve              → Levantar el motor LLM
2. docker compose up -d      → Levantar Memorwise
3. Importar PDFs             → Indexar documentos
4. Hacer consultas           → Chatear con tu conocimiento
5. Guardar en Obsidian       → Construir tu base de conocimiento
```

**Ejemplos de consultas:**

```
Resume este documento.
¿Cuáles son los conceptos principales del capítulo 3?
¿Qué diferencias hay entre X e Y según mis notas?
Genera un quiz sobre este tema.
```

---

## 📚 Integración con Obsidian

Estructura de vault sugerida:

```
Vault/
├── Backend/
├── IA/
├── Inglés/
├── Arquitectura/
└── DevOps/
```

**Plantilla de nota recomendada:**

```markdown
# Tema

## Resumen IA
<!-- Pegar respuesta de MindVault -->

## Conceptos Clave

## Ejemplos Prácticos

## Preguntas de Repaso

## Recursos
```

---

## 🐳 Configuración Docker

```yaml
# docker-compose.yml
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

## 💡 Casos de uso

- 📖 Estudiar cursos técnicos interrogando el material directamente
- 🔍 Buscar conceptos en tu documentación personal
- 📊 Analizar y resumir PDFs extensos
- 🗃️ Construir una base de conocimiento personal acumulativa
- ✍️ Generar resúmenes y notas de estudio automáticamente
- 🧪 Crear preguntas de repaso sobre cualquier tema

---

## 🛣️ Roadmap

- [ ] Soporte multi-modelo (cambiar modelo desde la UI)
- [ ] Ingesta de URLs y páginas web
- [ ] Exportación directa a Obsidian
- [ ] Soporte para imágenes (modelos multimodales)
- [ ] API REST para integración con otras herramientas

---

## 👤 Autor

Proyecto personal de **CristhAXe** — explorando el potencial de la IA local, RAG y la gestión del conocimiento con herramientas open source.

---

## 📄 Licencia

MIT — libre para usar, modificar y distribuir.

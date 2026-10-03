# test-simple-stock-flow-infra

> **Prueba Técnica SDD · Ficha ADSO 3413974**  
> **Aprendiz:** Paula Claros ([`paulaclaros`](https://github.com/paulaclaros))  
> **Tecnología:** Docker Compose (Motor de BD relacional, API Laravel, Frontend React/Nginx)  
> **Fecha:** 2026-10-03  

---

## 📌 1. Descripción de la Infraestructura

Este repositorio orquesta todos los contenedores y redes necesarios para desplegar *Simple Stock Flow* en cualquier entorno sin requerir software instalado en la máquina anfitriona (ADR-010).

### Componentes de la Arquitectura en Contenedores:
1. **`db` (Motor de Persistencia):**
   - Motor relacional (PostgreSQL / MySQL) con esquema limpio.
   - Las migraciones son propiedad exclusiva del contenedor de la API (ADR-001).
2. **`api` (Backend Laravel):**
   - Servidor PHP 8.2 FPM / Artisan para procesar solicitudes HTTP en el puerto `:8000`.
   - Aplica automáticamente las migraciones y seeders al arrancar.
3. **`app` (Frontend React):**
   - Servidor Nginx que distribuye la SPA construida con Vite en el puerto `:8080`.
   - Actúa como reverse proxy redirigiendo el tráfico `/api/*` y `/media/*` hacia el contenedor `api`.

---

## 🚀 2. Guía de Ejecución

### Requisitos Previos
* Docker y Docker Compose instalados.

### Paso a Paso para Despliegue:
```bash
# 1. Copiar archivo de entorno
cp .env.example .env

# 2. Levantar los servicios en segundo plano
docker compose up -d --build

# 3. Comprobar estado de los contenedores
docker compose ps
```

### Puntos de Acceso:
* **Aplicación Web:** [http://localhost:8080](http://localhost:8080)
* **API REST:** [http://localhost:8000](http://localhost:8000)
* **Verificación de Salud:** [http://localhost:8000/health](http://localhost:8000/health)

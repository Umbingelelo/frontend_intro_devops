# frontend_intro_devops

Aplicación web SPA construida con **Angular 17** para gestión de tareas.
Forma parte de la asignatura **Introducción a Herramientas DevOps (ISY1101)**.

---

## Stack

- Angular 17 (standalone components)
- TypeScript
- Imagen Docker base: `node:20-alpine` con `ng serve`

---

## Estructura

```
frontend_intro_devops/
├── src/
│   ├── app/
│   │   ├── app.component.ts    ← componente principal + template inline
│   │   └── services/
│   │       └── tareas.service.ts  ← HTTP client hacia la API
│   ├── index.html
│   ├── main.ts
│   └── styles.css
├── Dockerfile
├── .dockerignore
├── angular.json
├── package.json
├── tsconfig.json
└── tsconfig.app.json
```

---

## Configuración del backend

La URL de la API está definida en `src/app/services/tareas.service.ts`:

```typescript
readonly baseUrl = 'http://localhost:3000';
```

> **Importante:** Angular es una SPA que corre en el **navegador del usuario**.
> Si el backend está en un servidor remoto (ej. EC2), cambia `localhost`
> por la IP o dominio del backend antes de construir la imagen.

---

## Cómo correr en local

### Sin Docker

```bash
npm install
npm start
# App disponible en http://localhost:4200
```

### Con Docker

```bash
# Construir imagen
docker build -t tareas-frontend:1.0 .

# Correr contenedor
docker run -d \
  --name tareas-frontend \
  -p 4200:4200 \
  tareas-frontend:1.0
```

> El servidor de desarrollo (`ng serve`) tarda ~2 min en compilar la primera vez.
> Sigue el progreso con: `docker logs -f tareas-frontend`

---

## Uso en las experiencias del curso

Este repositorio es el código base que se usa en las actividades prácticas.

| Experiencia | Qué se trabaja |
|---|---|
| Experiencia 2 – Docker en local | Build de imagen, `docker run`, bind mount, hot-reload, Docker Compose |
| Experiencia 3 – ECR + EC2 | Rebuild con URL del backend EC2, push a Amazon ECR, despliegue en EC2 |

Repositorio de ejercicios: [ejercicios-intro-herramientas-devops](https://github.com/Umbingelelo/ejercicios-intro-herramientas-devops)

---

## Repositorio del backend

[https://github.com/Umbingelelo/backend_intro_devops](https://github.com/Umbingelelo/backend_intro_devops)

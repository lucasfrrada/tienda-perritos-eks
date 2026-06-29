# Frontend

Frontend web estático para la gestión CRUD de productos de la tienda. Se sirve con Nginx y consume la API del backend mediante la ruta `/api/productos`.

## Archivos principales

- `index.html`: interfaz principal de la aplicación.
- `app.js`: lógica del CRUD y llamadas HTTP al backend.
- `default.conf`: configuración de Nginx, incluyendo proxy de `/api/` hacia `tienda-backend:3001`.
- `Dockerfile`: imagen basada en `nginx:alpine`.

## Construir imagen Docker

Desde esta carpeta:

```bash
docker build -t tienda-frontend .
```

## Ejecutar localmente con Docker

```bash
docker run --name tienda-frontend -p 8080:80 tienda-frontend
```

La aplicación queda disponible en `http://localhost:8080`. Para que el CRUD funcione localmente, el proxy de Nginx debe poder resolver el backend como `tienda-backend:3001`.

## Despliegue en EKS

En Kubernetes se despliega como `Deployment` con nombre `tienda-frontend`, contenedor `frontend` y puerto `80`. El servicio `tienda-frontend` es de tipo `LoadBalancer` para exponer la aplicación.

## Manifiestos relacionados

- `k8s/frontend-deployment.yaml`
- `k8s/frontend-service.yaml`
- `k8s/frontend-hpa.yaml`

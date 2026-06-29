# TIENDA-PERRITOS-EKS

Sistema CRUD simple para gestionar productos de una tienda de alimentos para perritos. El proyecto incluye frontend, backend, base de datos MySQL, contenedores Docker, manifiestos Kubernetes para AWS EKS, autoscaling con HPA y pipeline CI/CD con GitHub Actions.

## Arquitectura

```text
Usuario
  ↓
Frontend / Nginx
  ↓
Backend / Node.js
  ↓
MySQL
```

## Tecnologías utilizadas

- Docker
- Kubernetes
- AWS EKS
- Amazon ECR
- GitHub Actions
- Node.js
- Nginx
- MySQL

## Estructura del repositorio

```text
TIENDA-PERRITOS-EKS/
├── .github/
│   └── workflows/
│       └── deploy-eks.yml
├── backend/
├── db/
├── frontend/
├── k8s/
└── README.md
```

## Carpetas principales

- `frontend/`: aplicación web estática servida con Nginx. Consume la API mediante `/api/productos`.
- `backend/`: API Node.js con Express para el CRUD de productos y conexión a MySQL.
- `db/`: imagen MySQL 8 con script de inicialización de base de datos.
- `k8s/`: manifiestos Kubernetes para namespace, deployments, services, secrets y HPA.
- `.github/workflows/`: pipeline CI/CD para construir imágenes, subirlas a Amazon ECR y desplegar en AWS EKS.

## CI/CD

El workflow `.github/workflows/deploy-eks.yml` se ejecuta al hacer push a la rama `main` o manualmente con `workflow_dispatch`.

Flujo general:

```text
Commit
→ Build Docker
→ Push a ECR
→ Deploy en EKS
```

El pipeline construye las imágenes `tienda-frontend`, `tienda-backend` y `tienda-db`, hace login en Amazon ECR, sube las imágenes con un tag basado en el commit y actualiza los deployments en EKS. Usa GitHub Secrets para credenciales y configuración de AWS/EKS, como región, cluster, namespace y credenciales AWS.

## Comandos útiles

```bash
kubectl get pods -n tienda
kubectl get svc -n tienda
kubectl get hpa -n tienda
kubectl logs -l app=tienda-backend -n tienda -c backend
```

## Evidencias sugeridas

- Clúster EKS activo.
- Imágenes en ECR.
- Pipeline GitHub Actions exitoso.
- Pods en estado `Running`.
- Services activos.
- HPA configurado.
- Frontend funcionando.
- Logs del backend.
- Comunicación Frontend → Backend → MySQL.

## Conclusión

`TIENDA-PERRITOS-EKS` implementa un flujo completo de aplicación contenedorizada con frontend, backend, MySQL, despliegue en Kubernetes sobre AWS EKS, publicación de imágenes en Amazon ECR y automatización CI/CD con GitHub Actions.

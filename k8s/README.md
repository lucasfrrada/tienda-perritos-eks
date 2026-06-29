# Kubernetes

Esta carpeta contiene los manifiestos Kubernetes para desplegar la aplicación completa en el namespace `tienda`.

## Manifiestos

- `namespace.yaml`: crea el namespace `tienda`.
- `mysql-secret.yaml`: secret usado por MySQL para credenciales. No documentar valores sensibles.
- `mysql-deployment.yaml`: despliega MySQL como `tienda-db` en el puerto `3306`.
- `mysql-service.yaml`: expone MySQL internamente como servicio `tienda-db`.
- `backend-deployment.yaml`: despliega el backend `tienda-backend` en el puerto `3001`.
- `backend-service.yaml`: expone el backend internamente como servicio `tienda-backend`.
- `backend-hpa.yaml`: autoscaling del backend entre 2 y 10 réplicas según CPU.
- `frontend-deployment.yaml`: despliega el frontend `tienda-frontend` en el puerto `80`.
- `frontend-service.yaml`: expone el frontend con un servicio `LoadBalancer`.
- `frontend-hpa.yaml`: autoscaling del frontend entre 2 y 6 réplicas según CPU.

## Orden recomendado de despliegue

```bash
kubectl apply -f namespace.yaml
kubectl apply -f mysql-secret.yaml
kubectl apply -f mysql-deployment.yaml
kubectl apply -f mysql-service.yaml
kubectl apply -f backend-deployment.yaml
kubectl apply -f backend-service.yaml
kubectl apply -f backend-hpa.yaml
kubectl apply -f frontend-deployment.yaml
kubectl apply -f frontend-service.yaml
kubectl apply -f frontend-hpa.yaml
```

## Comando general

Desde la raíz del repositorio:

```bash
kubectl apply -f k8s/
```

## Validación

```bash
kubectl get all -n tienda
kubectl get hpa -n tienda
kubectl get svc -n tienda
kubectl get pods -n tienda
```

Para revisar logs del backend:

```bash
kubectl logs -l app=tienda-backend -n tienda -c backend
```

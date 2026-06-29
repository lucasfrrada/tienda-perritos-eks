# Backend

API backend para la tienda de alimentos para perritos. Expone endpoints REST para listar, crear, actualizar y eliminar productos, además de un endpoint de salud para Kubernetes.

## Tecnologías y dependencias

Detectado en `package.json`:

- Node.js
- Express
- CORS
- mysql2

Script principal:

```bash
npm start
```

## Puerto

El backend usa el puerto `3001` por defecto. También puede configurarse con la variable de entorno `PORT`.

## Variables de entorno

Detectadas en `server.js` y `backend-deployment.yaml`:

- `PORT`: puerto HTTP del backend.
- `DB_HOST`: host del servicio MySQL, configurado como `tienda-db` en Kubernetes.
- `DB_USER`: usuario de conexión a MySQL.
- `DB_PASSWORD`: contraseña de MySQL, obtenida desde `mysql-secret` en Kubernetes.
- `DB_NAME`: base de datos, configurada como `tienda_perritos`.
- `DB_PORT`: puerto MySQL, configurado como `3306`.

No se documentan valores sensibles de secrets.

## Instalar dependencias

Desde esta carpeta:

```bash
npm install
```

## Ejecutar localmente

```bash
npm start
```

Para probar los endpoints con datos reales, debe existir una instancia MySQL accesible con las variables de entorno anteriores.

## Construir imagen Docker

```bash
docker build -t tienda-backend .
```

## Despliegue en EKS

En Kubernetes se despliega como `Deployment` con nombre `tienda-backend`, contenedor `backend`, puerto `3001`, probes en `/api/health` y variables de entorno para conectar con MySQL.

## Manifiestos relacionados

- `k8s/backend-deployment.yaml`
- `k8s/backend-service.yaml`
- `k8s/backend-hpa.yaml`

## Logs

```bash
kubectl logs -l app=tienda-backend -n tienda -c backend
```

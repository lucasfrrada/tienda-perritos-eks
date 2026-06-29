# Base de datos

Esta carpeta contiene la configuración de la base de datos MySQL usada por la aplicación.

## Archivos principales

- `Dockerfile`: imagen basada en `mysql:8`.
- `init.sql`: script de inicialización ejecutado al crear la base por primera vez.

## Inicialización

`init.sql` crea la base de datos `tienda_perritos` y la tabla `productos`.

La tabla `productos` contiene:

- `id`
- `nombre`
- `descripcion`
- `precio`
- `stock`

También inserta productos iniciales de alimentos y snacks para perritos.

## Construir imagen Docker

Desde esta carpeta:

```bash
docker build -t tienda-db .
```

## Uso en Kubernetes

Kubernetes despliega MySQL como `Deployment` con nombre `tienda-db`, contenedor `mysql` y puerto `3306`. La contraseña root se obtiene desde el secret `mysql-secret`.

No se documentan valores sensibles de secrets.

## Manifiestos relacionados

- `k8s/mysql-deployment.yaml`
- `k8s/mysql-service.yaml`
- `k8s/mysql-secret.yaml`

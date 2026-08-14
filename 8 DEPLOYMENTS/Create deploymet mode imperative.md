# Deployment de modo imperativo
```
kubectl create deployment apache --image=http
```

Con el deployment se crean
- deployment
- replicaset
- pod

## Comprobar el despliegue
```
kubectl get deploy
```

Cual es la diferencia entre READY Y AVAILABLE?
## Comprobar replicaset
```
kubectl get rs
```

## Comprobar pods
```
kubectl get pods
```

El nombre del **pod** esta representado por el nombre del **deployment**, el **replicaset** y por ultimo en nombre del **pod**.


## Crear un pod NGINX
```
kubectl run nginx1 --image=nginx
```
Lo que estamos haciendo es crear un **pod** con la imagen de **nginx**

## Comprobar el estado del POD
```
kubectl get pods
```
Nos muestra los pods creados que estan en ejecucion

## Ver mas caracteristicas del POD
```
kubectl get pods -o wide
```

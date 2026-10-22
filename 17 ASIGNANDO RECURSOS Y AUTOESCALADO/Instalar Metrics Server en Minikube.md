Vamos a ver como recolectar informacion de los **pods** para detectar como estan utilizando: memoria y cpu.
Para poder hacerlo vamos a tener que basarnos en algunas metricas tenemos que determinar el uso de ese contenedor con respecto a la: memoria y cpu.

Repositorio de Metrics Server: github.com/kubernetes/sigs/metrics-server
# Habilitar Metrics Server
## Verificar que recursos tengo para activar
```
minikube addons list
```

```
minikube addons -p cluster1 list
```
## Activar Metrics Server
```
minikube addons enable metrics-server -p cluster1
```
## Verificar que se activo
```
minikube addons list -p cluster1
```
# Obtener las metricas de un pod
Vamos a seleccinar un pod
```
kubectl get pods
```
Con el pod seleccionado vamos a ver que metricas tiene
```
kubectl top pod nginx-d-fsdflsk-sfdsd
```
Vamos a ver los limites que le asignamos a nuestro pod
```
kubectl describe pod nginx-d-fsdflsk-sfdsd
```
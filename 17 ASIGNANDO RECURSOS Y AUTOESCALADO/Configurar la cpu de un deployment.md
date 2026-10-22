Este laboratorio lo realizamos en nuestro minikube.
Vamos a asignar el recurso de CPU. Si dentro del pod hay un solo contenedor este sera el mismo, pero si dentro del pod hay varios contenedores este va ser distinto para cada contenedor.
# Workspace
```
cd /home/jon/Documents/kubernetes/17 ASIGNANDO RECURSOS Y AUTOESCALADO/recursos
```
# Desplegar deploy
```
kubectl apply -f deploy_nginx_cpu.yaml
```
# Ver el estado del deploy
```
kubectl get deploy
```
# Ver el estado de los pods
```
kubectl get pods
```
En este ejempo tenemos corriendo 2 pods y los otros estan en pending, por el motivo que sea no han podido arrancar.
# Ver le estado de las replicas
```
kubectl get rs
```
Por que no se han podido crear los otros pods sera por: memeira, cpu.
# Vamos a ver que tiene uno de esos pods porque no se han creado.
```
kubectl describe pod nginx-d-7373992
```
En la parte inferior en Events vamos a ver el motivo por el cual no se creo el pod, en este ejempo vemos que fue por cpu insuficiente.


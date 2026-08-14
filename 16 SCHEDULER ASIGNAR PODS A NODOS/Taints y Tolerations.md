Es es otra forma de asingar **pods** a **nodos**. Son parecido al Node Selector pero hacen lo contrario.

Cuando coloco un Taint dento de un nodo lo que le digo es que no acepte uno o varios pods, estamos colocando una regla donde dice si un pod no cumple esta condicion no lo va aceptar, no va aceptar que se asocie al nodo.

Los Taints son para los nodos y Tolerations para los pods.
# Laboratorio practico
## Workspace
```
cd /home/jon/Documents/kubernetes/16 SCHEDULER ASIGNAR PODS A NODOS/recurso_taints_tolerations
```

Vamos a suponer que el nodo tiene un hardware especial y no queremos que los pods normales vayan a ese hardware especial, solo determinados pod que tengan la condicion y la tolerancia correspondiente.
## Ver los nodos
```
kubectl get nodes
```
## Agregar Taint a un nodo
```
kubectl taint nodes ip-172-31-0-68.us-west-2.compute.internal memori=grande:NoSchedule
```
## Ver los Taints 
```
kubectl describe nodes | grep Taint
```
## Vamos a crear un deploy para ver que no se va a crear en el nodo que tiene nuestro taint
```
kubectl create deploy apache1 --replicas=10 --image=httpd
```

```
kubectl get pods -o wide
```
Podemos ver que ningun pod se creo en el nodo que tiene nuestro tain.
## Ejecutar un deploy para ver que si se adjunta al node con nuestro taint
```
kubectl apply -f deploy_nginx-toleration.yaml
```

```
kubectl get pods -o wide
```
Vamos hacer nuestro primer ejemplo de asociar un pod a un determinado nodo. Este metodo es el menos adecuado no es nada recomendable. Porque lo que hacemos en colocar en el pod el nodo al que queremos acceder.
# Workspace
```
cd /home/jon/Documents/kubernetes/16 SCHEDULER ASIGNAR PODS A NODOS/recurso_asignar_manual
```

# Ver los nodos
```
kubectl get nodes
```

# Crear nodo
```
kubectl apply -f pod.yaml
```
# Verificar la creacion del pod
```
kubectl get pod
kubectl get pod -o wide
```
Vamos a ver que nuestro pod esta en **Pending** porque no tengo un nodo llamado worker-01. Aqui me estoy saltando el Scheduler, el Scheduler es quien decide a que nodo debe ir un pod, y como yo le estoy diciendo a que nodo de ir pues no entra en funcionamiento. Despues de un tiempo este pod va ser rechazado y va dejar de intentar crearlo, se va dar cuenta de que no hay un nodo que cumpla con esa condicion y se escapa.

Ahora vamos hacerlo bien vamos a obtener los nombres de los nodos
```
kubectl get nodes
```

Vamos a modificar el fichero pod.yaml
Before
```
nodeName: worker-01
```

After
```
nodeName: ip-172-31-11-207.us-west-2.compute.internal
```
# Crear pod
```
kubectl apply -f pod.yaml
```
# Verificar que se creo el pod en el nodo especifico
```
kubectl get pod -o wide
```
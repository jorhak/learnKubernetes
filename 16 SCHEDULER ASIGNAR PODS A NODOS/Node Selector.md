Una manera mas eficiente de determinar a que nodos puede ir un pod es utilizar el selector de nodos, el Node Selector.
Lo que hace es buscar una serie de nodos que tengan una determinada condicion para ser candidatos a que ese pod pueda ir a ese nodo y como se ponen esas condiciones, pues a traves de las etiquetas.
# Workspace
```
cd /home/jon/Documents/kubernetes/16 SCHEDULER ASIGNAR PODS A NODOS/recurso_node_selector
```
# Ver las etiquetas de los nodos
```
kubectl get nodes --show-labels
```
Podemos ver los labels que k8s les a asignado, ninguno de los nodos cumple con la condicion de nuestro yaml.
# Ejecutar pod
```
kubectl apply -f pod.yaml
```
# Verificar pod
```
kubectl get pods -o wide
```
Vamos a ver que se queda en **Pending** porque no cumple con la regla de asignar el pod al nodo que tenga la etiqueta.
Vemos que el pod no escapa porque en algun momento puede que algun nodo cumpla con la regla y se asigne a ese pod.
# Crear etiqueta
```
kubectl label node ip-172-31-11-207.us-west-2.compute.internal entorno=desarrollo
```
Volvemos a ver si nuestro pod se a creado en el nodo correspondiente
```
kubectl get pods -o wide
```
Y volvemos a ejecutar el comando para ver si el nodo tiene la etiqueta
```
kubectl get nodes --show-labels
```

La forma en la que lo podemos aplicar es de que en un cluster hay muchos nodos en los que los podemos separar: desarrollo, staging, produccion.
Y de esta forma los nodos van a ir a parar a los nodos de desarrollo, staging, produccion. Dependiendo del selector label y poder segmentar a que nodos se van los pods.



# Workspace
```
cd /home/jon/Documents/kubernetes/16 SCHEDULER ASIGNAR PODS A NODOS/recurso_node_selector
```
# Ver los nodos del cluster
```
kubectl get nodes
```
# Procedemos a etiquetar dos nodos
Supongamos que tenemos unos 6 nodos y le agregamos la etiqueta a dos de ellos para que el deploy cree los pods en esos nodos especificos. Esto puede ser porque esos nodos tiene caracteristicas especiales para que esos pods puedan ejecutarse correctamente, por decir, mayor ram, cpu, gpu, etc.
```
kubectl label node ip-172-31-3-51.us-west-2.compute.internal aplicacion=web
```
# Verificar que se agrego la etiqueta
```
kubectl get nodes --show-labels
```
# Desplegar deploy
```
kubectl apply -f deploy-nginx.yaml
```
# Verificar que los pods estan creados en los nodos especificados
```
kubectl get pods -o wide
```
Podemos ver que los pods fueron creados en los dos nodos a los que les agregamos la etiqueta.
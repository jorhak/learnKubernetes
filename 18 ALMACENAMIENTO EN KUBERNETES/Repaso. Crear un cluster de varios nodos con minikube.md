Recomendacion tener al menos 3,4,5 worker nodes, lo podemos hacer en minikube, docker windows en un solo nodo, pero es mas interesante tener mas de un nodo.
En la practica siguiente vamos a utilizar NFS y seria interesante tener un cluster que tenga varios nodos.
En minikube para crear un cluster con varios nodos va depender de los recurso que tengamos disponibles, para cada node se va requerir CPU: 2, MEMORY:2 y si no contamos con los recursos no se van a poder crear los nodos.
# Crear cluster
Vamos a crear un cluster de tres nodos
```bash
minikube start -p cluster1 -n 3
```
# Listar nodos
```bash
kubectl get nodes
```
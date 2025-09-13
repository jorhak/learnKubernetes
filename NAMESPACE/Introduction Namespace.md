Un namespace es una division logica del cluster de K8s para poder dividir los objetos en distintas zonas.
Puedo tener distintos namespace y dentro puedo crear los objetos y trabajar con ellos, de forma que tengo como particiones dentro del cluster.

# Ver los namespace
```
kubectl get namespace
kubectl get ns
kubectl get namaspace default
kubectl describe namespace default
```

A los _namespace_ se les puede indicar que tenga ciertas limitaciones a nivel de recursos para los objetos que se alojen dentro de ese _namespace_.

# Ver los pods de un namespace
```
kubectl get pods -n kube-system
```
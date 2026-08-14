LoadBalancer es el mismo que NodePort la diferencia es que funciona dentro de un Cloud (AWS, Azure, GCP, etc).
Puedo crear un LoadBalancer dentro de minikube?
Si es puede, pero debes saber que hay un inconveniente es que en realidad estoy creando un NodePort porque se comporta exactamente igual que un NodePort porque no tiene ninguna posiblidad de estar en modo Cloud. /

# Ejemplo
```
kubectl create deployment apache2 --image=httpd
kubectl expose apache2 --port=80 --type=LoadBalancer
kubectl get svc -l app=apache2
```

Vamos a ver que en _External_ip_ su estado se queda en _pending_ que es exactamente como queda cuando creamos un _service_ de tipo _NodePort_.

Lo que quiere decir esto que _LoadBalancer_ solo debe crease en un proveedor de la nube, de lo contrario no tendria sentido. Ya que en cloud hay un driver que le asigna esa **IP externa** para exponer el _deployment_.


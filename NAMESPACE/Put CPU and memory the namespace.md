Vamos a ver como ponerle limites de memoria y de CPU a nuestros _pods_ pero dentro de un _namespace_, es decir, que a partir de la configuracion por defecto del _namespace_ le indicamos que a los _pods_ que se creen cumplan esas condiciones.

# Create namespace
```
kubectl create namespace n1
```

# Ver que se creo el namespace
```
kubectl get namespace n1
```

# Describir el namespace
```
kubectl describe namespace n1
```

Aqui vamos a ver que no tenemos ningun tipo de liminte.

# Agregar limintes modo descriptibo
```
kubectl apply -f limintes.yaml -n n1
```

# Ver que se aplicaron los cambios
```
kubectl describe namespace n1
```

# Verificar la configuracion
```
kubectl run nginx --image=nginx -n n1
```

# Ver que se crearon los objetos
```
kubectl get deploy -n n1
kubectl get pods -n n1
```

# Ver los limintes de los pods
```
kubectl describe pod <nombre del pod> -n n1
```
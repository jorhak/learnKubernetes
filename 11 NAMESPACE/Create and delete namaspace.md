# Crear namespace modo imperativo
```
kubectl create namespace hola
```

# Ver que se creo
```
kubectl get namespace
```

# Ver los pods 
```
kubectl get pods -n hola
```

Vamos a ver que no tenemos ningun objeto creado dentro del _namespace_.

# Crear namespace modo declarativo
```
kubectl apply -f namespace.yaml
```

# Describir namespace
```
kubectl describe namespace dev1
```

# Borrar namespace modo imperativo
```
kubectl delete namespace hola
```

# Borrar namespace modo declarativo
```
kubectl delete -f namespace.yaml
```
# Crear objetos dentro de un namespace
```
kubectl apply -f deploy_elastic.yaml --namespace=dev1
```

# Ver en que namespace creo los objetos
```
kubectl get deploy elastic
```

#### Nos dice que no a encontrado al objeto.

```
kubectl get deploy elastic -n dev1
```

#### Nos muestra los objetos creados en ese namespace.

Ver la descripcion del objeto que esta en el namespace
```
kubectl describe deploy elastic -n dev1
```

# Error
Vamos a tener un error aqui ya que la imagen elasticsearch:latest no existe en el repositorio de **docker hub**. Vamos a crear un issue para dejear resgistro y practicar.

La solucion es ir a **docker hub** y ver que versiones tiene _elasticsearch_ y modificar nuestro _elastic_deploy.yaml_. 
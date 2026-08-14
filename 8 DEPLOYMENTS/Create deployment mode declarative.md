Vamos a crear un deployment de modo declarativo utilizando _apply_. Si llegaramos a utilizar _create_ este lo hace de forma imperativa, ya que no guarda el estado del **deployment** mientras que _apply_ si guarda el estado, es por eso que si hacemos un cambio en el .yaml y volvemos a ejecutar este ve el estado en el que se encuentra el **deployment** y lo compara con el .yaml y lo actualiza.
Cuando utilizamos _create_ no podemos hacer lo que mencionamos previamente para hacer un cambio debemos eliminar el **deployment** y volver a crearlo con los cambios.

deploy_nginx.yaml
```
apiVersion: apps/v1 # i se Usa apps/v1beta2 para versiones anteriores a 1.9.0
kind: Deployment
metadata:
  name: nginx-d
spec:
  selector:   #permite seleccionar un conjunto de objetos que cumplan las condicione
    matchLabels:
      app: nginx
  replicas: 2 # indica al controlador que ejecute 2 pods
  template:   # Plantilla que define los containers
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
```

## Ejecutar deployment
```
kubectl apply -f deploy_nginx.yaml
```

## Verificar que los pods se crearon
```
kubectl get pods
```

## Verificar que replicaset se creo
```
kubectl get rs
```

## Verificar que el deployment se creo
```
kubectl get deploy
```

## Otras formas de ver los objetos con mas detalle
```
kubectl get pod -o wide
kubectl get rs -o wide
kubectl get deploy -o wide
```

## Buscar por etiqueta
```
kubectl get pods -l app=nginx
```

## Crear columna de la etiqueta
```
kubectl get pods -l app=nginx -L app
kubectl get pods -L app
```

## Ver distintos tipos de objetos a la ves
```
kubectl get pod,rs,deploy
kubectl get pod,rs,deploy -l app=nginx #para filtrar por la etiqueta
```
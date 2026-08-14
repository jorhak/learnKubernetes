
Debemos definir la nomenclatrua de las etiquetas dentro de la empresa ya esta soporta una longitud de 63 caracteres, pueden comenzar con numero o letra, admiten puntos y guiones. No admiten espacios en blaco y caracteres raros. Esto para tener defino como van a ser nombradas las llaves de las etiquetas.

## Anadir una etiqueta
```
kubectl label pod tomcat responsable=marco
```

## Ver que se agrego la etiqueta
```
kubectl get pod tomcat --show-labels
kubectl get pod tomcat --show-labels -L estado,responsable
```

# Modificar una etiqueta
```
kubectl label --overwrite pod tomcat estado=test
```

# Borrar etiqueta
```
kubectl label pod tomcat responsable-
```
Podemos ver que aqui no hay un **remove**, sin embargo, vemos que ya no esta la etiqueta.
responsable-: aqui tenemos un guion al final.

Hasta aqui hemos trabajado de forma imperativa, lo mejor es trabajar de forma declarativa. Todo lo que hicimos previamente lo podemos hacer de forma declarativa.

Agregar etiqueta
```
apiVersion: v1
kind: Pod
metadata:
  name: tomcat
  labels:
    estado: "desarrollo"
    responsable: "tono"
spec:
  containers:
    - name: tomcat
      image: tomcat
```

```
kubectl apply -f tomcat.yaml
kubectl describe pod tomcat
```

Editar etiqueta
```
apiVersion: v1
kind: Pod
metadata:
  name: tomcat
  labels:
    estado: "desarrollo"
    responsable: "SERGIO"
spec:
  containers:
    - name: tomcat
      image: tomcat
```


```
kubectl apply -f tomcat.yaml
kubectl describe pod tomcat
```

Eliminar etiqueta
```
apiVersion: v1
kind: Pod
metadata:
  name: tomcat
  labels:
    estado: "desarrollo"
spec:
  containers:
    - name: tomcat
      image: tomcat
```

```
kubectl apply -f tomcat.yaml
kubectl describe pod tomcat
```
Las label son solo etiquetas que le ponemos a los objetos, estas se pueden repetir en otros objetos.
Los selectores son como *Where are* condiciones que utilizo para encontrar objetos con determinadas etiquetas, es decir, buscar los **pods** que tengan como etiqueta desarrollo, pues desde alli va intentar buscar todos los objetos que tengan esa condicion.

Vamos ejecutar varios **.yaml** las cuales van a tener etiquetas diferentes.
```
kubectl apply -f .
```

. : que ejecute todo lo que hay en el directorio actual, ya que en nuestro caso tenemos cuatro ficheros los va ejecutar todos.

tomcat.yaml
```
apiVersion: v1
kind: Pod
metadata:
  name: tomcat
  labels:
    estado: "desarrollo"
    responsable: "juan"
spec:
  containers:
    - name: tomcat
      image: tomcat
```

tomcat1.yaml
```
apiVersion: v1
kind: Pod
metadata:
  name: tomcat
  labels:
    estado: "desarrollo"
    responsable: "juan"
spec:
  containers:
    - name: tomcat
      image: tomcat
```

tomcat2.yaml
```
apiVersion: v1
kind: Pod
metadata:
  name: tomcat
  labels:
    estado: "testing"
    responsable: "pedro"
spec:
  containers:
    - name: tomcat
      image: tomcat
```

tomcat2.yaml
```
apiVersion: v1
kind: Pod
metadata:
  name: tomcat
  labels:
    estado: "producion"
	    responsable: "pedro"
spec:
  containers:
    - name: tomcat
      image: tomcat
```

## Como buscar con los selectores
```
kubectl get pod --show-labels -l estado=desarrollo
kubectl get pod --show-labels -l estado=testing
kubectl get pod --show-labels -l estado=produccion
```

## Condiciones tipo AND
```
kubectl get pod tomcat --show-labels -l estado==desarrollo,responsable=juan
```

## Condicion tipo !AND
```
kubectl get pod tomcat --show-labels -l responsable!=juan
```

## Conjuntos

Buscar todos los **pods** que estan en desarrollo
```
kubectl get pod tomcat --show-labels -l 'estado in(desarrollo)'
```

Buscar los que estan en desarrollo y test
```
kubectl get pod tomcat --show-labels -l 'estado in(desarrollo,testing)'
```

Tambien tenemos el notin, que no este en desarrollo y testing
```
kubectl get pod tomcat --show-labels -l 'estado notin(desarrollo,testing)'
```

# Eliminar pods a traves de los selectores
```
kubectl delete pods -l estado=desarrollo
```
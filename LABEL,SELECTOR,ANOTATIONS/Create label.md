Hoy vamos a hablar sobre las etiquetas. Tenemos nuestro **tomcat.yaml** en donde vamos a hacer nuestra prueba de etiqueta.

tomcat.yaml
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

Ejecutamos 
```
kubetctl apply -f tomcat.yaml
```

Ahora para ver las etiquetas de nuestro **POD** ejecutamos
```
kubectl get pod tomcat --show-label
```

--show-label: nos permite ver las etiquetas del objeto

## Crear columna con los valores de las etiquetas
```
kubectl get pod tomcat --show-label -L estado
```

Si agregamos una etiqueta que no existe este nos la muestra en blanco ya que no verifica si existe la etiqueta.
```
kubectl get pod tomcat --show-label -l estado,apli
```


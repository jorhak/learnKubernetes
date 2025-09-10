Los labels son objetos que identifican a los componentes y que luego puedo buscar que otros componentes van a utilizar para relacionarse con **pods, deployments, replicaset, etc**,.
Las anotaciones son similares a los labels por que son clave-valor. En realidad son mas descriptivas, poner documentacion, comentarios.
Las anotaciones sirven para describir y documentar a nuestros componentes.

tomcat4.yaml
```
apiVersion: v1
kind: Pod
metadata:
  name: tomcat
  labels:
    estado: "desarrollo"
  annotations:
    doc: "Se debe compilar con gcc"
    adjunto: "ejemplo de anotacion"
spec:
  containers:
    - name: tomcat
      image: tomcat
```

```
kubectl apply -f tomcat4.yaml
kubectl describe pod tomcat4
```

# Ver las anotaciones
```
kubectl get pod tomcat -o jsonpath={.metadata.annotations}
```
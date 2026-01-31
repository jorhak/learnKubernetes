Lo que se quiere ensenar es que las variables por si solas no utililes hasta que las utilizas, en nuestro caso le vamos a pasar variables a nuestro contenedor para que crear un contenedor con MySQL, estas varibles no son diferentes de las de docker solo que la estamos usando en K8s.
```
kubectl apply -f mysql.yaml
kubectl get pod
kubectl exec -it mysql-deploy-xxxxxx.xxxx bash
printenv
mysql -u usdb -p kuberntes
```
```
kubectl create configmap datos-mysql-env --from-env-file datos_mysql.properties
```

```
kubectl get cm
kubectl describe configmap datos-mysql-env
kubectl get cm datos-mysql-env -o yaml
```

```
kubectl apply -f pod1.yaml
```

Vamos a tener una diferencia entre el .yaml anterior, que utiliza env mientras que el que vamos a utilizar usa envFrom.

```
kubectl get pod
kubectl exec -it pod1 bash
printenv
echo $MYSQL_USER
```
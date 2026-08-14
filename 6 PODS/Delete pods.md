El comando para borrar se puede aplicar a cualquier otro objeto que hayamos creado.

En este caso lo vamos hacer con los **pods**, lo primero que debemos hacer es listar los **pods**

```
kubectl get pods
```

Luego elegimos el **pod** que deseamos borrar

```
kubectl delete pod nginx
kubectl delete pod/nginx1
```

Tambien existen otros flags para la eliminacion de un objeto por decir que espere un determinado tiempo o que lo elimine de inmediato

```
kubectl delete pod nginx --grace-period=5
kubectl delete pod nginx1 --now
```

Luego tenemos un flag que pude ser peligroso el cual no se recomienda emplear, en este caso elimina a todos los **objetos** de tipo **pod**

```
kubectl delete pods --all
```

El comando **delete** va ser el mismo para todos los objetos: pods, deployment, service, etc.
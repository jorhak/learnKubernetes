## Ver las propiedades de un POD
```
kubectl describe pod/nginx1
```

No solo podemos ver la propiedades del objeto **POD**, sino de cualquier otro objeto del cluster de k8s. Para ello debemos colocar como prefijo el objeto y luego el nombre del objeto en este caso nuestro objeto es **POD** y el nombre del objeto es **nginx1**. Esto es valido para los otros objetos: replicaset, deployment, secret, configmap, etc.


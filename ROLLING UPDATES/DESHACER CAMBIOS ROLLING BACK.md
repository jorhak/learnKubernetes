Cuando hacemos RollingBack?
Cuando la imagen no nos convence, esta falla, se tarda en responder.
Vamos hacer que nuestro **deploy_nginx2.yaml** falle para hacer un RollingBack.
```
image: nginx:1.16.hh1
```

```
kubectl apply -f deploy_nginx2.yaml
```

# Ver el estado del RollingUpdate
```
kubectl rollout status deploy nginx-d
kubectl get pods
kubectl get rs
kubectl rollout history deploy nginx-d
kubectl rollout history deploy nginx-d --revision=4
```

Aqui en los _pods_ vamos a tener un error **ErrImagePull** esto se debe a que no se puede localizar la imagen.
Tambien nos vamos a dar cuenta que nos hemos equivocado con el tag de la imagen.
Ahora lo que debemos hacer es volver hacia atras.

# RollingBack
```
kubectl rollout undu deploy nginx-d --to-revision=2
kubectl rollout status deploy nginx-d
kubectl rollout history deploy nginx-d
kubectl rollout history deploy nginx-d --revision=5
```

Lo que hace aqui es que quita la revision 2 y la pone en la revison 5. La dos se convierte en la cinco.
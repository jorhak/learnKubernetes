El objeto mas sencillo que podemos utilizar para conectar exterior o injectarle datos y propiedades a nuestro contenedores, nuestros _pods_ que son los que pueden utilizar estas variables.
Lo que se hizo fue crear variables para un _pod_.
```
    env:
    - name: NOMBRE
      value: "Curso de Kubernetes"
    - name: PROPIETARIO
      value: "Apasoft Training"
```

Podemos ver como es que le pasamos las variables a los contenedores. Por si solas las variables no hacen nada, sino que lo que hagan con ellas es lo que importa dentro del contenedor.

```
kubectl apply -f var1.yaml
kubectl get pod
kubectl exec -it var-ejemplo bash
printenv
echo $NOMBRE
echo $PROPIETARIO
```
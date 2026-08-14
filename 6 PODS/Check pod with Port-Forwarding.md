Es mapear un puerto local a un puerto remoto similar al servicio, el servicio es un recurso interno de k8s y port-forwarding es un recurso general que se suele usar en muchas redes y que k8s tambien lo tiene.

No es algo que se deba utilizar un produccion, sin embargo, para realizar pruebas esta bien, para no tener que crear servicios o similares.

```
kubectl port-forward nginx 9999:80
```

Aqui podemos ver que vamos a utilizar el puerto 9999 para poder acceder al pod nginx que tiene el puerto 80.

```
localhost:9999
```

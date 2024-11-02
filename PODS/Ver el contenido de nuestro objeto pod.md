Como ya hemos creado nuestro pod desde el fichero .yaml tambien podemos ver la configuracion que tiene nuestro pod ya  en ejecucion, las salidas de esta configuracion puden ser de tipo **json** o **yaml**.

```
kubectl get pod/nginx -o yaml > f1.yaml
kubectl get pod/nginx -o json > f1.json
```

Esto nos sera util cuando queramos cambiar las configuraciones de nuestro objeto pod.
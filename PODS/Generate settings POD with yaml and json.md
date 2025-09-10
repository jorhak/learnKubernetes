# Vamos a capturar las configuraciones de un POD en los formatos ymal y json

nginx.yaml
```
kubectl get pod/nginx -o yaml > nginx.yaml
```

nginx.json
```
kubectl get pod/nginx -o json > nginx.json
```
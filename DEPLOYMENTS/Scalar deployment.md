Escalar un _deployment_ de forma manual, ya antes lo hicimos desde el fichero .yaml.

## Escarlar deployment
```
kubectl scale deploy nginx-d --replicas=5
```

## Verificar el escalado
```
kubectl get deploy nginx-d
kubectl get rs 
kubectl get pods
```

## Escalar a traves de los labels
Vamos a modificar el deploy_nginx.ymal
```
apiVersion: apps/v1 
kind: Deployment
metadata:
  name: nginx-d
  labels:
    estado: "1"
```

Al ser un numero debo colocarle comillas

## Aplicar cambios
```
kubectl apply -d deploy-nginx.yaml
```

### Escalar con labels
```
kubectl scale deploy -l estado=1 --replicas=10
kubectl scale deploy -l estado=1 --replicas=2
```
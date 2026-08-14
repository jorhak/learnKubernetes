Vamos a modificar el fichero deploy_nginx2.yaml
```
strategy:
   type: Recreate
minReadySeconds: 2
```

# Aplicar estrategia
```
kubectl apply -f deploy_nginx2.yaml
kubectl describe deploy nginx-d
kubectl rollout history deploy nginx-d
```

## Cambiar la imagen
```
image: nginx:1.17.8
```

```
kubectl apply -f deploy_nginx2.yaml
kubectl get pods
```

Ahora lo que vemos es que todos los _pods_ los termina y luego los recrea.
Para este escenario seria cuando la aplicacion no funciona y no tiene sentido ir apangando progresivamente y levantando la nueva aplicacion de la misma forma.
Sino que terminamos todos los _pods_ y los volvemos a iniciar. No necesitamos esperar que los borre todos y que los vuelva a cargar.

```
kubectl rollout history deploy nginx-d
kubectl rollout history deploy nginx-d --revision=7
```

Hemos visto dos estrategias en donde la primera dice, voy haciendolo, modificandolo, eliminando y sustituyendo. Y el otro los elimino de golpe y los sustituyo de golpe.

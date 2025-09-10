NodePort aquel que nos permite exponer nuestro deployment, pod al exterior (fuera del cluster).

Vamos a comenzar creado un _deploy_ para que luego lo podamos exponer con un _service_.
## Deploy
```
kubectl create deploy apache1 --image=http
kubectl get all
```

## Service
Ya sea un _pod_, _deploy_ lo que hace es exponer al objeto con el exterior. Lo mas normal es asociarlo a los _deploy_, como hemos visto tambien lo podemos asociar a un _pod_.
```
kubectl expose deploy apache1 --port=80 --type=NodePort
```

--port=80: puerto interno por el que esta escuchando el _pod_
--type=NodePort: sin no le pongo el tipo me lo va tomar como ClusterIP. El --type solo se usa para _NodePort_ y _LoadBalancer_, no es necesario para ClusterIP.

## Verificar la creacion del service
```
kubectl get svc
```

Ahora cuando nos muestro el resultado vamos a ver **PORT(S)** el cual nos indica el puerto del _pod_ y el puerto por el cual vamos acceder al _pod_ desde el exterior.

## Verificar service
Lo primero que hacemos es saber cual es la ip de nuestro cluster
```
minikube ip
```

Abrimos el navegador y escribimos la _ip_ y el puerto del _service_
```
192.178.43.2:3945
```

Esto solo para minikube
```
minikube service list
```
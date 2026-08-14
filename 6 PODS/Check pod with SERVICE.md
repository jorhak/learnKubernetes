# Probar el POD con un servicio
Como ya hemos visto con _kubectl proxy_, es una forma alternativa para hacer la prueba de que nuestro _pod_ esta funcionando. Ahora vamos a exponer nuestro _pod_ con el objeto **SERVICE**.

Primero listamos nuestros _pods_.
```
kubectl get pods
```

Exponer _pod_
```
kubectl expose pod nginx1 --port=80 --name=nginx1-svc --type=LoadBalancer
```

Ver los services
```
kubectl get svc
```

Debemos pedir cual es la IP de nuestro minikube
```
minikube ip
```

Una ves tengamos el puerto del _service_ y la IP de minikube abrimos nuestro navegador y escribimos la IP y el puerto.
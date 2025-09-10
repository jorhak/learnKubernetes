
# Acceder a un POD
```
kubectl exec -it $pod -n $namespace -- bash
kubectl exec -it laravel-app-54c45994f6-4ghls -n monografia -- bash 
```
Lo que tenemos aqui es que podemos acceder al POD de modo interactivo y luego dentro del POD ejecutar comandos. Para salir del POD escribimos el comando _exit_.

```
kubectl exec nginx1 -- ls
```
Aqui lo que tenemos es que estamos ejecutando comandos dentro del POD, sin embarago, no estamos dentro del POD, como el anterior comando.
Los de tipo _ClusterIP_ solo son accesibles desde dentro del propio cluster, digamos que son servicios privados estandar. Si no digo nada el tipo siempre es de _ClusterIP_. Al final los Middelware y Backend que tengamos dentro de nuestro _Cluster de K8s_ suelen tener este tipo de servicio porque no queremos exponerlos hacia fuera.

Server
```
kubectl create deployment redis-master --image=redis
kubectl get deploy -l app=redis-master
kubectl get pods -l app=redis-master
```

Cliente
```
kubectl create deployment redis-cli --image=redis
kubectl get deploy -l app=redis-cli
kubectl get pods -l app=redis-cli
```

Servicio para conectarnos al Server
```
kubectl expose deploy redis-master --port=6379 --type=ClusterIP
kubectl get svc -l app=redis-master
```

Vamos a conectarnos desde el Cliente
```
kubectl get pods
kubectl exec -it <nombre del pod> -- bash 
redis-cli -h redis-master
set v1 10
```

Vamos a conectarno al Server (abrimos otra terminal)
```
kubectl exec -it <nombre del pod> -- bash
redis-cli # se conecta en local
info keyspace
get v1
```

El hostname es el que aparece en el _Service_. Aqui lo que tenemos es que el _deploy_ no es conocido hasta que le creamos un servicio el cual funciona como un tipo de DNS. Ahora si quiero acceder a ese _pod_ lo hago a traves del _service_.
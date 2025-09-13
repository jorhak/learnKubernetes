Vamos a desplegar una aplicacion que va constar de cinco objetos:
Redis Master: se va a encargar de la escritura 
Redis Master Service: expone el servicio de manera interna con ClusterIP
Redis Slave: se va a encargar de la lectura
Redis Slave Service: expone el servicio de manera interna con ClusterIP
PHP: servicio frontend

Nos debemos dirigir a "Ejemplo\ PHP/ejemplo" para ejecutar los comandos.
# Redis Master
```
kubectl apply -f redis-master.yaml
kubectl get all -l app=redis
```
## Redis Master Service
```
kubectl apply -f redis-master-service.yaml
kubectl get svc 
kubectl describe svc redis-master-svc
```

Con el ultimo comando podemos ver la **IP** del servicio y los **Endpoints** a los que apunta el servicio. Y tambien el puerto por el cual se conecta.

### Verificar que los pods se pueden comunicar con el servicio
```
kubectl get pods
kubectl exec -it <nombre del pod> -- bash
kubectl exec -it redis-master-388738438-f34l -- bash
uname -a
cat /etc/host
```

Como puedo yo probar que efectivamente puedo acceder al servicio?
Kubernetes integra un DNS (un servicio de DNS), que es el que usa para el nombre de las maquinas, los nombres de los recurso, los nombres de los servicios.

Si hago un "uname -a" dentro del _pod_ me da el nombre del propio _pod_.
Si haga un "cat /etc/hosts" vemos la **IP** que tiene el _pod_, sera el _endpoint_ que vimos en el **describe** del servicio.

Abrimos otra terminal para verificar con el servicio
```
kubectl describe svc redis-master-svc
```

Nos volvemos a la terminal anterior para verificar si el _pod_ puede llegar al _service_
```
ping redis-master-svc
wget redis-master-svc
```

El servicio no responde a un ping pero si veo que me a capturado la **IP** del _service_. Efectivamente es capas de reconocer la **IP**.

### Instalar nslookup
```
apt update
apt install bind-utils #o
apt install dns-utils
```

Con esto vamos a preguntar que **IP** tiene determinado _service_ y lo tiene que encontrar en el DNS

```
nslookup redis-master-svc
```

Vemos el nombre del servicio con la **IP** que le corresponde.
Vamos a ver la **IP** del servidor DNS que ha creado Kubernetes para gestionarse.

```
cat /etc/resolv.conf
```

Fichero que apunta al DNS de esta maquina, le dice que busque el servidor de DNS y este servidor de nombres es el que traduce el nombre del servicio a la **IP** correspondiente.
# Redis Slave
```
kubectl apply -f redis-slave.yaml
```

## Redis Slave Service
```
kubectl apply -f redis-slave-service.yaml
```

### Verificar que los pods del master y slave se pueden conectar
```
kubectl get svc
kubectl get pods
```

Aqui vamos a obtener los nombres de Redis Slave y Redis Master lo que vamos hacer es entrar al _pod_ de Redis Master ya que este tienen instalado _nslookup_ y vamos a probar que puede llegar a Redis Slave Service

```
kubectl exec -it <nombre del pod Redis Master> -- bash
nslookup redis-slave
```

Podemos ver que nos va la **IP** del servicio.

Abrimos otra terminal para compara las **IP's**

```
kubectl get svc
```

Ahora los **pods** se ven entre si, que los hemos configurados con servicos que les han hecho accesibles desde la propia red del cluster. Todavia no se pueden acceder desde fuera. 
# PHP
```
kubectl apply -f frontend.yaml
kubectl get pods
kubectl get pods all -l app=guestbook
```


## PHP Service
```
kubectl apply -f frontend-service.yaml
kubectl get svc
kubectl describe svc frontend
```

# Probar app
```
minikube ip
```

Ahora con esta **IP** y el puerto que se le asigno al servico de tipo **NodePort** vamos acceder a la apliacion.

Abrir navegador
```
192.168.34.22:30352
```

# Probar conectividad del servicio frontend con Redis Master 
```
kubectl get pods 
kubectl exec -it redis-master-88d934l3e-345l3 --bash
nslookup frontend
```

Efectivamente tenemos la **IP** del servico.




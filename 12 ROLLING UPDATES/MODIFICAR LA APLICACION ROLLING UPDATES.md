Cuando decido cambiar una imagen, alguna caracteristica del container esto va probocar que los _pods_ que tengan esos contenedores se destruyan y se recreen.
Porque? Por que evidentemente si modifico la plantilla k8s va intentar llegar a ese estado, al estado deseado de esa plantilla.
Vamos a tener dos estrategias:
1. RollingUpdate
2. Recreate
Que diferencias tienen estas dos estrategias:
RollingUpdate va modificando los _pods_ de manera evolitiva (los va haciendo de poco a poco) para que siempre haiga algun _pod_ que este dando servicio de esta manera no corto el servicio sino que los _pods_ se van sustituyendo con la nueva version, con el nuevo componente de una manera pausada.
Mientras que Recreate directamente borra todos los _pods_ de la version antigua y los sustituye por la nueva, en este caso si tengo perdida de servicio temporalmente.

Se produce un Update cuando se cambia alguna propiedad inerente a los contenedores, es decir, si yo cambio la label de un _deployment_ eso no es un cambio, un update que obliga hacer un RollOut de nuevo. 
Pero si le cambio por ejemplo la label de un contenedor, el puerto, o le cambio algun valor importante eso si que puede producir un Update.

```
kubectl apply -f deploy_nginx2.yaml
kubectl get pods
kubectl describe deploy nginx-d
```

### El historico del deployment nginx-d
Lo que vamos a ver sera que solo tenemos un cambio porque este surgio cuando lo hemos desplegado. 
```
kubectl rollout history deploy nginx-d
```

### Especificar revision
Nos da mas detalles sobre container
```
kubectl rollout history deploy nginx-d --revision=1
```

## RollingUpdate
Lo que vamos hacer para obligarle hacer un Update es cambiarle la imgen del container, vamos a modificar el **deploy_nginx2.yaml**
Esto es un cambio importante porque modifico mi despliegue de manera notable dentro del _pod_.
```
kubectl apply -f deploy_nginx2.yaml
```

Ahora va empezar a reconstruir mediante un RollingUpdate los _pods_ que tenga dentro de este despliegue.
```
kubectl get pods
kubectl get deploy
```

Aqui vamos a ver que unos estan corriendo, otros se estan finalizando y otros se estan creando.

## Revisar lo RollingUpdate
Vamos apreciar que se ha cambiado de uno a otro
```
kubectl rollout histroy deploy nginx-d
kubectl rollout history deploy nginx-d --revision=2
kubectl rollout history deploy nginx-d --revision=1
```

Que paso con los Replicaset?
Ahora el _replicaset_ lo tengo a cero y no tengo nada. Mientras que el _replicaset_ nuevo lo tengo configurado y trabajando.

Vamos a modificar mas propiedades para hacer un RollingUpdate.
Politica de cambios de _pods_ lo que hace es sumar o restar uno, si tenemos 10 replicas no podemos tener 11 se suma (maxUnavailable), si tenemos 10 replicas no podemos tener menos de 9 se resta (maxSurge). Vamos a estar en este rango
```
strategy:
   type: RollingUpdate
   rollingUpdate:
      maxUnavailable: 1
      maxSurge: 1
```

### Numero de segundos minimos que pasa para crear un pod
Si el numero es muy elevado lo va hacer de forma pausada, por lo que habria demasia pausa en crear un _pod_.
```
minReadySeconds: 2
```

### Bajar la version de la imagen
```
image: nginx:1.16.1
```

## Objetos afectados
Uno de los objetos afectados es el _service_. Por lo que vamos a definir un servicio.
Vamos a ver como cambian los _endpoints_ del _service_ ya que con el RollingUpdate se crean nuevos _pods_.
```
kubectl apply -f nginx-svc.yaml
kubectl describe svc nginx-svc
```

### Aplicar el RollingUpdate
```
kubectl apply -f deploy_nginx2.yaml
kubectl get pods
kubectl get rs
kubectl get describe svc nginx-svc
kubectl get rs
kubectl get rollout history deploy nginx-d
kubectl get rollout history deploy nginx-d --revision=3
kubectl describe svc nginx-svc
```

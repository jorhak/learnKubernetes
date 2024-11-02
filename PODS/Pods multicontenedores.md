Bien vamos a ver que se tenga dos contenedores en un pod. Un Nginx y un componente que lo monitoree y le haga ping, y desde afuera ver los logs del componente.

Antes que nada vamos a borrar todo con el comando
```
kubectl delete all --all
```

Aqui debemos explicar la sintaxis de este comando:
kubectl >> comando que se ejecuta en el k8s
delete   >> accion que se va emplear
all          >> tipo de objeto al que sele va aplicar la accion                    en este caso es a todos los objetos: pod, svc,                    depleyment, etc.
--all       >> indica que se ve aplicar a todos los que pertenecen a ese servicio, por decir, si tenemos tres pods los va a eliminar, si tenemos cinco svc de igual modo los va a eliminar.

Tenemos para este ejemplo un fichero **multi.yaml** y lo ejecutamos

```
apiVersion: v1
kind: Pod
metadata:
  name: multi
spec:
  containers:
  - name: web
    image: nginx
    ports:
    - containerPort: 80  
  - name: frontal
    image: alpine
    command: ["watch", "-n5", "ping",  "localhost"]
```

```
kubectl apply -f multi.yaml
kubectl get pods 
```

En esta salida donde teniamos habitualmente un 1/1 tenemos 2/2 lo que quiere decir que tenemos dos contenedores en un **pod**.

Ahroa vamos a ver la diferencias que se tienen con el comando **describe**

```
kubectl describe pod multi
```

Ahora teniendo dos contenedores como accedemos a ver los logs de un contendor en especifico, para ello vamos a ejecutar el siguiente comando

```
kubectl logs -f multi -c frontal
kubectl logs -f multi -c web
```

De esa forma podemos ver los logs de un contenedor en especifico de un **pod**. Si no colocamos el flag -c indicando el contenedor nos va mostrar los logs del primer contenedor que se especifico en el fichero **multi.yaml**.

Ejecutar comandos dentro del contenedor

```
kubectl exec multi -c frontal -- data
```

Para ver el movimiento que se realiza podemos entrar al dashboard y ver el comportamiento.
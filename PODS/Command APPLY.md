Con el comando APPLY trabajamos de forma declarativa.

Previamente vimos el comando **create**

```
kubectl create -f nginx.yaml
```

Ahoro si cambiamos el contenido del fichero y lo volvemos a ejecutar nos saldra el mesaje de que ya esta creado de tal forma que no tomo la actualizacion que le hemos hecho.

Para ello utilizamos el comando **apply** el cual nos permitira realizarle cambios a nuestro objeto pod y a cualquier otro objeto que se haya creado con el comando **apply**.

Como ejemplo tenemos este fichero

```
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    zone: prod
    version: v1
spec:
  containers:
   - name: nginx   
     image: apasoft/nginx:v1
```

```
kubectl apply -f nginx.yaml
```

Ahora vamos a modificar el fichero

```
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    zone: prod
    version: v1
    encargado: JorhakMormont
spec:
  containers:
   - name: nginx   
     image: apasoft/nginx:v1
```

Aplicar cambios

```
kubectl apply -f nginx.yaml
```

De esta forma si me va agarar los cambios, sin embargo, si utilizo **create** este no me va dejar hacer la actualizacion.

Para ver que se tomaron los cambios

```
kubectl get pod nginx -o yaml
```

El **apply** me permite hacer cambios mientras que el **create, run** que son de forma imperativa no.
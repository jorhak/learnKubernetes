Politica de restart (restartPolicy), rebote que indica cuando un pod termina.
Como debe rebotar nuestro pod, en este caso para que nuestro pod se reinice tenemos tres opciones:
- Allways        >> Que siempre que cuando el pod                                      tenga un problema o se pare o tenga                             alguna caida que este se reinicie                                    siempre
- OnFailure     >> Que solo se reinicia si ha fallado, solo                             me lo reinicia si el pod si me falla el                                contenedor.
- Never           >> No quiero que este pod haga en                                     reinicio, hasta que se lo haga a mano.

Allways es la opcion predefinida en los **pods**, a los pods que no se le pone la propiedad este se reinicia por defecto.

Vamos a realizar tres ejemplos con las diferentes Politicas de reinicio.

1. Allways. Tenemos el fichero restart-allways.yaml
que vamos a ejecutar con el comando

```
apiVersion: v1
kind: Pod
metadata:
  name: tomcat
  labels:
    app: tomcat
spec:
  containers:
   - name: tomcat     
     image: tomcat
  restartPolicy: Always
```

```
kubectl apply -f restart-allways.yaml
kubectl get pods
```

Vamos a matar el proceso que esta ejecutando este **tomcat**, para ver como reacciona el **pod**, para ello vamos a ejecutar los comandos

```
kubectl exec -it tomcat bash
ps -ef
catalina.sh stop
```

Como vemos ahora estamos fuera del contenedor y se vemos que paso con **get pods**, notamos que el **pod** se a reiniciado. Para notar esto ejecutamos el comando

```
kubectl describe pod tomcat
```

Vamos a borrar el **pod** porque vamos a cambiar la politica a OnFailure

2. OnFailure. Tenemos el fichero restart-allways.yaml que vamos a ejecutar con el comando, al cual se le cambiara la propiedad __restrartPolicy__ por __OnFailure__.

```
apiVersion: v1
kind: Pod
metadata:
  name: tomcat
  labels:
    app: tomcat
spec:
  containers:
   - name: tomcat     
     image: tomcat
  restartPolicy: OnFailure
```

```
kubectl exec -it tomcat bash
catalina.sh stop
```

Hemos vuelto a ejecutar los mismos comandos del anterior y nos a sacado. Con la direfencia de que el **pod** no se ha reiniciado ya que no a tenido ninguna falla sino que nosotros lo hemos detenido.

```
kubectl get pods
kubectl describe pod tomcat
```

Y podemos ver que el **pod** se detuvo y no se ha vuelto a reiniciar ya que no se debio a una falla sino a que se detuvo el servicio de manera formal.

Ahora vamos a probar con otra imagen en la que forzaremos el error y que se vea que se reinicia el contenedor.
Para ello tenemos el fichero **restart-onfailure.yaml** que vamos a ejecutar con el comando

```
apiVersion: v1
kind: Pod
metadata:
  name: on-failure
  labels:
    app: app1
spec:
  containers:
  - name: on-failure
    image: busybox
    command: ['sh', '-c', 'echo Ejemplo de pod fallado  && exit 1']
  restartPolicy: OnFailure
```

```
kubectl apply -f restart-onfailure.yaml
kubectl get pods
```

Ahora podemos ver que nos sale un error en el estatus y si ejecutamos repeditamente el comando

```
kubectl get pods
```

Podremos ver los diferentes estados por los que pasa el contenedor: Error, CrashLoopBackOff.

3. Never. Tenemos el fichero restart-never.yaml que vamos a ejecutar con el comando

```
apiVersion: v1
kind: Pod
metadata:
  name: never
  labels:
    app: app1
spec:
  containers:
  - name: never
    image: busybox
    command: ['sh', '-c', 'echo Ejemplo de pod fallado  && exit 1']
  restartPolicy: Never
```

```
kubectl apply -f restart-never.yaml
kubectl get pods
```

Podemos que el estado es de Error y no a intentado reiniciarse.



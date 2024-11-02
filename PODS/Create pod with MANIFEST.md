Lo primero que vamos hacer es crear nuestra imange desde docker ya que en k8s no se puden crear imagenes, luego subirla nuestro dockerHub, luego la vamos a integrar en nuestro k8s desde un pod.

**Dockerfile**

```
##Descargamos UBUNTU
FROM ubuntu

##Actualizamos el sistema
RUN apt-get update

##En algunas versiones de Linux es necesario configurar una variable para el TIMEZONE
ENV TZ=Europe/Madrid

##Luego creamos un fichero llamado /etc/timezone para configurar 
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

##Instalamos NGINX
RUN apt-get install -y nginx

##Creamos un fichero index.html en el directorio por defecto de nginx
RUN echo 'Ejemplo de POD con KUBERNETES y YAML' > /var/www/html/index.html

##Arrancamos NGINX a través de ENTRYPOINT para que no pueda ser modificado en la creación del contenedor
ENTRYPOINT ["/usr/sbin/nginx", "-g", "daemon off;"]

##Exponemos el Puerto 80
EXPOSE 80
```

Crear la imagen

```
docker built -t jorhak/nginx:v1 .
docker images
docker login
docker push jorhak/nginx:v1
```

Para verificar debemos ir a nuestro dockerHub y validar que se ha subido correctamente.

Ahora que ya tenemos construida nuestra imagen no toca subirla a nuestro k8s, previamente debemos validar nuestra imagen.

```
docker run -d -p 80:8080 -name nginx jorhak/nginx:v1
```

Una ves se este ejecutando nuestro contenedor con la imagen debemos ir a nuestro navegador.

```
localhost:8080
```

Una ves validada nuestra imagen procedemos a construir nuestro .yaml para tenerlo en nuestro k8s.

**nginx.yaml**

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

Una vez que ya tenemos nuestro fichero procedemos a crear nuestro pod con el comando:

```
kubectl create -f nginx.yaml
kubectl get pods
kubectl logs nginx
kubectl describe pod/nginx
```

El comando **create** me permite crear un objeto a partir de un fichero .yaml

## Comprobar que el pod funciona con un servico

Nos vamos a crear un servicio para poder ver el contenido de nuestro nginx.

```
kubectl expose pod nginx --name=nginx-svc --port=80 --type=LoadBalancer

kubectl get svc nginx-svc
minikube ip
```

Ahora con todos estos datos nos vamos a nuestro navegador

```
IP:PORT ##PORT es el puerto del servicio
```




Como eliminar un pod
```
kubectl delete pod/nginx
```

[[Ver el contenido de nuestro objeto pod]]
[[Dashboard de minikube]]


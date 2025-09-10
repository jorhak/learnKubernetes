# Construir la imagen

Para esta practica vamos a contar con una web ya hecha lo que debemos hacer es crear la imagen para la aplicacion web. 
Lo primero que vamos hacer es crear un _Dockerfile_ para crear la imagen y luego vamos a probar la imagen.

Dockerfile
```
##Descargamos una versión concreta de UBUNTU, a través del tag
FROM ubuntu
MAINTAINER Apasoft Formacion "apasoft.formacion@gmail.com"
##Actualizamos el sistema
RUN apt-get update
##Instalamos HTTPD Apache 2
RUN apt-get install -y apache2
##Creamos un fichero index.html en el directorio por defecto de nginx
ADD web /var/www/html
##Exponemos el Puerto 80
EXPOSE 80
##Arrancamos Apache a través de ENTRYPOINT para que no pueda ser modificado en la creación del contenedor
CMD /usr/sbin/apachectl -D FOREGROUND
```

Crear imagen
```
docker build -t practica:v1.0.0 .
```

Probar imagen
```
docker run -d --name imagen-practica -p 8080:80 practica:v1.0.0
```

# Crear deploy y service

Previamente habiamos creado los _service_ de modo imperativo ahora lo vamos hacer de modo declarativo y vamos a crear ambos objetos desde un solo .yaml.

### completo.yaml

```
#############  
# DEPLOYMENT     
#############  
apiVersion: apps/v1    
kind: Deployment  
metadata:  
 name: web-d  
spec:  
 selector:   #permite seleccionar un conjunto de objetos que cumplan las condicione  
   matchLabels:  
     app: web  
 replicas: 2 # indica al controlador que ejecute 2 pods  
 template:   # Plantilla que define los containers  
   metadata:  
     labels:  
       app: web  
   spec:  
     containers:  
     - name: apache  
       image: practica:v1.0.0
       ports:  
       - containerPort: 80  
---  
  
#############  
# SERVICIO     
#############  
apiVersion: v1  
kind: Service  
metadata:  
 name: web-svc  
 labels:  
    app: web  
spec:  
 type: NodePort  
 ports:  
 - port: 80  
   nodePort: 30002  
   protocol: TCP  
 selector:  
    app: web
```

### Ejecutar 

```
kubectl apply -f completo.yaml
```

Como sabe .yml donde comienza el otro objeto?
Para saber donde comienza otro objeto dentro del .yaml se coloca "---" y seguimos con el otro objeto.

### Verificar despliegue y servicio

Primero debemos saber cual es la **IP** de nuestro cluster

```
minikube ip
```

Ahora debemos conocer cual es el **PUERTO** del servicio por el que lo estamos exponiendo al exterior

```
kubectl get svc
```

Finalmente abrimos nuestro navegador
```
<IP de minikube>:<puerto del servicio>
http://192.168.49.2:30002/
```

### Eliminar
```
kubectl delete -f completo.yaml
```

## Error
Despues de ejecutar el .yaml tubimos un error por que la imagen no estaba en un repositorio para que sea descargado.
Crei que por estar en local este lo iba a sacar de ahi, pero el cluster necesita tenerlo en su local (cluster) y no en el host (mi equipo).

## Posibles soluciones
1. Subir nuestra imagen a [docker hub](hub.docker.com)

```
docker tag practica:v1.0.0 jorhak/practica:v1.0.0
docker push jorhak/practica:v1.0.0
```

Ahora debemos reemplazar la imagen
```
   spec:  
     containers:  
     - name: apache  
       image: jorhak/practica:v1.0.0
       ports:  
       - containerPort: 80  
```

Debemos volvera a Ejecutar.

2. La otra opcion es empaquetar la imagen en un .tar para llevarla al cluster y cargarla.

```
docker save -o practica_v1.0.0.tar practica:v1.0.0
```

Ya que tenemos el comprimido lo que debemos hacer es cargala en el cluster.

```
/usr/local/bin/minikube image load practica_v1.0.0.tar
#O
minikube image load practica_v1.0.0.tar
```

Listar imagenes

```
/usr/local/bin/minikube image ls
#O
minikube image ls
```

El nombre que nos salga debemos reemplazar. 

```
   spec:  
     containers:  
     - name: apache  
       image: docker.io/library/practica:v1.0.0
       ports:  
       - containerPort: 80 
```

Debemos volver a Ejecutar.

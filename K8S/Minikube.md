# Version de Minikube
```
minikube version
```

# Asignar runtime
```
minikube start # toma por defecto docker
minikube start --driver=docker
minikube start --driver=virtualbox
minikube start --driver=vmware...
```

Podemos especificar en runtime o en todo caso Minikube va detectar por defecto a docker.

# Comandos de Minikube
Nos mostrara los comandos que podemos utilizar con minikube.
```
minikube
```

# Ver el estado de Minikube
```
minikube status
```

# Ver los logs de Minikube
```
minikube logs
```

# Ver la IP de Minikube
```
minikube ip
```

# Acceder a Minikube
Ya que solo tenemos en un solo nodo todo: control plane , worker node.
```
minikube ssh
```

# Directorios de Minikube
```
# ~/ es el directorio home de nuestro usuario
~/.kube
~/.minikube
```

El fichero que existe en _~/.kube_ es config que contiene la configuracion de conexion al cluster de minikube, esto nos permitira poder conectarnos a otrso cluster. Mas adelante vamos a ver esto.

En el directorio _~/.minikube_ existe un fichero que me indica todos los cluster de minikube que estoy utilizando _~/.minikube/machines_. En este caso por ahora solo tenemos uno que es el que creamos con **minikube start**

# Como crear otro cluster de minikube

## Listar los cluster de minikube
```
minikube profile list
```

## Crear cluster con dos nodos
```
minikube start --driver=docker -p clusterDesa -nodes=2
```

## Eliminar cluster
```
minikube delete -p clusterDesa
```

## Configurar memoria del cluster de minikube
```
minikube config set memory 4G -p minikube
```

-p <nombre_del_cluster> con este flag indicamos a que cluster le vamos hacer la configuracion suponiendo que tengamos otros cluster. Previo debemos listar los cluster para saber el nombre.
Luego de ejecutar el comando nos pedira eliminar el cluster y volver a inicializarlo para que tome los nuevos cambios, esto porque el container que creamos tiene configuraciones y para ello debemos hacer lo que ya mencionamos y el nuevo container tomo esas configuraciones.

## Ver la configuracion del recurso memoria
```
minikube config get memory
```

## Con que cluster estoy trabajando
```
minikube profile
```
Nos indica con que cluster estamos trabajando. Otra forma de saber cuantos cluster hay es dirigirnos al directorio
```
~/.kube
nano config
```

Y veremos los cluster que tenemos a nuestra disposicion. En el fichero vamos a ver una key:value
```
current-context: minikube
```
La que nos indica que estamos trabajando con ese cluster.

## Cambiar de cluster
```
minikube profile clusterDesa
```

## Verificar que se cambio
```
minikube profile
```

## Listar los nodos del cluster
```
kubectl get nodes
```

## Dashboard Web
```
minikube dashboard
```
Se nos va abrir una pagina web en donde vamos a poder dejar trabajar sobre nuestro cluster de k8s.

# Runtime
Hemos utilizado hasta ahora Docker como runtime, sin embargo, K8s nos deja elegir el container runtime que deseamos utilizar.
K8s ya no viene por defecto con Docker como runtime. Minikube tambien tiene esta opcion aunque algo restrictivo ya que es de un tercero y nos debemos limitar a las opciones que tiene.

## Iniciar un clustar con un runtime distinto a docker
```
minikube start --container-runtime=cri-o -p cluster2
```

## Ver que se creo 
```
minikube profile list
```

## Borrar cluster
```
minikube profile list
minikube delete -p clusterDesa
```
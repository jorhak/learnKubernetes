# Introduccion
_Kubeconfig_ es un nombre generico, en realidad en nombre es _config_ nos referimos a el como fichero de configuracion de K8s o _kubectl_ que es la herramienta con la que vamos a manejar realmente.

### Que tiene este fichero?
es un fichero que utilizamos para determinar como me conecto a un determinado cluster de K8s, con que credenciales, donde se encuentra el servidor, etc. Fichero de tipo yaml

### Donde se encuentra este fichero?
Con el comando:
```
kubectl --kubeconfig
```

Ahora si utilizamos:
```
kubectl get pod/ejemplo --kubeconfig /home/casa/.kubeconfig/config
```
Lo que hace es conectarse a ese cluster que tiene esa configuracion. Y no al nuestro que esta local.

Puedo tener mas de un fichero kubeconfig, por decir, para mi entorno de Desarrollo, Produccion.

Una de las formas para que no ejecute la configuracion local es la que vimos previamente.

Variable de entorno **$KUBECONFIG** con esto le puedo indicar donde ir a buscar el fichero de configuracion _kubeconfig_.

### Donde suele encontrarse?
1. Linux
```
cat ~/.kube/config
```

2. Windows
```
%USERPROFILE%\.kube\config
```

3. Mac
```
cat ~/.kube/config
```

## Que contiene este fichero
Este fichero contiene informacion que nos permite manejar o conectarnos a un cluster como puede ser el:
- Certificado
- Servidor
- Nombre
- Usuario
- Token de usuario

# Como ver el kubeconfig
Desde su ubicacion desde la terminal

```
nano ~/.kube/config
```

Desde _kubectl_
```
kubectl config view | grep current
kubectl config current-context
```

### Cambiar de contexto
```
kubectl config use-context <contexto>
```

# Incorporar o modificar un cluster
Lo podemos hacer de dos formas entrando en el fichero y modificarlo o con _kubectl config set-cluster_.
En nuestro caso vamos a usar la linea de comandos para evitar un error al momento de modificar el fichero. Si nos llegamos a equivocar la linea de comandos va a protestar.
Si ya existe lo modifica y si no lo crea.

Crear conexion con cluster en el fichero por defecto
```
kubectl config set-cluster cluster2 --server=https://1.2.3.4
```

Crear conexion con el cluster en un fichero especifico
```
kubectl config --kubeconfig=config-alternativo set-cluster cluster2 --server=https://1.2.3.4
```

Agregar certificado
```
kubectl config set-cluster cluster2 --certificate-authority=/home/hola/cert.crt
kubectl config --kubeconfig=config-alternativo set-cluster cluster2 --certificate-authority=/home/hola/cert.crt
```

## Obtener pod del cluster
Vamos a obtener de ese cluster del cual acabamos de agregar su configuracion para poder acceder.
```
kubectl --kubeconfig config-alternativo get pods
```

## Agregar credenciales
```
kubectl config --set-credentials usu1 --username=usu1 --password=<base64>
```

## Agregar certificado
```
kubectl config --set-credentials usu2 --client-certificate=/home/hola/fichero.crt
kubectl config --set-credentials usu2 --client-key=/home/hola/fichero.key
```

## Agregar contexto
```
kubectl config set-context contexto-cluster --cluster=cluster2 --user=usu1 --namespace=desarrollo
```

#### Cambiar de contexto
```
kubectl --kubeconfig=config-alternativo config use-context contexto-cluster2
```

#### Probar
```
kubectl --kubeconfig=config-alternativo get pods
```
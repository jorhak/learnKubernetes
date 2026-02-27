Vamos a crear un secreto por medio de un fichero, en este caso la clave va ser el nombre del fichero y el valor el contenido del fichero.

Lo que se va hacer sera injectar este fichero para que tomo el contenido como su valor.

# WorkSpace
```
cd /home/jon/Documents/kubernetes/VARIABLES,\ CONFIGMAPS\ Y\ SECRESTS/secretDesdeFicheros/
```

# Crear secret
```
k create secret generic datos --from-file=datos.txt
k describe secret datos
k get secret datos -o yaml
```

## Verificar secret
```
k get secret
```

# Ejecutar pod
```
kapp pod1.yaml
```

## Veriricar que el pod fue creado
```
kgp
```

## Ingresar al pod
```
k exec pod1 -it -- bash
env
echo $DATOS | od -c
exit
```

Podemos ver el contendio que esta en el fichero, solo que ahora lo tiene como variable de entorno:
```
KUBERNETES_PORT_443_TCP_PROTO=tcp  
KUBERNETES_PORT_443_TCP_ADDR=10.96.0.1  
DATOS=hola vamos a ver  
como funciona un  
secret desde un fichero  
  
KUBERNETES_SERVICE_HOST=10.96.0.1  
KUBERNETES_PORT=tcp://10.96.0.1:443
```

- Con el comando: echo $DATOS | od -c 
  Nos muestra por que tenemos un salto de linea y es algo que debemos tomar en cuenta.
# Eliminar pod
```
kdel pod1.yaml
```

# Eliminar secret
```
k delete secret datos
```

En el contorno externo no puedo ver el contenido del secret, hasta que injeto el secret en el container.
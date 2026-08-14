# WorkSpace
```
cd /home/jon/Documents/kubernetes/VARIABLES,\ CONFIGMAPS\ Y\ SECRESTS/s  
ecretDeclarativos/
```

Crear secretos de forma declarativa, vamos a ver que hay dos formas de generar los secretos. En los ejemplos previos hemos dejado que el propio K8s generara la codificacion en base64.

- Crear el secret automaticamente todo
- Crear el secrte con encriptacion manual

# Codificar en base64
```
echo -n "usu1" | base64
echo -n "password-usu1" | base64
```

## Editar secreto1.yaml
Esto valores son lo que vamos a colocar en 
```
data:
  usuario1: xxxxxx
  usu1-pass: xxxxxx
```

- Al colocar _data_ le tenemos que pasar los datos en base64.
## Ejecutar
```
kapp secreto1.yaml
```

# Codificar automaticamente
## Editar secreto2.yaml
```
stringData:
  usuario2: 'usu2'
  usu2-pass: 'password-usu2'
```

- Al colocarle _stringData_, le estoy pidiendo a K8s que codifique en base64 y se la pase al contenedor.

Ahora esta ya en mis manos si lo uso de una u otra manera.
- En la primera primero lo paso codificado en base64
- En la segunda dejo que K8s lo codifique, sin embargo, si alguien accede al fichero podra conocer los valores.

## Ejecutar
```
kapp secreto2.yaml
```

# Crear pod
```
kapp pod1.yaml
```

# Verificar que se crearon los secrets
```
k get secret
```

## Ver contenido de los secrets
```
k describe secret secreto1
k describe secret secreto2
k get secret secreto1 -o yaml
k get secret secreto2 -o yaml
```

# Verificar pod
```
kgp
```

## Ingresar al pod
```
k exec -it pod1 -- bash
env
```

# Eliminar objetos
```
kdel pod1.yaml
kdel secreto1.yaml
kdel secreto2.yaml
```
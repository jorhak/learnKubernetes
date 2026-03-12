Credenciales con las que me puedo conectar a un repositorio privado, registro privado de imagenes de docker.
Cuando trabajamos con DockerHub el cual es un repositorio publico por lo cual tenemos acceso a las imagenes sin problemas.

Que pasa cuando intento acceder a un repositorio que me pide usuario y contrasena?

De igual modo si intento acceder a un registro de imagenes.

De alguna forma me tengo que autenticar y para evitar que me pregunte y tenga que ingresar mis credenciales vamos a utilizar un **Secret Docker**.

Vamos a crear nos un repositorio privado en **DockerHub** para realizar la prueba.

1. WorkSpace
```
cd /home/jon/Documents/kubernetes/VARIABLES,\ CONFIGMAPS\ Y\ SECRESTS/secretDocker/
```

2. Crear **Pod**:
```
kapp pod-secret-docker.yaml
```

3. Verificar **Pod**
	Vamos apreciar que no se a podido crear el pod debido a un problema con la imagen, ya que necesitamos los credenciales para poder descargarla.
```
kg pod/ejemplo
kd pod/ejemplo
```

4. Eliminar **Pod**:
```
kdel pod-secret-docker.yaml
```

5. Crear **secret docker**:
```
k create secret docker-registry midocker \
  --docker-server=docker.io \
  --docker-username=jorhak \
  --docker-password= \
  --docker-email=00amaterasu16@gmail.com
```

5. Modificar fichero _pod-secret-docker.yaml_
	Debe estar a la altura de _containers_. Podemos colocar mas de un secret docker si en caso tubieramos mas de una imagen.
```
imagePullSecrets:
  - name: midocker
```

6. Ejecutar fichero
	Volvemos a ejecutar los pasos 2 y 3.
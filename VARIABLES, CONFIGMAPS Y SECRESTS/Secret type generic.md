# Creando un secret generico
```
kubectl create secret generic \
   passwords \
   --from-literal=pass-root=kubernetes \
   --from-literal=pass-usu=kubernetes
```

# Verificar que se creo el secret
```
kubectl get secrets
```

# Obtener la informacion
```
kubectl get secret passwords -o yaml
```

### Configmap
Vamos a combinar configmap y secret. En la ruta vamos a tener el configmap:
```
cd /home/jon/Documents/kubernetes/VARIABLES,\ CONFIGMAPS\ Y\ SECRESTS/secretGeneric/
```

```
kubectl apply -f datos-mysql-env.yaml
kubectl get cm
kubectl describe cm datos-mysql-env
```

### Modificar mysql.yaml
```
nano mysql.yaml
```

```
env:
  - name: MYSQL_ROOT_PASSWORD
    valueFrom:
      secretKeyRef:
        name: passwords  ##Nombre del secret
        key: pass-root   ##Key
  - name: MYSQL_ROOT_PASSWORD
    valueFrom:
      secretKeyRef:
        name: passwords  ##Nombre del secret
        key: pass-usu    ##Key
```

Lo que vemos aqui es que le podemos pasar a las variables de entorno un secreto, de igual modo que en los configmaps.

# Ejecutar 
```
kapp mysql.yaml
```

## Ver pod
```
kgp
```

## Acceder al pod
```
kexec mysql-deploy-6b6cc84bf5-nzs2j -- bash
env
exit
```

Ahora puedo ver el contenido de mis variables de entorno dentro del contenedor, pero no fuera del contenedor porque los tengo en base64. Las propiedades estan ocultas y han llegado perfectamente al container.

## Eliminar mysql.yaml
```
kdel mysql.yaml
```

## Eliminar secret
```
k delete secret passwords
```

## Eliminar configmap
```
kdel datos-mysql-env.yaml
```
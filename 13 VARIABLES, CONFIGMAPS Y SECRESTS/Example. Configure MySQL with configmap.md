Antes que nada debemos ubicarnos en la ruta
```
cd /home/jon/Documents/kubernetes/VARIABLES, CONFIGMAPS Y SECRESTS/ejemploCofigurarMySQLConConfigMaps
```

Vamos a cargar las variables de entorno a traves de un configMap.
## Ver fichero de configMap
```
cat datos-mysql-env.yaml
```

## Crear configMap
```
kubectl apply -f datos-myswl-env.yaml
```

## Verificar la creacion del configMap
```
kubectl get cm
```

## Ver la configuracion del deploy
Aqui es donde vamos a cargar nuestro configMap. En el bloque **env** hemos definido las cuatro varibles que vamos a utilizar para cargar dentro del MySQL que van a ser:
- El nombre que le doy a la variable que le voy a pasar al contenedor
- De donde la optiene **valueFrom** -> **configMapKeyRef** -> el configMap tiene el nombre **datos-mysql-env** en donde hay una clave **MYSQL_ROOT_PASSWORD** que es la que recupera ese valor. Y ser repite para las otras variables.
Hay un dato muy importante que la **Key** que se tiene en el **configMap** no es igual a la que se quiere pasar al contenedor. Por ejemplo en el **configMap** la key es MYSQL_PASSWORD y la key que espera el contenedor es MYSQL_ROOT_PASSWORD, es por eso que utilizamos este metodo. Dado que aqui nos permite hacer ese cambio.
```
vi mysql.yaml
```

## Crear deploy
```
kubectl apply -f mysql.yaml
```
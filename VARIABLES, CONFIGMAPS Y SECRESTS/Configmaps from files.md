Cargar configmap con ficheros pero tenemos que tener especial cuidado porque no es lo mismo cargar ficheros para cargar datos en mi _pod_, que para cargar variables de entorno.
En nuestro caso en particular para nuestro MySQL vamos a cargar variables de entorno.
Tengo un fichero _datos_mysql.properties_ que quiero que se incorporen a mi _pod_ a mi contenedor MySQL, para que se cargen automaticamente.

```
kubectl create configmap datos-mysql --from-file=datos_mysql.properties
kubectl get cm
```

Aqui vemos que nos lo a cargado como si fuera un solo valor lo cual no nos sirve, sin embargo, para otros escenarios si nos serviria.
```
kubectl describe cm datos-mysql
```

Aqui lo que vemos es la 
clave 
datos_mysql.propeties 

Y el valor es:
MYSQL_ROOT_PASSWORD=
MYSQL_USER=
MYSQL_PASSWORD=
MYSQL_DATABASE=

Esto no me satisface la necesidad de que me pase las cuatro de forma independiente para usarlas.

```
kubectl apply -f pod1.yaml
kubectl exec -it pod1 bash 
printenv
echo $DATOS_MYSQL
```

Vamos a ver que nos vota como valor todas las varibles y eso no es lo que queremos. Contiene el contenido del fichero.
No sirve para cargar varibles de entorno, pero si para otras cirscunstancias, por decir, si necesitamos un .json dentro de nuestro contenedor este seria un buen escenario para utilizarlo.

```
kubectl get cm datos-mysql -o yaml
```

Aqui podemos ver que solo tenemos un solo dato que contiene el contenido del fichero.


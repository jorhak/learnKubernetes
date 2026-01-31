Que paso si el numero de variables es muy grande, este pude llegar a ser difil de manejar, ya que tendriamos que meter todas las varibles dentro de _env:_.
Lo ideal seria tener un fichero adicional del cual poder cargar los datos y que se pudieran incorporar dentro del environment de un contenedor de un _pod_.
Ese objeto es ConfiMap, los mapas de configuracion no son nada mas que ficheros que nos van a permitir incorporar este conjunto de propiedades, propiedades:valor; propiedades:valor;..... de una manera sencilla.

# Atraves del comando imperativo create
```
kubectl create configmap cf1 --from-literal=usuario=usu1 --from-literal=password=pass1
```

# Verificar la creacion del configmap
```
kubectl get cm
kubectl get cm -o wide
kubectl describe cm cf1
kubectl get cm cf1 -o yaml
```

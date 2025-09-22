Vamos a ver el seguimiento y control de eventos, hay que tener en cuenta que lo que se hace, todo lo que se genera dentro de un namespace va tener como finalidad o fin algun evento que indique los procesos que se han hecho con ese objeto. Por ejemplo si se crea un _pod_ en donde se van a generar una serie de eventos: creacion, bajada de imagen, etc.

# Crear namesapce
```
kubectl create namesapce desarrollo
```

# Asignar namespace por defecto
```
kubectl config --set-context --current --namespace=desarrollo
```

Como puedo ver los eventos que se generran en esta namespace?
```
kubectl get events --namespace desarrollo
```
No me devuelve nada porque es una namespace recien creada.

# Crear pod
```
kubectl run apache1 --image=httpd
kubectl get pods
```

Ahora si volvemos a ver los eventos de este namesapce, se veran los objetos que se han creado en el namespace.

```
kubectl get events --namespace desarrollo
```

En este caso coinciden efectivamente con los que van aparecer dentro del _pod_.
```
kubectl describe pod apache1
```

Debemos tener en cuenta que esto puede causar errores, supongamos que me equivoco, esto me va dar un error pero va lanzar, crear el _pod_.
Vamos a ver un ErrImagePull
```
kubectl run apache2 --image=httpd1
kubectl get pod
```

Vamos a ver los eventos que se generaron
```
kubectl get events --namespace desarrollo
kubectl describe pod apache2
```

## Buscar eventos por tipo
Podemos hacer varios filtros
```
kubectl get events --field-selector type="Warning"
kubectl get events --field-selector reason="Scheduled"
```

Que se ejecute en segundo plano
```
kubectl get evetns --namespace desarrollo -w
```

Abrimos otra terminal y vamos a observar que en la terminal previa se van a estar viendo los eventos que se estan ejecutando.
```
kubectl run apache3 --image=hpptd
kubectl get events --field-selector reason=Failed --namespace desarrollo -w
```
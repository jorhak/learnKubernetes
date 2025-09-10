Como sabe el servico a donde debe ir?
```
kubectl describe svc apache1
```

En la salida vamos a ver _Endpoints_ nos va mostar una **IP**. Ahora si listamos los **pods**
```
kubectl get pod -o wide
```

Ahora podemos ver que el _Endpoints_ apunta a la **IP** del **pod**.

El _service_ esta utilizand _selector_ para poder saber a que **pod** apuntar.
```
kubectl get pod <nombre del pod> --show-labels
```
De esta forma el _service_ conoce al _pod_.

Que paso si yo escalo el **deployment**
```
kubectl scale deploy apache1 --replicas=3
kubectl get pods -o wide
```

Ahora cada _pod_ tiene su propia direccion **IP**, ahora si yo _service_ voy a ver que se agregaron esas **IP's**.
```
kubectl describe svc apache1 
```

Ahora si yo elimino un _pod_, el _deploy_ se encarga de gestionar que se cree un _pod_ ya que en la especificacion dice que se espera que tenga creado tres _pods_, por lo cual crea un nuevo _pod_ con una **IP** diferente. Cuando se elimina un _pod_ o este llega a fallar este no se revive, es por eso que se tiene un nuevo _pod_ con una nueva **IP**.

Por eso que el _service_ en los **Endpoints** quita la **IP** del _pod_ eliminado y agrega la nueva **IP** del _pod_ que se creo gracias a que se cumple con el estado deseado de _pods_ que se requieren el el _deploy_.

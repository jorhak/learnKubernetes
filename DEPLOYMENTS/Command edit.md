Si no llegaramos a tener el fichero .yaml podemos utilizar _edit_ para editar cuarlquier objeto del cluster.
Cuando hagamos el cambio debemos guardarlo en nuestro control de version ya que esto no se recomienda hacer en _produccion_, sin embargo en ocasiones se lo puede hacer en _desarrollo_.

## Editar deployment
```
kubectl edit deploy nginx-d
```
Se abrira el editor predeterminado (nano, vi, edit)
## Verificar cambios
```
kubectl get deploy nginx-d
```

## Obtener el deployment en formato yaml
```
kubectl get deploy nginx-d -o yaml
```
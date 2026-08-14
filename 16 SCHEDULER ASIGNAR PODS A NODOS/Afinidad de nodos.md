Hay dos tipos de afinidad:
- Afinidad de nodos: que identifica los nodos que son candidatos a que se les asigne un pod.
- Afinidad inter pod: que esta asociada a como se juntan los pod dentro de los nodos.

La afiniad de nodos es parecida a nodo selector pero mas sofisticado, con muchas mas reglas y mas condiciones. Es una forma mas granular que el node selector. Incluir reglas de distintos tipos.

# Ejemplo de afinidad de nodos
## Workspace
```
cd ~/Documents/kubernetes/16\ SCHEDULER\ ASIGNAR\ PODS\ A\ NODOS/recurso_afinidad_nodos
```

```
vi pod_affinity.yaml
```

Niguno de nuestros nodos tiene las etiquetas que necesita nuestro pod, por eso no se va a poder crear el pod hasta que un nodo o nodos tenga esa etiqueta.
# Crear pod
```
kubectl apply -f pod_affinity.yaml
```
# Ver si se creo el pod
```
kubectl get pods -o wide
```
Como vemos no esta encontrando ningun nodo que cumpla con esa condicion.
# Ver las caracteristicas del pod
```
kubectl describe pod apache1
```
En eventos vamos a ver que dice: de los 6 nodos hay 0 disponibles.
# Modificar uno de los nodos
Vamos a modificar un nodo para que tenga esa afinidad.
```
kubectl get nodes
kubectl label node ip-172-31-4-215.us-west-2.compute.internal equipo=desarrollo-web
```
# Verificar que se creo el pod
Ahora podemos ver que si se creo el pod
```
kubectl get pods -o wide
```

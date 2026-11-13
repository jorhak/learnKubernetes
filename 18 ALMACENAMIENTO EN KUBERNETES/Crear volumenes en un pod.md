# Workspace
```bash
cd /home/jon/Documents/kubernetes/18 ALMACENAMIENTO EN KUBERNETES/recursos/volumen_pod
```
Vamos a crear volumenes locales en nuestro entorno mas adelante veremos otros tipos de volumenes.
Vamos a ver una nueva clausula **volumeMounts** donde vamos a indicar que directorios se van a montar dentro del contenedor para albergar la asociacion del volumen del contenedor y el espacio fisico de fuera (nuestro control plane o worker node).
- mountPath: En que directorio se va montar
- name: Nombre del volumen

Los **volumeMounts** que tiene el contenedor asosciado deben estar mapeados con la clusua **volumes**, vamos a traducirlos en la forma en la que deben comportarse.
- name: Es el nombre del volumen y debe ser el mismo que se encuentra en **volumeMounts**
- hostPath: Tipo del volumen, este volumen va estar asociado a un directorio de nuestro: control plane, worker node o minikube. Lo que quiere decir es que todo lo que tenga el contenedor en su directorio (mountPath) se va ver reflejado en hostPath. No se recomiendo utilizar hostPath para ambientes de QA, PROD porque con este tipo de volumen se crea un espacio en el control plane o worker node y si se crean otros pods en otros worker node estos no van a poder llevar al volumen es por eso que solo se recomienda usarlos en DEV, pruebas.
- path: A pesar de K8s puede crear el directorio, yo debe crear el directorio en todos los worker nodes para evitar posibles errores, tambien porque no se sabe en que worker node se va asociar el volumen.

En el volumen de git lo que hacemos es hacer un clone y no lo vamos a poder modificar porque le colocamos ReadOnly: true.

En el volumen de temp utilizamos un volumen de tipo temporal, es decir, que cuando se elimine el pod ese volumen va a desaparecer.
# Ejecutar
```bash
kubectl apply -f volumen.yaml
kubectl get pods
kubectl describe pod volumenes
```
# Eliminar
```
kubectl delete -f volumen.yaml
```
Hemos eliminado el pod, sin embargo, el volumen path sigue persistiendo los datos, si vuelvo a crear el pod y este es creado en otro worker node es en este mismo donde va crear el volumen.
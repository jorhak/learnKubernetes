Que aporta el almacenamiento dinaminco?
De finimos una clase de almacenamiento en esa clase definimos el provisioner, es decir, el proveedor que va facilitar ese almacenamiento. Luego de definir el proveedor defino una clase sobre ese tipo. Y luego todos los volumenes que asocie a esa clase van a estar asociados a ese tipo de almacenamiento.
# Workspace
```bash
cd /home/jon/Documents/kubernetes/19 STORAGE CLASS/recursos
```
# Crear Storage Class
```bash
kubectl apply -f storage-class.yaml
kubectl get sc
kubectl describe sc bbdd
```
# Crear PV
```bash
kubectl apply -f pv.yaml
kubectl get pv
```
Vamos a crear otro PV
```bash
kubectl apply -f pv1.yaml
kubectl get pv
```
Van a pertenecer a la misma Storage Class con diferentes capacidades de almacenamiento.
# Crear PVC
```bash
kubectl apply -f pvclaim.yaml
kubectl get pvc
```
Nos va salir en Pending porque no hemos creado un pod que vaya a utilizar ese PVC. Tener claro que cuando se crea un PV y luego se crea un PVC que vaya a utilizar una clase este no se asigna inmediatamente porque tenemos una propiedad **volumeBindingMode: WaitForFirstConsumer** (esperar al primer consumidor), que lo que quiere decir es que no se lo va asignar hasta que se tenga un _pod_ que lo vaya a utilizar. Y como vimos hemos creado dos PV que utilizan la misma SC, cuando creemos el _pod_, este va tener dos opciones para elegir eso es lo que lo vuelve dinamico porque al tener dos PV en un SC este va elegir el que se adecue mejor a su requerimiento.
# Crear POD
```bash
kubectl apply -f postgres.yaml
kubectl get pvc
kubectl get pv
```
Vamos a ingresar donde se creo el volumen
```bash
kubectl get pod -o wide
ssh esclavo1
sudo ls /tmp/bbdd-vol2
```
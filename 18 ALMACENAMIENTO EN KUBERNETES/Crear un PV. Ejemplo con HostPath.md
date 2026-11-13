# Workspace
```bash
cd /home/jon/Documents/kubernetes/18 ALMACENAMIENTO EN KUBERNETES/recursos/hostPath
```
Vamos a crear un PV para luego crear un PVC y por ultimo un POD que consuma todos esos recursos, lo vamos hacer con hostPath que es de tipo local, tipo que no debemos utilizar en PROD.
No hay ningun comando para crear un PV.

Para que un PV esta asociado un PVC vamos a utilizar STORAGE CLASS, vamos a usar la property _storageClassName_ y se le va asignar un nombre, lo importante es que este nombre coincida con el de PVC, esta vendria a ser la forma estatica de relacionar un PV con un PVC.
No creamos un _storageClassName_ sino que debe coincidir con el nombre del PVC, de esta forma estoy relacionando de forma directa un PV con un PVC.

El tipo de driver que vamos a utilizar es _hostPath_, crea un directorio dentro de la maquina local. El servidor donde vaya a para el pod va a reclamar el espacio.

No se recomienda usar _hostPath_ en produccion porque al crear varios _pods_ estos pueden ir a parar en distintos worker nodes y crear los directorios por lo que vamos a tener informacion dispersa, esto es perjudicial porque si se registra un usuario este se lo crea en el pod al cual ingreso, y ahora si vuelve y se quiere logearse debe ingresar al mismo nodo porque de lo contrario no va encontrar su informacion.

En un ambiente de PROD los _pods_ deben ver lo mismo, por lo cual el almacenamiento debe ser compartido.
# Crear PV
```bash
kubectl apply -f pv.yaml
kubectl get pv
kubectl describe pv pv-volume
```
El directorio se crea recien cuando se crea el _pod_, porque por ahora no sabemos en que nodo se va a crear nuetro pod.
Repositorio de Metrics Server: github.com/kubernetes/sigs/metrics-server
Este laboratorio se realizo con el proveedor AWS. Se crearon Instancias: un Control Plane y dos Nodes Worker.
# Ver cuantos nodos tenemos
```
kubectl get nodes
```
# Verificar si tenemos instalado Metrics Server
```
kubectl top nodes
```
# Instalar Metrics Server
```
kubectl apply -f <URL la sacamos de la documentacion>
```
Los objetos que nos importan en este momento son: service/metrics-server y deployment.apps/metrics-server
Metrics Server se instalo en el namespace de **kube-system**
# Ver el service
```
kubectl get svc metrics-server -n kube-system
```
# Ver el deploy
```
kubectl get deploy metrics-server -n kube-system
```
Vemos que nuestro deploy no se esta ejecutando
## Verificar porque nos e esta ejecutando
```
kubectl get pods -n kube-system
```
Vemos que tenemos un CrashLoopBackOff
```
kubectl describe pod metrics-server-sdhfsd-shdfls -n kube-system
```
Este error se debe  a que no estamos cumpliendo con uno de los cinco requisitos que vimos en la documentacion.
# Vamos a solucionar estos errores
## Descargar el fichero de instalacion
```
mkdir metrics-server && cd metrics-server
wget <URL la sacamos de la documentacion>
```
## Modificamos el fichero
```
nano components.yaml
```
Nos vamos a dirigir al Deployment que esta abajo de Service. Y nos dirigimos a **args** y modificamos
```
- args:
  - --cert-dir=/tmp
  - --secure-port=4443
  - --kubelet-insecure-tls
  - --kubelet-preferred-address-types=InternalDNS,InternalIP,ExternalDNS,ExternalIP,Hostname
  - --kubelet-use-mode-status-port
  - --metrics-resolutions=30s
```
Debajo de **nodeSelector** agregamos
```
nodeSelector:
  kubernetes.io/os: linux
hostNetwork: true   #AGREGAR
```
# Aplicar cambios
## Eliminar deploy
```
kubectl delete deploy metrics-server -n kube-system
```
## Aplicamos los cambios
```
kubectl apply -f components.yaml
```
## Verificar que se creo correctamente
```
kubectl get pods -n kube-system
```
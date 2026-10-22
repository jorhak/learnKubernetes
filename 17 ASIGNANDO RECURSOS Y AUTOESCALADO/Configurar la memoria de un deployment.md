Vamos a ver como colocarle recursos de memoria a un pod o aun conjunto de pods que pertenecen aun deployment. Esto es valido tanto para deployment y pod.
Quien debe tener los recursos es el pod ya que un deployment es una estructura logica.
# Workspace
```
cd /home/jon/Documents/kubernetes/17 ASIGNANDO RECURSOS Y AUTOESCALADO/recursos
```
# Crear deploy con pod que tienen recursos especificos
```
kubectl apply -f deploy_nginx.yaml
```
# Ver que se asignaron los recuros
```
kubectl edit deploy nginx-d
```
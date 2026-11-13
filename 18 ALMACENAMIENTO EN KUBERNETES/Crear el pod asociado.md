# Workspace
```bash
cd /home/jon/Documents/kubernetes/18 ALMACENAMIENTO EN KUBERNETES/recursos/hostPath
```
# Crear pod
```bash
kubectl apply -f pod-pvc.yaml
kubectl get pod -o wide
kubectl describe pod pv-pod
```
# Listar nodos
```bash
kubectl get nodes
```
# Ver donde se creo el pod
```bash
kubectl get pods -o wide
```
# Ingresar al nodo
```bah
minikube ssh -p cluster1 -n cluster1-m02
cd /mnt
ls
ls data
exit
```
Si ahora ingreso a otro nodo no vamos a var el directorio data
```bash
minikube ssh -p cluster1 -n cluster1-m03
cd /mnt
ls
```
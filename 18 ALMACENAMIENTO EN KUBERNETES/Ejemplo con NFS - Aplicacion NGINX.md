# Workspace
```bash
cd /home/jon/Documents/kubernetes/18 ALMACENAMIENTO EN KUBERNETES/recursos/nginx_nfs
```
# Desplegar PV (zona de almacenamiento)
```bash
kubectl apply -f pv-nfs.yaml
kubectl get pv
```
# Desplegar PVC
```bash
kubectl apply -f pvc-nfs.yaml
kubectl get pvc
```
# Desplegar POD
```bash
kubectl apply -f pod-nfs.yaml
kubectl get pods
kubectl describe pod pod-nfs
```
# Verificar
```bash
kubectl proxy
```
Abriimos navegador: localhost:8081/api/v1/namespaces/default/pods/pod-nfs/proxy
```bash
kubectl get pods -o wide
```

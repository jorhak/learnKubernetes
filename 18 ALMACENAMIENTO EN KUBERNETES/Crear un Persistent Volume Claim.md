# Workspace
```bash
cd /home/jon/Documents/kubernetes/18 ALMACENAMIENTO EN KUBERNETES/recursos/hostPath
```
# Crear PVC
```bash
kubectl apply -f pvclaim.yaml
kubectl get pvc
kubectl get pv
kubectl describe pvc pv-claim
```
Los PV no estan asociado a un namespace, son globales, no pertenecen a ninguna namespace.
Los PVC son creados en el namespace que se encuentra, podemos decir que los PVC son locales y los PV son globales.

# Workspace
```bash
cd /home/jon/Documents/kubernetes/18 ALMACENAMIENTO EN KUBERNETES/recursos/WordPressMysql
```
# Crear directorios en Control Plane
```bash
mkdir -p ~/datos/mysql
mkdir -p ~/datos/wordpress
```
# Configurar NFS
```bash
sudo vi /etc/exports
```

```
/home/kubernetes/datos/mysql *(rw,sync,no_root_squash,no_all_squash)
/home/kubernetes/datos/wordpress *(rw,sync,no_root_squash,no_all_squash)
```
## Reiniciar servicio
```bash
sudo systemctl restart nfs-kernel-server
```
# Crear directorios en Worker Nodes
```bash
mkdir -p ~/datos/mysql
mkdir -p ~/datos/wordpress
```
## Montar directorios NFS
```bash
mount -t nfs 192.168.0.32:/home/kubernetes/datos/mysql /home/kubernetes/datos/mysql

mount -t nfs 192.168.0.32:/home/kubernetes/datos/wordpress /home/kubernetes/datos/wordpress

df -h
```
# Desplegar PV Wordpress y PV MySQL
```bash
kubectl apply -f pv-wordpress.yaml
kubectl apply -f pv-mysql.yaml
kubectl get pv
```
# Desplegar PVC Wordpress y PVC MySQL
```bash
kubectl apply -f pvc-wordpress.yaml
kubectl apply -f pvc-mysql.yaml
kubectl get pv
kubectl get pvc
```
# Desplegar Wordpress y MySQL
```bash
kubectl apply -f wordpress-deployment.yaml
kubectl apply -f mysql-deployment.yaml
```
Verificar que el servicio de wordpress este en NodePort.
# Verificar
Abrimos nuestro navegador con la IP del Control Plane y el puerto del servico de wordpress vamos a ingresar a su interfaz de Wordpress.
# Escalar
```bash
kubectl get deploy
kubectl get pods -o wide
kubectl get svc
kubectl describe svc wordpress
```

```bash
kubectl scale --replicas=4 deploy/wordpress
kubectl get pods -o wide
kubectl describe svc wordpress
kubectl get deploy
kubectl get rs
kubectl scale --replicas=2 deploy-wordpress
kubectl describe deploy/workpress
```
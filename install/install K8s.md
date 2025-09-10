# Requisitos

## Control plane y worker nodes
```
cp1   192.168.0.10
wk1   192.168.0.11
wk2   192.168.0.12
wk3   192.168.0.13
```

## Configurar hostname y /etc/hosts
```
hostnamectl set-hostname cp1   # en el control plane
hostnamectl set-hostname wk1   # en worker1
```

En todos los nodos edita
```
192.168.0.10  cp1
192.168.0.11  wk1
192.168.0.12  wk2
192.168.0.13  wk3
```

## Deshabilitar SELinux (o ponerlo en permisivo)
```
setenforce 0
sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/' /etc/selinux/config
```

## Deshabilitar Swap
```
swapoff -a
sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab
```

## Habilitar módulos del kernel
```
cat <<EOF | tee /etc/modules-load.d/k8s.conf
br_netfilter
overlay
EOF

modprobe br_netfilter
modprobe overlay

cat <<EOF | tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables  = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward                 = 1
EOF

sysctl --system
```

# Firewall (firewalld)
## En el Control Plane
```
firewall-cmd --permanent --add-port=6443/tcp
firewall-cmd --permanent --add-port=2379-2380/tcp
firewall-cmd --permanent --add-port=10257/tcp
firewall-cmd --permanent --add-port=10259/tcp
firewall-cmd --reload
```

## En cada Worker
```
firewall-cmd --permanent --add-port=10250/tcp
firewall-cmd --permanent --add-port=30000-32767/tcp
firewall-cmd --reload
```

## Instalar containerd (runtime)
```
yum install -y yum-utils device-mapper-persistent-data lvm2

# Agregar repo de containerd
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

# Instalar containerd
yum install -y containerd.io

# Configuración
mkdir -p /etc/containerd
containerd config default | tee /etc/containerd/config.toml

# Cambiar en /etc/containerd/config.toml:
# SystemdCgroup = true
sed -i 's/SystemdCgroup = false/SystemdCgroup = true/' /etc/containerd/config.toml

systemctl enable --now containerd
```

## Instalar kubeadm, kubelet y kubectl
```
cat <<EOF | tee /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://pkgs.k8s.io/core:/stable:/v1.30/rpm/
enabled=1
gpgcheck=1
gpgkey=https://pkgs.k8s.io/core:/stable:/v1.30/rpm/repodata/repomd.xml.key
exclude=kubelet kubeadm kubectl
EOF
```

###  Instalar paquetes:
```
yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes
systemctl enable --now kubelet
```

### Sincronización de hora
```
yum install -y chrony
systemctl enable --now chronyd
timedatectl set-ntp true
```

## Usuario de gestión
```
useradd k8sadmin
passwd k8sadmin
usermod -aG wheel k8sadmin
```

# Configuración en el Control Plane
```
# Iniciar cluster
kubeadm init --pod-network-cidr=10.244.0.0/16

# Configurar kubectl para el usuario actual
mkdir -p $HOME/.kube
cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
chown $(id -u):$(id -g) $HOME/.kube/config

# Instalar red de pods (Flannel)
kubectl apply -f https://raw.githubusercontent.com/flannel-io/flannel/master/Documentation/kube-flannel.yml

```

### Al final de `kubeadm init` verás un comando tipo:
```
kubeadm join 192.168.0.10:6443 --token <token> \
    --discovery-token-ca-cert-hash sha256:<hash>
```

⚠️ Ese comando lo usarás en los **worker nodes**.

### Configuración en los Worker Nodes
```
kubeadm join 192.168.0.10:6443 --token <token> \
    --discovery-token-ca-cert-hash sha256:<hash>

```

## Validaciones
```
# Ver que los nodos están unidos
kubectl get nodes

# Probar con un deployment
kubectl create deployment nginx --image=nginx
kubectl scale deployment nginx --replicas=4
kubectl get pods -o wide

```
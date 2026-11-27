# Workspace
```bash
cd /home/jon/Documents/kubernetes/19 STORAGE CLASS/recursos/ebs
```
Vamos a ver como funciona un volumen de AWS EBS con K8s instalado en instancias EC2. Lo primero que debemos hacer es ir a la documentacion de K8s para ver la forma en la que se instala el plugin.
[Amazon EBS](https://docs.aws.amazon.com/es_es/eks/latest/userguide/ebs-csi.html)
[Instalar driver para EBS](https://github.com/kubernetes-sigs/aws-ebs-csi-driver)
# Instalar driver
```bash
kubectl apply -k "github.com/kubernetes-sigs/aws-ebs-csi-driver/deploy/kubernetes/overlays/stable/?ref=release-1.68"

kubectl get csidrivers.storage.k8s.io
```
# Crear un disco virtual (EBS)
Vamos a crear nuestro disco para realizar las pruebas y conexiones con el volumen, debemos obtener el _Volume ID_ para las configuraciones necesarias.
No nos olvidemos de darle permiso a las instnacias para poder utilizar el disco virutal (EBS), vamos a crear un rol.
# Crear politica
Nos dirigimos a **IAM->Policies->Create policy**, seleccionamos la pestana **JSON** y seguimos con la creacion.
```json
{
  "Version": "2012–10–17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ec2:AttachVolume",
        "ec2:CreateSnapshot",
        "ec2:CreateTags",
        "ec2:CreateVolume",
        "ec2:DeleteSnapshot",
        "ec2:DeleteTags",
        "ec2:DeleteVolume",
        "ec2:DescribeAvailabilityZones",
        "ec2:DescribeInstances",
        "ec2:DescribeSnapshots",
        "ec2:DescribeTags",
        "ec2:DescribeVolumes",
        "ec2:DescribeVolumesModifications",
        "ec2:DetachVolume",
        "ec2:ModifyVolume"
      ],
      "Resource": "*"
    }
  ]
}
```
# Crear rol
Nos dirigimos a **IAM->Roles->Create Role->AWS Service->EC2** damos click en **Next**, buscamos la politica que creamos y seguimos con la cracion.
# Asignar rol a las instancias
Debemos seleccionar las instancias y damos click en **Actions->Security->Modify IAM role**, seleccionamos el rol que hemos creado, al control plane y los worker nodes.
# Crear Storage Class
```bash
kubectl apply -f sc.yaml
kubectl get sc
```
# Crear PV
```bash
kubectl apply -f pv.yaml
kubectl get pv
```
# Crear PVC
```bash
kubectl apply -f pvc.yaml
kubectl get pvc
kubectl describe pvc aws-claim
```
# Crear POD
```bash
kubectl apply -f pod.yaml
```
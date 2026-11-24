Vamos a crear un volumen un poco mas profesional donde los worker nodes se van a conectar al mismo volumen. Es decir, si creo varios pods y estos se crean en los distintos worker nodes, estos van a utilzar el mismo volumen de tal forma que los datos van a ser mas congruentes que si se crea un volumen por cada worker node, donde el pod solo va acceder al volumen del worker node lo que llevaria a una inconsistencia por que puede que la peticion se realice en un worker node, pero si se llegara ha obtener los valores de esa peticion que fue almacenda en el worker node desde otro worker node esto no podria ser posible ya que el volumen no se comparte con los otros worker node.

Hostpath solo debe ser usado en dessarrollo o en pruebas cuando tenemos un solo nodo, porque todos los pods acceden a mismo worker node.

Vamos a crear un entorno compartido entre los distintos worker nodes de mi K8s.

Se recomienda tener un servidor por separado para NFS, en esta practica la vamos a tener un nuestro Control Plane. Y en los Worker Node vamos a tener a los clientes.
# Instalar NFS en Control Plane
```bash
sudo apt install nfs-kernel-server
```
## Sitio compartido
```bash
mkdir /var/datos
```
## Configurar NFS
Le vamos a indicar el sitio que vamos a compartir con los otros Worker Nodes
```bash
vi /etc/exports
```

```text
/var/datos *(rw,sync,no_root_squash,no_all_squash)
```
El asterisco (\*) representa que todas las IPs van a poder acceder al sitio.
## Reiniciar NFS
```bash
sudo systemctl restat nfs-kernel-server
```
## Verificar 
```bash
showmount -e 192.168.0.23
```
# Configurar Worker Node
```bash
sudo apt install nfs-common
```
## Verificar 
Debe ser la IP del Control Plane dado que alli fue donde se instalado NFS Server.
```bash
showmount -e 192.168.0.23
```

```bash
mkdir /var/datos
mount -t nfs 192.168.0.23:/var/datos /var/datos
```
Realizo todos estos pasos en todos los Worker Nodes.
Como prueba podemos crear un fichero desde un Worker Node y luego nos dirigimos al Control Plane y verificamos que se encuentra el fichero que creamos.
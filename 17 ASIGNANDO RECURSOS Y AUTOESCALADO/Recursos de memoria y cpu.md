# Determinar los recursos de memoria y las cpus en un Namespace
Si quisiera poner limites dentro de un proyecto, namespace lo podria hacer sin ningun problema.
Porque realizar esta accion, ya que vamos a estar trabajando en la misma infraestructura con otros equipo: DEV, STAGING, PROD. Pues vamos a querer asignale distintos recursos a los equipos. No va ser lo mismo para PROD que DEV en produccion vamos a querer utilizar mas memoria y cpu, mientras que en desarrollo vamos a darle lo minimo.

# LimitRange. Limintar los recursos de los contenedores en una Namespace
Vamos a tener dos tipos de configuracion:
- Default: para todo el namespace, limitRange es a nivel de namespace. Se aplica si no decimos nada
- max y min: nos indica la pacacidad maxima y minima que va tener nuestro pod o container.
- type: especifica a quien se le va aplicar la configuracion si es a un pod o un container. si se lo aplica a un pod y este tiene dos container lo que quiere decir es que el uso de esos dos containers no deben ser superados. Pero si se lo aplica a un container este se aplica a cada container.
## Workspace
```bash
cd /home/jon/Documents/kubernetes/17 ASIGNANDO RECURSOS Y AUTOESCALADO/recursos
```
## Aplicar LimitRange
Debemos cambiarnos de Namespace para no crearla en la de default
```bash
kubectl apply -f limitex.yaml
```
## Verificar que se agregaron las configuraciones
```bash
kubectl describe ns n1 
```
## Prueba
### Crearmos un pod
```bash
kubectl run apache1 --image=httpd
```
Como no le indicamos nada va utilizar la configuracion por defecto
```bash
kubectl describe pod apache1
```
### Instalamos programa para estresar el pod
```bash
kubectl exec -it apache1 -- bash
apt update
apt install stress 
stress -n 10
dmesg
```
### Verificamos el uso del pod
Abrimos otra terminal, tomemos en cuenta que las metricas tardan un poco en recolectarse
```bash
kubectl top pod
watch kubectl top pod
```
### Creamos un pod para ver la configuracion por defecto
```bash
kubectl run nginx1 --image=nginx1
```

```bash
kubectl describe pod nginx1
```
# ResourceQuota. Limitar los recurso de una Namespace
## Workspace
```bash
cd /home/jon/Documents/kubernetes/17 ASIGNANDO RECURSOS Y AUTOESCALADO/recursos/resourcequota
```
La diferencia entre limit y quota es que limintamos al pod y en el otra caso limitamos la namespace respectivamente.
Por lo tanto la cuota lo que me impide es que un namespace sobre pase ciertos limites a nivel global.
## Crear cuota
```
kubectl apply -f Resource1.yaml
```
## Verificar que se haya creado la cuota
```
kubectl get quota
kubectl get ns n1
```
## Modificamos el fichero Resource1.yaml
### Before
```bash
cpu: "100" 
memory: "500Mi"
```
### After
```bash
request.cpu: "100" 
request.memory: "500Mi"
limit.cpu: "100" 
limit.memory: "500Mi"
```
Aplicamos los cambios y vemos su comportamiento.
# Que pasa si creamos un pod sin limits, quota
```bash
kubectl run apache1 --image=httpd
```
Me va dar un error porque no estoy cumpliendo con lo que me pide la cuota, no es que me lo pida sino que necesita saber que recurso va utilizar nuestro pod y de esta manera si se llega a pasar de las cuotas ya no se le va poder crear.
# Crear pod con las especificaciones
```bash
kubectl apply -f nginx.yaml
```

```bash
kubectl get pods
kubectl get quota
kubectl get pod nginx
```
# Sobre pasar los limites
```bash
kubectl apply -f deploy_recursos.yaml
```

```bash
kubectl get pods
kubectl get quota
kubectl get pod nginx-d
kubectl describe pod nginx-d
```
No me deja crear un pod porque ya estamos sobre pasando las cuotas establecidas para la namespace. Dado que nuestro deploy indica que va crear dos pod y cada pod tiene una memoria de 400Mi por lo que ocuparia 800Mi y nuestro limite dice que solo tenemos permitido hasta 500Mi. Por lo que solo crea un pod.
# Para que se cren los recursos modificamos las cuotas Resource1.yaml
### Before
```bash
request.cpu: "100" 
request.memory: "500Mi"
limit.cpu: "100" 
limit.memory: "500Mi"
```
### After
```bash
request.cpu: "100" 
request.memory: "1Gi"
limit.cpu: "100" 
limit.memory: "1Gi"
```

# Dar prioridades a nuestros Pods priorityClassName
Como hacer que un pod tenga mayor prioridad que otro. Las PriorityClassName son las que nos van a permitir tener prioridad entre nuestros **pods**, para que nuestro pod tenga mayores recursos y de ser necesario expulsar a los otros pods que tengan menor prioridad en el nodo.
Para la ejecucion de mis priorityClassName debe eliminar todos los limites que tenga creado porque de lo contrario me va dar errores muy extranos: de creacion.
## Workspace
```bash
cd /home/jon/Documents/kubernetes/17 ASIGNANDO RECURSOS Y AUTOESCALADO/recursos/resourcepriority
```
### Ver las PC por defecto
```bash
kubectl get pc
```
### Crear prioridades
```bash
kubectl apply -f prioridades.yaml
```
### Crear pods con priorityClass
```bash
kubectl apply -f deploy_pc_low.yaml
```
Debemos bajarle el numero de replicas porque solo tenemos un nodo podria ser a unas 15 o 20, en ves de 100.
Ver cuantos pods se crearon
```bash
kubectl get deploy 
```
Vamos a apreciar que no se crearon todos los pod algunos van a estar en pending debido a que ya hemos utilizado todos los recursos y no hay mas para asignar.
```bash
kubectl get pod -o wide
```
Vamos a inspecionar uno de los nodos que esten en running
```bash
kubectl describe pod apache-deploy-937432-wc32dk 
```
Vamos a ver que esta utilizando la propiedad.
### Crear pod con mayor prioridad
Que pasa si ahora creamos pods con mayor prioridad a los que se estan ejecutando en este momento, se van a retirar los pods con menor prioridad para que se puedan ejecutar los pods con mayor prioridad.
```bash
kubectl apply -f deploy_pc_alta.yaml 
```
Vamos a ver que a pasado con los pods con menor prioridad
```bash
kubectl get deploy
```
Vamos a ver que el numero de pod de menor prioridad han bajado
# Quotas. Trabajar con multiples quotas
Vamos a ver como trabajar con mas de una cuota, el hecho de poder tener varias cuotas significa que yo puedo acoplar determinados pods o determinados deployment a distintas cuotas de forma que algunas puedan consumir mas que otras dentro del namespace, dependiendo de las cuotas que se hayan asignado.
Antes debemos borrar todo lo que tubieramos
```bash
kubectl delete pods --all
kubectl delete quota --all
```
De forma que todo quede vacio.
Vamos a ver que se hayan borrado del namespace
```bash
kubectl describe ns n1
```
Vemos que no tienen _limitrange_ (que es unico, porque es a nivel de pod), _resource_ (pueden ser varias).
## Workspace
```bash
cd /home/jon/Documents/kubernetes/17 ASIGNANDO RECURSOS Y AUTOESCALADO/recursos/resourcequotas
```
### Crear Quotas
```bash
kubectl apply -f Resource2.yaml
```
### Ver las quotas
```bash
kubectl get quota
kubectl describe ns n1
```
### Asignar pods
Para que vayan a parar a una couta u otra.
Previamente las priorityClassName deben existir
### Crear priorityClass
```bash
kubectl get pc
```

```bash
kubectl apply -f nginx-prioridad_produccion.yaml
kubectl get quota
```

```bash
kubectl apply -f nginx-prioridad_desarrollo.yaml
kubectl get quota
```
# Ver los recursos de un nodo
Vamos a ver las caracteristicas de un nodo y los recursos dentro del mismo.
```bash
kubectl get nodes
kubectl top nodes
kubectl get deploy
kubectl top node cluster1-m3
kubectl get node -o wide
kubectl describe node cluster1-m3
```
# HugePages. Introduccion
Es un recurso que se utiliza dentro de las maquina linux, nos permite trabajar con memirias mas grandes de lo normal.
El kernel soporta el tamano de las paginas se divide en bloques de 4K.
Con este recurso podemos tener paginas de 2MB o hasta 1GB.
No todos los OS puden soportar paginas grandes.
# Configurar HugePages en Linux
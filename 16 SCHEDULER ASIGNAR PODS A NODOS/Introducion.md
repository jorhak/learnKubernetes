Vamos a ver como se asocian los **pods** a los **nodos**, que decisiones toma k8s para decidir si un pod va a parar a determinado nodo o va parar a otro.
El principal responsable de esto es **Scheduler**.

# Scheduler
Se encarga de determinar a que nodo envia cada pod. La asignacion de de en donde
va ir el pod no es aleatoria, sigue un proceso muy estricto.

Aquin no vamos a trabajar en local sino mas bien con un proveedor: AWS.
Vamos a intentar replicar esto en nuestro minikube.
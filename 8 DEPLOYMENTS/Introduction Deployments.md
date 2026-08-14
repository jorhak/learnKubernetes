Que es un deploymen?
El objeto mas pequeno que puedo tener dentro de K8s es un contenedor, ya sabemos que un contenedor no se pude lanzar solo en K8s, hay que envolverlo dentro de un **pod**. Los **pods** tienen distintos problemas:
- no escalan
- no se recuperan ante caidas
- updates y rollbacks complicados

Si los **pods** tienen todos estos problemas, no tengo que trabajar de forma directa como tal sino lo que vamos hacer es poner los **pods** dentro de un **deployment**. El **deployment** es otro componente que es una especie de burbuja que engloba unas propiedades, caracteristicas entre ellos los **pods** que debe de tener lo que permite que cuando yo tengo un **deployment** voy a poder tener:
- updates y rollbacks
- recuperacion ante caidas
- escalan (anadir o quitar pods)

Tambien debemos tener en cuenta el estado actual y el estado deseado y K8s intenta a toda costa que ambos coincidad.

Cuando creo un **deployment** sin que yo se lo diga me crea otro objeto llamado **replicaset**. Los **replicaset** son los encargados basicamente de hacer las replicas y de gestionar la recuperacion de caidas. Es un componente individual.

Un **deployment** es la unidad de trabajo mas habitual para empezar a desplegar mis proyectos dentro de K8s
PV (Persisten Volume) es una capa que le pone K8s a los usuarios de tal forma que puedan acceder al almacenamiento de manera totalmente transparente y sin conocer realmente lo que hay por detras.
Los PV deben ser creados por los administradores porque hacen una configuracion fisica de bajo nivel. PV es como un disco logico que se puede utilizar ahora dentro de K8s.
Es una especie de disco virtual que apunta al disco real que hay por detras, como utilizan los desarrolladores este PV, lo primero que se hace es crear un PVC (Psersisten Volume Claim) esto es como una peticion de recurso. El que crear el PVC no sabe como esta creado el PV si es un disco A, si es un disco Scaci, NFS, etc.
Donde se pone el PVC, se coloca en el pod.

Que son las STORAGE CLASS?
En lugar de tener PV individuales lo que hago es crear clases, es decir, mira voy a crear la clase _discos rapidos_, _discos lentos_, _xxxx_, y asocio los PV a estas clases
Ahora al crear un PVC ya no vamos a llamar un PV sino a un STORAGE CLASS, en el STORAGE CLASS van a estar asociadas varias PV, y cuando llame desde PVC se me va asignar las mas proxima a lo que solicito, si solicito 5GB y en el STORAGE CLASS tengo dos PV de 6GB y 8GB me va asignar la de 6GB porque es la mas cercana y me sobre pasa. A esto se le llama almacenamiento dinamico.
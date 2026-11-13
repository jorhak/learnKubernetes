Todo el almacenamiento que se crea dentro de un container de K8s, es decir, dentro de un contenedor de un **pod** es siempre efimero, temporal.
Se crea de forma temporal dentro de la maquina y que desaparece en el momento en que se destruye el **pod** (contenedor).
No siempre voy a querer almacenamiento temporal, sino que tambien voy a querer almacenamiento persistente.
## Volumenes
Es un objeto que nos va permitir persistir el almacenamiento que necesito para trabajar.
Esto me va permitir cuando cree un **pod** y si lo elimino los datos los voy a seguir teniendo, para volver a utilizar ese volumen en otro **pod**.
Tipos de volumenes
- Locales
- Externos
- Cloud
Investigar los drivers soportados para los volumens al dia de hoy.
**CSI** Container Storage Interface
[Lista de drivers](https://kubernetes-csi.github.io/docs/drivers.html).
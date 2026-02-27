Un secrets es un recurso que nos permite almacernar informacion confidencial: contrasenas, token de autorizacion, claves ssh, etc.

La forma mas directa de usar un secret es ponerlo en un pod.

# Tipos de Secrets
### Opaque
Que son los normales (opacos o genericos) guarda cualquier cosa son muy parecidos a los configmaps. Estan codificados en base64, no encriptados.

### Service Account Token
Tienen un toke para un service account. Y que es esto? es una Identity que nos permite poder ejecutar dentro de un Pod un determinado proceso.

### Docker config
Guarda los credenciales de un repositorio privado de docker.

### Basic Authentication
Contiene usuario y contrasena.

### SSH
Credencial para conectar por un par de llave.

### TLS
Lo que vamos a guardar dentro de este secret va ser un certificado y la clave asociada (tls.key, tls.crt).

### Bootstrap
Estos tokens son especiales que se utilizan para el proceso de bootstrap de un nodo. Normalmente estos no se tocan.
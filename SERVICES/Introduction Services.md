Los servicios son los objetos que permiten que las aplicaciones, despliegues se conecten con el mundo exterior. Nos va permitir que nuestros _pods_ se comuniquen entre si o que se conecten al exterior.

Los _servicios_ nos van a permitir poder conectarnos de forma externa contra los _pods_.

Tenemos tres tipos de _servicio_:
- ClusterIP
- NodePort
- LoadBalancer

El _selector_ es como un query, que dice voy a buscar a todos los que tengan esta etiqueta.
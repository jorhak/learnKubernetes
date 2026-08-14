Los **PODS** que hemos creado hasta ahora no podemos hacerles pruebas de que se estan ejectuando, es decir, no podemos ver el contenido del **POD**. Es cierto que hemos hecho pruebas dentro de los **pods** para ver que se estan ejecutando. Sin embargo, el usuario final no podra hacer este tipo de pruebas ya que no estamos exponiendo el servico para ver su pagina web.
La prueba que hemos realizado son alternativas, lo que quiere decir que solo a nosotros nos consta que el servico se esta ejecutando, ahora lo que debemos hacer es que se pueda hacer la prueba de que el **pod** si se esta ejecutando de tal forma que el usuario final pueda apreciar su pagina web, endpoints, etc.

Nos faltan ver los objetos que nos permitiran que nuestro **pod** se esta ejecutando los cuales son: _deployment_, _service_. Los que me permetiran desplegar y poder acceder a mi aplicacion desde fuera del cluster.

En este momento el **pod** esta en una encapsula en la cual no puede ser accedida de forma directa.

## kubectl proxy
Nos brindara una IP y PUERTO el cual nos ayudara a realizar no solo la prueba de nuestro **pod** sino que tambien nos mostrara todas las _apis_ del cluster que tenemos a nuestra disposicion.
En este momento solo nos enfocaremos a ver que nuestro **pod** con **apache** se este ejecutando correctamente.
```
kubectl proxy
```

Luego en un navegador vamos a escribir lo siguiente.
```
localhost:8001/api/v1/namespaces/default/pods/apache/proxy
```
De esta forma vamos a poder ver la pagina web de apache, esto solo siver para ver que nuestro servidor web esta funcionando si esto fuera otro tipo de servicio no nos serviria.

Mas adelante vamos a utilizar el objeto **service** para exponer los recursos del **pod** al exterior.

Lo que hemos hecho hasta ahora es para ver si nuestro **pod** se esta ejecutando correctamente ya que nos encontramos en desarrollo y queremos ver si nuestras soluciones van por buen camino.

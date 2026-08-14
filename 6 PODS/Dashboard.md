# Dashboard de Minikube
Vamos a ver los _pods_ desde el dashboard de minikube
```
minikube dashboard
```

## Opciones dentro del Dashboard
En esta ocacion vamos hablar de los _pods_, nos dirigimos en la parte izquierda a **PODS** y nos va listar los _pods_ que estan en ejecucion, seleccionamos uno y nos va mostrar los detalles de ese _pod_ y en la parte derecha superior vamos a encontrar cuatro iconos: logs, exec, update y delete, vamos a poder ver los logs de ese pod, vamos a poder entrar en el pod y ejecutar comandos, podremos modificar el pod (los vamos a poder hacer en formato yaml o json) y tambien se podra realizar la eliminacion del pod respectivamene. 

## Crear un objeto desde el Dashboard
Para crear un objeto desde el _dashboard_ nos vamos a dirigir a la parte superior derecha en el icono de **MAS** damos click y se abrira una ventana donde tendremos tres opciones para crear un objeto:
- Crear desde entrada
- Crear desde un fichero
- Crear desde un formulario

Entrada: vamos a escribir el objeto que deseamos crear o en todo caso un copy y paste.
Fichero: vamos a poder cargar un fichero y crear el objeto de ese fichero
Formulario: aqui tendremos un inconveniente ya que este lo que crea es un **deployment** y es mas complejo que un **pod**.
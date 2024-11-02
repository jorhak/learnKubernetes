Vamos a utilizar el dashboard de minikube para ver como funciona y sus funciones

```
minikube dashboard
```

Nos lanza una pagina web donde podemos visualizar y monitorear los objetos.

## Modificar nuestro pod desde el Dashboard

Abrimos nuestro navegador y introducimos la IP:PORT que nos haya dado el comando previo.

Debemos seleccionar el namespace donde se encuentra nuestro pod luego en la parte derecha damos click en **Pods**, luego damos click en **nginx** y en la parte superior tendremos cuatro iconos que representan __logs, exec, editar, eliminar.__

En editar tendremos las dos opciones que ya habiamos visto la de **json** y **yaml**, en labes le vamos a agregar 

```
responsable: Jorhak Mormont
```

Y finalmete damos click sobre el boton **Actualizar**

## Crear pods desde Dashboard

Se tiene tres formas para crea un objeto pod y para ello debemos ir a la parte superior derecha y dar click sobre el icono **+**
- Crear desde entrada
- Crear desde un fichero
- Crear desde un formulario

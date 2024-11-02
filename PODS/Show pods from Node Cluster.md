Esto no es algo que se haga todos los dias sino cuando se tenga un problema.

Vamos a ver como es que se traducen los objetos que creamos internamente k8s. Y para ello nos conectamos al nodo de k8s.

```
minikube ssh
uname -a

```

Todo lo que va haciendo k8s por debajo lo va haciendo con el motor de contenedores con el que estemos trabajando, por decir, docker.

```
docker ps
docker ps | grep apache
```

Aqui no se ven los pods sino los contenedores como tal, de las imagenes que vamos creando con los pods.
Podemos manipular estos componentes, sin embargo, no se lo hace directamente ya que para ello lo hacemos desde fuera con kubectl. No se toca directamente.
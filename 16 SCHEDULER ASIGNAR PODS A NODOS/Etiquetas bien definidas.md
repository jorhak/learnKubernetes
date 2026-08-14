Vamos a ver que significa **Well-Known Labels, Annotations and Taints**, durante todo el curso hemos estado utilizando etiquetas para en cierta forma buscar objetos, selectores, en el **Ejemplo Node Selector con Deployment** hemos seleccionado los nodos de los pods.

Hay una serie de etiquetas y anotaciones que se asignan a los objetos que se van creando de forma automatica dentro de K8s.
Estas etiquetas suelen llevar la extension _kubernetes.io_ y lo mas interesante es que se asocian automaticamente el propio K8s es el que las va generando.

Hay etiquetas recomendadas que deberia conocer, esto para poder trabajar con un conjunto de objetos.

# Veamos lo que tienen nuesto nodo
```
kubectl get nodes
kubectl describe node hola
```
Y veremos dentro de las labels tenemos una serie de etiquetas que ya estan predefinidas.

Por dar un ejemplo si quiero desplegar mis pods en linux y tengo una mescla de nodos de linux y win, es factible que en el selector le diga aquellas maquinas sean linux.
# Ver etiquetas asignadas por K8s
```
kubectl get pods --show-labels 
```
K8s siempre intenta colocar etiquetas por defecto.
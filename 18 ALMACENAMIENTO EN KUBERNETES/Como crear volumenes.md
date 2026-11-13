Vamos a utilizar dos clausulas:
- Nos va indicar donde montar el almacenamiento dentro del **pod**. Tipo de volumen y donde esta.
- Donde o como van a ser los volumenes que vamos a utilizar. Donde se va a mapear dentro del **pod**.
volumeMounts: donde lo montamos dentro del **pod**.
volumes: el nombre debe ser igual al nombre que se va tener en el volumeMounts, y vamos a difinir el tipo de driver que vamos a utilizar. Dependiendo del tipo de volumen lo vamos a tener que configurar.
[Configurar volumes con sus drivers](https://kubernetes.io/docs/concepts/storage/volumes/#hostpath).
Los volumes pertenecen al pod y los volumeMounts pertenecen al contenedor.
```yml
apiVersion: v1
kind: Pod
metadata:
  name: volumenes
spec:
  containers:
    - name: nginx
      image: nginx
      volumeMounts:
      - mountPath: /home
        name: home
volumes:
  - name: home
    hostPath:
      path: /home/kubernetes/datos
```
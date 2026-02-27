Debemos ingresar en la ruta
```
cd /home/jon/Documents/kubernetes/VARIABLES, CONFIGMAPS Y SECRESTS/configMapYVolumenes
```

Los **configMap** nos permiten dejarlos en un sitio dentro de nuestro contenedor como si fueran un fichero lo cual nos genera opciones, perspectivas dado que podemos tomar esa informacion que hemos dejado en algun sitio y luego utilizarla para cualquier cosa dentro de nuestro contenedor.
Recordemos que ni las variables, configMaps, secrets son de por si utiles, son utiles en cuanto yo los uso dentro del contenedor.

Cuando hablamos de dejar un fichero nos referimos a que lo vamos a dejar en un volumen.
Esto hace que nuestro volumen lo podamos acceder desde fuera para que nuestro contenedor lo consuma.

## Ver configMap
```
vi configmap.yaml
```

## Ver el pod
```
vi pod1.yaml
```

## Crear configmap y pod
```
kubectl apply -f .
```

## Verificar que se creo el configmap y el pod
```
kubectl get cm
kubectl describe cm config-volume
kubectl get pod
kubectl describe pod pod1
kubectl exec pod1 -- env
```

Podemos ver que no tenemos las dos variables porque no lo hemos montado como varible, lo hemos montado como volumen. Entonces si me voy al directorio */etc/config-map*
```
kubectl exec -it pod1 -- sh
cd /etc/config-map
ls -la
cat ENTORNO
cat VERSION
```

Lo a montado como enlaces ENTORNO -> ..data/ENTORNO. Puedo manejar estos ficheros.
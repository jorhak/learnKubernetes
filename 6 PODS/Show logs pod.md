## Primero creamos el POD
```
kubectl run apache --image=httpd --port=8080
```

## Ver los logs del POD
```
kubectl logs apache
```
Este comando nos permite ver los logs de nuestro **POD** esto hasta donde se han generado logs en ese momento. Si queremos ver los logs que se generan en cada momento debemos agregar un flag -f para que quede a la escucha de los eventos.
```
kubectl logs -f apache
```

## Ver la ultimas lineas del log
```
kubectl logs apache --tail=30
```
Con el flag --tail=30 nos mostrara las ultimas 30 lineas del log.

# Verificar que el POD se esta ejecutando
Abrimos otra terminal y accedemos al **POD**.
```
kubectl exec apache -it -- bash
```

En este caso vamos a tener aque actualizar nuestro **pod** para instalar _wget_ para hacer la prueba.
```
apt update
apt install wget -y
```

Ahora realizamos la prueba y luego volvemos a la terminal donde dejamos los logs a la escucha de los eventos.
```
wget localhost
```
De esta forma vamos a ver que estamos realizando peticiones get y esto se ve refejado en los logs.
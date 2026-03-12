Son identicos a trabajar con **configmap** en el caso de los volumenes, vamos asociar un secreto a un directorio donde cada propiedad cada componente del secreto va ser un fichero.

Cuando tenemos un secret vamos a tener dos opciones:
	a) stringData, texto plano
	b) Data, codificado en base64

En este caso como hemos montado el volumen en _/tmp/datos_ vamos a tener dos ficheros:
```
DATO1 -> ..data/DATO1
DATO2 -> ..data/DATO2
```

Verificamos el contenido de cada fichero
```
cat DATO1
cat DATO2 
```

1. WorkSpace
```
cd /home/jon/Documents/kubernetes/VARIABLES,\ CONFIGMAPS\ Y\ SECRESTS/secretV  
olume/
```

2. Ejecutar **Secret**:
```
kapp secretoVolumen.yaml
```

3. Verificar **Secret**:
```
kd secret/secreto-volumen
```

4. Ejecutar **Pod**:
```
kapp pod1.yaml
```

5. Verificar **Pod**:
```
kd pod/pod1
```

```
kexec pod/pod1 -- bash
cd /tmp/datos
```
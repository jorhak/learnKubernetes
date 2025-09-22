# Ver configuracion
```
kubectl config view
```

# Configurar namespacer por defecto
```
kubectl config set-context --current --namespace=dev1
```
# Configurar namespace desde fichero
```
cd ~/.kube
nano config
```

# Probar configuracion
```
kubectl get pods
```

Ya no tengo que estar agregando **-n dev1** por que ya lo tengo por defecto.

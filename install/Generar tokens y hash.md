# Generar tokens y hash desde el fichero /etc/kubernetes/admin.conf

## Exporta la variable para usar el kubeconfig
```
export KUBECONFIG=/etc/kubernetes/admin.conf
```

## Genera un nuevo token válido
```
kubeadm token create
```

## Obtén el hash del CA
```
kubeadm token create --print-join-command
```

### ⚠️ Importante

- Si en tu worker **tienes `kubeadm` instalado** y el `/etc/kubernetes/admin.conf` apunta correctamente al API server, puedes ejecutar lo anterior sin problema.
    
- Si el worker **no tiene conectividad con el API server del control plane**, no funcionará.
# Ver los logs
```
git log
```

# Eliminar ultimo commit
Se borra el ultimo commit y sus cambios del repositorio local
```
git reset --hard HEAD~1
```

## Commit en el repositorio remoto
Si el commit esta en el repositorio remoto debemos ejecutar:
```
git push origin +main
```
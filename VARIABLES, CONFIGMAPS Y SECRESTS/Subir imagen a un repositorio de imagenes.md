# Iniciar sesion
```
docker login
```

# Construir imagen
```
docker buildx build --platform=linux --no-cache -t appprueba .
```

# Asignar tag
```
docker tag appprueba user/appprueba
```

# Subir imagen
```
docker push user/appprueba
```
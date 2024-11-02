Es un fichero de configuracion que nos permite construir y componer objetos, recursos de k8s.

YAML es un fichero que contiene basicamente componentes tipo clave-valor, la cual nos ayudara a contruir nuestras properties.

Es un lenguaje de serializacion, la identacion deben ser espacios en blanco y no tabuladores debido aque estos deben ser multisistema.

```
#Las cadenas no requieren comillas:
Título: Introducción a YAML

# Pero se pueden usar:
title-w-quotes: 'Introducción a YAML'

# Las cadenas multilínea comienzan con |
ejecutar: |
    npm ci
    npm build
    prueba npm

#Secuencias
#Las secuencias nos permiten definir listas en YAML:
# Una lista de números usando guiones:
números:
    - uno
    - dos
    - Tres

# La versión en línea:
números: [uno, dos, tres]

#Valores anidados
#Podemos usar todos los tipos anteriores para crear un objeto con valores anidados, así:
# Mil novecientos ochenta y cuatro datos nuevos.
1984:
    autor: George Orwell
    publicado en: 1949-06-08
    recuento de páginas: 328
    descripción: |
        Una novela, a menudo publicada como 1984, es una novela distópica del novelista inglés George Orwell.
        Fue publicado en junio de 1949 por Secker & Warburg como noveno y último b de Orwell.


#Lista de objetos
#Combinando secuencias y valores anidados  podemos crear una lista de objetos.
# Hagamos una lista de libros:
- 1984:
    autor: George Orwell
    publicado en: 1949-06-08
    recuento de páginas: 328
    descripción: |
        Una novela, a menudo publicada como 1984, es una novela distópica del novelista inglés George Orwell.

- el Hobbit:
    autor: J. R. R. Tolkien
    publicado en: 1937-09-21
    recuento de páginas: 310
    descripción: |
        The Hobbit, o There and Back Again es una novela de fantasía para niños del autor inglés J. R. R.
```
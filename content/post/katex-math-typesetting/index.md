---
date: "2020-02-28"
tags:
- katex
- math
- typesetting
- hugo
title: IDE y Tidyverse
---

### Instalación de Paquetes.

Estos se integran por  funciones que se han construido por miembros de la comunidad, nos permiten realizar operaciones concretas así como estimar procedimientos estadisticos de diverso gado de complejidad.
Para poder utilizar estos paquetes es necesario instalarlos y activarlos en el espacio de trabajo usando el menú Install y Packages. Área inferior izquierda. La siguiente figura muestra el menú para instalarlos.


![](/Packages.jpg)


Alternativamente podemos utilizar la línea de comandos para hacer la instalación usando la función: `install.packages("ggplot2")`.

Un paquete básico es `tidyverse` este es una colección de funciones y es útil para realizar  tareas de análisis de datos e incluye herramientas  para visualización como `ggplot`. 

Una vez que tenemos el paquete que necesitamos instalado, lo activamos con la función  `library()`.


Una via básica de consulta para conocer los propósiots y los paramétros necesarios para las diferentes funciones para anáisis,  es la documentación de ayuda. Esto se hace anteponiendo un signo $?$  al nombre de la función.   Ej. `?mutate`. *IMPORTANTE*, la libreruia que contiene la funcion debe estar actualmente activa para poder acceder a la documentación solicitada. 

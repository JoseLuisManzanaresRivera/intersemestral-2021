---
date: "2020-02-28"
tags:
- Teoría
- Conceptos 
- IDE
- Tidyverse
title: IDE y Tidyverse
---


### Algunas consideraciones preeliminares sobre R.

R es un lenguaje que nos permite hablar con la computadora, wn analogía con cualquier lenguaje, como aprenderemos existen **sustantivos**, estos son los objetos (data frames o conjunto de adtos),  las funciones pueden entenderse como **verbos** y sus argumentos como **adverbios**.

Estamos aprendiendo un lenguaje para comunicarnos con nuestra computadora con la finalidad de conducir tareas de análisis de datos. 

En la base del proceso de análisis de datos se encuentra la habilidad para almacenar **grandes cantidades de datos** y tener la capacidad para sustraer estos datos cuando lo necesitamos. 

El resto  de actividades como la **manipulación de los datos**, su **visualización** y el **modelado** son etapas en la secuencia del proceso de análisis. 


## R Studio IDE 

Cuatro secciones principales para trabajo: 

![](/IDE.jpg)

![](/IDE2.jpg)


 *Source pane*
 
![](/source.jpg)
### Environment 

![](/environment.jpg)

*Console pane*

![](/console.jpg)

*Viewer*

![](/viewer.jpg)



### Instalación de Paquetes.

Estos se integran por  funciones que se han construido por miembros de la comunidad, nos permiten realizar operaciones concretas así como estimar procedimientos estadisticos de diverso gado de complejidad.
Para poder utilizar estos paquetes es necesario instalarlos y activarlos en el espacio de trabajo usando el menú Install y Packages. Área inferior izquierda. La siguiente figura muestra el menú para instalarlos.


![](/Packages.jpg)


Alternativamente podemos utilizar la línea de comandos para hacer la instalación usando la función: `install.packages("ggplot2")`.

Un paquete básico es `tidyverse` este es una colección de funciones y es útil para realizar  tareas de análisis de datos e incluye herramientas  para visualización como `ggplot`. 

Una vez que tenemos el paquete que necesitamos instalado, lo activamos con la función  `library()`.


Una via básica de consulta para conocer los propósiots y los paramétros necesarios para las diferentes funciones para anáisis,  es la documentación de ayuda. Esto se hace anteponiendo un signo $?$  al nombre de la función.   Ej. `?mutate`. *IMPORTANTE*, la libreria que contiene la funcion debe estar actualmente activa para poder acceder a la documentación solicitada. 


### Consideraciones a recordar sobre los tipos de variables  clases y tipo de atributos.

*Numeric*
*Strings* 
*Factors*

Esta clase se permite almacenar información categórica,  datos que son categóricos por ejemeplo los estados de la república mexicana, sabemos que son 32 y pueden ser almacenados como un vector de factores, en una variable categórica. 

El vector sexo con valores c("Mujer","Hombre"), igual es de clase factor. Un conjunto de rangos de edad por ejemplo con factores en un vector como grupo_e<-C(1,2,3,4)  para 1:0-12 años, 2:13-24, 3:25-34 y 4 35-64 años. 

Estas variables se pueden representar con vectores de clase factor. Esencialmente un factor es una categoría. Note que  no son variables cuyo orden o magnitud sea de terminante. Por ejemplo en el vector sexo  el 2: Mujer,  no es más que uno: Hombre. 

Para asignar la clase **factor** a un vector únicamente pasamos la funcion `as.factor()`   del paquete `tidyverse` o bien la *built in* función   `factor()`. R almacenará los datos en un vector de enteros **integer** . R también agregará el atributo **levels** al atributo ya existente **class**.


`sexo <- factor(c("masculino", "femenino", "femenino", "masculino"))typeof(sexo) class(sexo) attributes(sexo) sexo`


Note que los factores parecen texto pero se comportan como números. Note que R convertirá las strings de texto en factores cuando leemos una base de datos.

Para converitr una variable a  texto  **character strings** solo utilizamos la función `as.character()`

Ejemplo
|
`as.character(sexo)`


## Objetos


### Listas.

Este objeto, permite almacenar un grupo de vectores, cada elemento de la lista puede ser un vector, a diferencia  del caso de los vectores atómicos en donde se agrupan elementos individuales, en una lista cada "elemento" es un vector y estos puden ser de diferentes tipos, ej. numéricos, character strings, logicos. La función utilizada para crear una lista es `list()`

Ejemplo 

`{r} lista<-list(100:130,"R",list(TRUE,FALSE)) lista `


La flexibilidad de este objeto es una ventaja ya que nos permite contar con una herramienta versátil de almacenamiento para agrupar cualquier objeto. 

### Data frames.

Este tipo de objeto es la versión bi-dimensional de una lista donde las **columnas** son vectores (variables) y cada **renglón** observaciones. Este es el tipo de objeto más útil para realizar el análisis de datos. Podemos pensar en un data frame como el equivalente de R a una hoja de cálculo de excel.

Un data frame agrupa los **vectores en columnas**, de tal forma que cada vector de un data frame puede contener un tipo de datos específico, pero cada celda dentro un vector tendrá la misma información. Asímismo, los vectores agrupados en un **data frame** son de la misma longitud. La figura siguiente muestra un ejemplo de esta configuración.


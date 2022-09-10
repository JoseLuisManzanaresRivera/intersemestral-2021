---
date: "2022-09-06"
tags:
- Teoría
- Conceptos 
- IDE
- Tidyverse
title: Miércoles 7 Septiembre (2)
mathjax: true
---


### Algunas consideraciones preeliminares sobre R.

## IDE 

R es un lenguaje que nos permite hablar con la computadora, en analogía con cualquier lenguaje, como aprenderemos existen **sustantivos**, estos son los objetos (data frames o conjunto de adtos),  las funciones pueden entenderse como **verbos** y sus argumentos como **adverbios**.

Estamos aprendiendo un lenguaje para comunicarnos con nuestra computadora con la finalidad de conducir tareas de análisis de datos. 

En la base del proceso de análisis de datos se encuentra la habilidad para almacenar **grandes cantidades de datos** y tener la capacidad para sustraer estos datos cuando lo necesitamos. 

El resto  de actividades como la **manipulación de los datos**, su **visualización** y el **modelado** son etapas en la secuencia del proceso de análisis. 


## IDE Componentes del entorno de trabajo en R  Studio

El entono de trabajo de **R**, (IDE *Integrated Development Environment*) permite introducción de  código para ejecutar estimaciones. Cuatro secciones principales para trabajo: 



![](/IDE.jpg)

![](/IDE2.jpg)


 **Source pane** Permite el registro de los comandos las operaciones utilizadas. (el código utilizado)
 
![](/source.jpg)

**Environment** 

![](/environment.jpg)

**Console y Terminal pane** Area para  introducir código y  ejecutarlo.

![](/console.jpg)

**Viewer**


![](/viewer.jpg)


A medida que avanzamos con el aprendizaje de la implementación en R aprenderemos a manejar elementos en el entorno de R como: **los objetos**, **tipos de datos**,  **notación**, **funciones**, etc.,

### Instalación de Paquetes.

Estos se integran por  funciones que se han construido por miembros de la comunidad, nos permiten realizar operaciones concretas así como estimar procedimientos estadisticos de diverso gado de complejidad.
Para poder utilizar estos paquetes es necesario instalarlos y activarlos en el espacio de trabajo usando el menú Install y Packages. Área inferior izquierda. La siguiente figura muestra el menú para instalarlos.


![](/Packages.jpg)


Alternativamente podemos utilizar la línea de comandos para hacer la instalación usando la función: `install.packages("ggplot2")`.

Un paquete básico es `tidyverse` este es una colección de funciones y es útil para realizar  tareas de análisis de datos e incluye herramientas  para visualización como `ggplot`. 

Una vez que tenemos el paquete que necesitamos instalado, lo activamos con la función  `library()`.


Una via básica de consulta para conocer los propósiots y los paramétros necesarios para las diferentes funciones para análisis,  es la documentación de ayuda. Esto se hace anteponiendo un signo $?$  al nombre de la función.   Ej. `?mutate`. **IMPORTANTE**, la libreria que contiene la funcion debe estar actualmente activa para poder acceder a la documentación solicitada. 


### Consideraciones a recordar sobre los tipos de variables  clases y tipo de atributos.

- Numeric

- Strings 

- Factors

Esta clase se permite almacenar información categórica,  datos que son categóricos por ejemeplo los estados de la república mexicana, sabemos que son 32 y pueden ser almacenados como un vector de factores, en una variable categórica. 

El vector sexo con valores c("Mujer","Hombre"), igual es de clase factor. Un conjunto de rangos de edad por ejemplo con factores en un vector como grupo_e<-C(1,2,3,4)  para 1:0-12 años, 2:13-24, 3:25-34 y 4 35-64 años. 

Estas variables se pueden representar con vectores de clase factor. Esencialmente un factor es una categoría. Note que  no son variables cuyo orden o magnitud sea de terminante. Por ejemplo en el vector sexo  el 2: Mujer,  no es más que uno: Hombre. 

Para asignar la clase **factor** a un vector únicamente pasamos la funcion `as.factor()`   del paquete `tidyverse` o bien la **built in** función   `factor()`. R almacenará los datos en un vector de enteros **integer** . R también agregará el atributo **levels** al atributo ya existente **class**.


```{r}
sexo <- factor(c("masculino", "femenino", "femenino", "masculino"))
typeof(sexo) 
class(sexo) 
attributes(sexo) 
sexo
```


Note que los factores parecen texto pero se comportan como números. Note que R convertirá las strings de texto en factores cuando leemos una base de datos.

Para converir una variable a  texto  **character strings** solo utilizamos la función `as.character()`

Ejemplo

`as.character(sexo)`



Las bases de datos analizados en el curso tiene la siguiente estructura general con **n** renglones (observaciones)  por **p** columnas (variables).  

![](/m.jpg)

Con una variable por columna y una observación por renglón tal como tradicionalmente se estructura la información en una hoja de cálculo. 
Note que el elemento $$x_{ij}$$ de la matriz $$X$$ muestra la 

**observación** 

**i** que va de $$i=1,2,3,...,n$$ 

Y la **variable** **j**  que va $$j=1,2,3,...,p$$

A esta forma de organizacón de datos la denominaremos **TIDY** para efectos de esta clase.


## Estructuras de datos a las que se dirige esta clase.

### Corte transversal

Datos organizados con relación a una unidad de análisis, por ejemplo: una **muestra** de individuos, familias, empresas, ciudades, estados, paises, tomados para  un punto  determinado en el tiempo. Ejemplo: ENIGH, ENGASTO.ENSANUT, ENOE, SINAIS, DENUE. En algunos casos los datos corresponden a encuestas realizadas a lo largo de un perido en distintas semanas, estos datos se consieran de corte transversal.

Este es el tipo de datos que estudiaremos en este curso principalmente. 

Para participación: ¿la siguiente base contiene datos de corte transversal?

```{r, echo=TRUE}
library(tidyverse)
library(datagovindia)

url<-"https://github.com/JoseLuisManzanaresRivera/intersemestral-2021/blob/main/content/post/TASA15.rds?raw=true"

datos_ejercicio_1<-read_rds_from_github(url)%>%
  select(-c(id_ent,espT,pstd))

datos_ejercicio_1


TASA15_M<-datos_ejercicio_1%>%
  filter(Sexo==2)

TASA15_M
```

![](/corte.jpg)

Una submuestra de los datos con filtro únicamente registros para sexo femenino. 

![](/corte2.jpg)


¿Cuál es la unidad de análisis? 


**Nota:** Un supuesto importante para el análisis de datos en estructura de corte transversal es que provienen de una **muestra aleatoria**. Algunos sesgos de selección comúnes ocurren por ejemplo en encuestas que preguntan sobre los ingresos, generalmente es un dato que algunas familias (sobre todo de altos ingresos) no proporcionan.  

### Series de tiempo,

Contienen datos de una unidad de análisis para varios momentos del tiempo, de periodicidad generalmente homogénea (diaria, mensual, trimestral, anual, etc.,).


#### Ejemplo 1 

##### Comportamiento del precio de la Mezcla Mexicana de Petróleo 11/20/2018. 

![](/oil.jpg)

#### Ejemplo 2

##### Comportamiento de la Temperatura Mundial 1880-2000 (°C). ![](/tseries.png)

#### Ejemplo 3

##### Cociente de localización para Diabetes 1998-2015 Frontera Norte y Frontera Sur, México.
![](/panel.jpg)

Otras estructuras incluyen  **datos de panel** que básicamente agrupan series de corte transversal para diferentes momentos en el tiempo (ej. varios años).

```{r, echo=FALSE}

library(gapminder)
glimpse(gapminder)
gapminder<-gapminder%>%
mutate(year1950=year-1950)

gapminder


gapminder_corte<-gapminder%>%
filter(year=="2007")

gapminder_corte

```
#### Ejemplo 4 

##### Datos estructurados como panel.

 
![](/panel1.jpg)

Note la variable que distingue la unidad de análisis es **(country)** y son 142 paises para la variable que incorpora la dimensión temporal para la estructura de panel **(year)**.



Note: Si solo consideramos un año, tenemos una estructura de corte transversal.

![](/paneldos.jpg)

En el ejemplo siguiente la unidad de análisis es la ciudad y la dimensión temporal se consigna por la variable año, en este caso sólo dos años 1982 y 1987.

```{r,echo=FALSE}

library(wooldridge)
library(tidyverse)


data(crime2)

crime2

glimpse(crime2)


crime2<-crime2%>%group_by(year)%>%
mutate(city_id=row_number())%>%
select(city_id,crimes,pcinc,unem,officers,year)%>%
rename(ciudad=city_id, año=year)%>%
  head(15)

crime2
```
Note la estructura en este caso solo tenemos dos años, y como unidad de análisis  la ciudad. 

#### Ejemplo 5

##### Pooled cross section.

![](/panel2.jpg)

También note que la dimensión que denota tiempo (año) se encuentra registrada en una varible.

Así tenemos un data frame de 92 observaciones a lo largo del 2 años para 46 ciudades.

Una estructura de este tipo, donde la dimensión tiempo se extiende por un período corto (ej, comparación ente 2 años). También se denomina comumnente como *pooled cross-section*.

Una ventaja importante de la estructura de datos de panel sobre cross-section es que nos permite **controlar por características no observadas** en un sólo período de tiempo entre las unidades de análisis. 

## Definiciones para implementación en R: 

### Definición de Objetos

Estos se componen por los datos o grupos de datos que podemos analizar en **R**. Para efectos de esta clase los **Data frames** y las **listas** serán los objetos más comunes.

#### Listas.

Este objeto, permite almacenar un grupo de vectores, cada elemento de la lista puede ser un vector, a diferencia  del caso de los vectores atómicos en donde se agrupan elementos individuales, en una lista cada "elemento" es un vector y estos pueden ser de diferentes tipos, ej. **numéricos**, **character strings**, **lógicos**. La función utilizada para crear una lista es `list()`

#### Ejemplo 


```{r}
lista<-list(100:130,"R",list(TRUE,FALSE)) 

lista 

view(lista)
```


La flexibilidad de este objeto es una ventaja ya que nos permite contar con una herramienta versátil de almacenamiento para agrupar cualquier objeto. 

### Data frames.

Este tipo de objeto es la versión bi-dimensional de una lista donde las **columnas** son vectores (variables) y cada **renglón** observaciones. Este es el tipo de objeto más útil para realizar el análisis de datos. Podemos pensar en un data frame como el equivalente de R a una hoja de cálculo de excel.

Un data frame agrupa los **vectores en columnas**, de tal forma que cada vector de un **data frame** puede contener un tipo de datos específico, pero cada celda dentro un vector tendrá el mismo tipo de dato. 
Por ejemplo si la columna es país, y se almacena como factor, cada elemento que integra esta columna será una categoria.


```{r, echo=FALSE}
library(gapminder)
gapminder
str(gapminder)
glimpse(gapminder)
```



Asimismo, los vectores agrupados en un **data frame** son de la misma longitud. La figura siguiente muestra un ejemplo de esta configuración.

#### Ejemplo 1

![](/dataframe.jpg)

#### Ejemplo 2

![](/dataframe2.jpg)

#### Práctica.

Cargue en **R** la base de datos:   `repda_2021.csv` y determine que tipo de variables contiene así como la estructura (ej. corte transversal, panel  o series de tiempo).

Cargamos un data frame (df) con la función read.csv(). Este df  esta alojado en un archivo de texto separado por comas **commas separeted values**  (.csv) nombrado **repda_2021.csv** en la ruta indicada entre comillas: **"C:/Users/..."**. 

```{r}
library(tidyverse)

## Read via url

repdafile<-"https://raw.githubusercontent.com/JoseLuisManzanaresRivera/intersemestral-2021/main/content/post/repda_2021.csv"

practica_datos<-read.csv(repdafile)

## Read From local

agua<-read.csv("C:/Users/josel/Desktop/on/web/MDR-intersemestral-2021/content/post/repda_2021.csv")

names(practica_datos)
glimpse(practica_datos)
str(practica_datos)
class(practica_datos)
```

Este contiene información consesiones para extracción de agua subterránea en el territorio nacional. Note que contiene 15 vectores (variables).

Hemos  utilizado la función `glimpse()` del paquete `tidyverse`  para conocer el tipo de vectores almacenados en el **data frame** y una función alternativa para conocer esta información  mediante la función `str()` structure.

Note que la clase del objeto `agua` es data.frame. También hemos extraído con la función `names()` los nombres de los vectores contenidos en el df.


## Scripts

Para evitar escribir todo el análisis nuevamente, el   *work flow* (la secuencia de trabajo) recomendado en **R** es trabajar con **scripts**, estos son archivos de texto en donde almacenamos todo el código utilizado en nuestro análisis.

Aún mejor, si deseamos podemos almacenar el código en un archivo **R Markdown**  [R Markdown](https://rmarkdown.rstudio.com/), lo que nos permite la flexibilidad de crear el resultado del análisis en diversos formatos incluido **html**. Sí, una página web para consultarla en internet que podemos alojar en servidores como [Netlify](https://www.netlify.com/) o repositorios como [Github](https://github.com/) y publicar el contenido usando un sitio web estático, una forma que permite una enorme ventaja para trabajar de manera colaborativa y remota.

![](/scripts.jpg)

Una vez que almacenamos el código en un script podemos ejecutar cada linea de este código (solo usamos las teclas **ctrl** **enter** en frente de la línea de código a ejecutar), seleccionar una porción  (y lo ejecutamos con ctr+enter) o bien ejecturar todo el **code chunk** (como le decimos en la comunidad **R** a las porciones de código de un script.) utilizando la función **Run** del menú superior. 


### Creación de objetos y lectura de archivos

Para iniciar el análisis de datos cargamos una base que puede presentarse en una variedad de formatos (uno muy común es .csv ) o bien podemos crear un objeto (ej. un dataframe o una lista de variables) en **R** y almacenarlo para su análisis, para lo cual asignamos un nombre usando el simbolo **<-** y tenemos  los datos almacenados en la memoria, a esto le denominamos objetos. 

El simbolo será el equivalente al **=**. Se lee igual a...
Esta notación es un estándard en **R**.

Una vez que nos familizarizamos con la **línea de comando** con facilidad podemos realizar operaciones básicas.


**Note:** Cuando creamos un objeto este aparece en la parte superior derecha en el área de environment

**Ejercicio**

Realice las siguentes operaciones: 

* Elija un número y sume  2. 
* Multipleque el resultado por 3.
* Reste 6 de la respuesta. 

Podemos observar La lista de los objetos activos en el entorno de trabajo usando el comando **ls()**



```{r}
## Para listar  los objetos disponibles.
ls()
```
Importante sobre las reglas para asignar el nombre a un objeto en **R**: 

**Note:** You can name an object in R almost anything you want, but there are a few rules. First,
a name **cannot start with a number**. Second, a name cannot use some special symbols,
like **^, !, $, @, +, -, /, or * **: Note también que  los nombres son sensibles al uso de mayúsculas. Note que si el nombre asignado ya existe, el nuevo objeto sobre escribirá el objeto anterior.








---
date: "2022-08-31"
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


Una via básica de consulta para conocer los propósiots y los paramétros necesarios para las diferentes funciones para anáisis,  es la documentación de ayuda. Esto se hace anteponiendo un signo $?$  al nombre de la función.   Ej. `?mutate`. *IMPORTANTE*, la libreria que contiene la funcion debe estar actualmente activa para poder acceder a la documentación solicitada. 


### Consideraciones a recordar sobre los tipos de variables  clases y tipo de atributos.

- Numeric

- Strings 

- Factors

Esta clase se permite almacenar información categórica,  datos que son categóricos por ejemeplo los estados de la república mexicana, sabemos que son 32 y pueden ser almacenados como un vector de factores, en una variable categórica. 

El vector sexo con valores c("Mujer","Hombre"), igual es de clase factor. Un conjunto de rangos de edad por ejemplo con factores en un vector como grupo_e<-C(1,2,3,4)  para 1:0-12 años, 2:13-24, 3:25-34 y 4 35-64 años. 

Estas variables se pueden representar con vectores de clase factor. Esencialmente un factor es una categoría. Note que  no son variables cuyo orden o magnitud sea de terminante. Por ejemplo en el vector sexo  el 2: Mujer,  no es más que uno: Hombre. 

Para asignar la clase **factor** a un vector únicamente pasamos la funcion `as.factor()`   del paquete `tidyverse` o bien la *built in* función   `factor()`. R almacenará los datos en un vector de enteros **integer** . R también agregará el atributo **levels** al atributo ya existente **class**.


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

Así la estructura de los datos analizados se integra por pares ordenados  $${(x_1,y_1),(x_2,y_2),...,(x_n,y_n)}$$

A esta estructura de datos la denominaremos **TIDY** para efectos de esta clase.


## Estructura de datos.

**Corte transversal.** Datos organizados con relación a una unidad de análisis, por ejemplo: una **muestra** de individuos, familias, empresas, ciudades, estados, paises, tomados para  un punto  determinado en el tiempo. Ejemplo: ENIGH, ENGASTO.ENSANUT, ENOE, SINAIS, DENUE. En algunos casos los datos corresponden a encuestas realizadas a lo largo de un perido en distintas semanas, estos datos se consieran de corte transversal.

Este es el tipo de datos que estudiaremos en este curso principalmente. 

Pregunta, la siguiente base contiene datos de corte transversal.

```{r, echo=TRUE}

TASA15<-readRDS("TASA15.rds")%>%
  select(-c(id_ent,espT,pstd))
TASA15

TASA15_M<-TASA15%>%
  filter(Sexo==2)

TASA15_M
```

![](/corte.jpg)

Una submuestra de los datos con filtro únicamente registros para sexo femenino. 

![](/corte2.jpg)

**Nota:** Un supuesto importante para el análisis de datos en estructura de corte transversal es que provienen de una **muestra aleatoria**. Algunos sesgos de selección comúnes ocurren por ejemplo en encuestas que preguntan sobre los ingresos, generalmente es un dato que algunas familias (sobre todo de altos ingresos) no proporcionan.  

**Series de tiempo** Contienen datos de una unidad de análisis para varios momentos del tiempo, de periodicidad generalmente homogénea (diaria, mensual, trimestral, anual, etc.,).


#### Comportamiento del precio de la Mezcla Mexicana de Petróleo 11/20/2018. ![](/oil.jpg)

#### Comportamiento de la Temperatura Mundial 1880-2000 (°C). ![](/tseries.png)

#### Cociente de localización para Diabetes 1998-2015 Frontera Norte y Frontera Sur, México.
![](/panel.jpg)

Otras estructuras incluyen  **datos de panel** que básicamente agrupan series de corte transversal para diferentes momentos en el tiempo (ej. varios años).

```{r, echo=FALSE}

library(gapminder)

gapminder<-gapminder%>%
mutate(year1950=year-1950)%>%
  head(50)

gapminder
```

![](/panel1.jpg)

Note la variable que distingue la unidad de análisis **(country)** y la variable que incorpora la dimensión temporal para la estructura de panel **(year)**.


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

![](/panel2.jpg)

También note que la dimensión que denota tiempo (año) se encuentra registrada en una varible.

Así tenemos un data frame de 92 observaciones a lo largo del 2 años para 46 ciudades.

Una estructura de este tipo, donde la dimensión tiempo  se extiende por un periodo corto (ej, comparación ente 2 años). También se denomina comumnente como *pooled cross-section*.

Una ventaja importante de la estructura de datos de panel sobre cross-section es que nos permite **controlar por características no observadas** en un sólo período de tiempo entre las unidades de análisis.  


## Definiciones para implementación en R: 

### Objetos


#### Listas.

Este objeto, permite almacenar un grupo de vectores, cada elemento de la lista puede ser un vector, a diferencia  del caso de los vectores atómicos en donde se agrupan elementos individuales, en una lista cada "elemento" es un vector y estos puden ser de diferentes tipos, ej. numéricos, character strings, logicos. La función utilizada para crear una lista es `list()`

Ejemplo 


```{r}
lista<-list(100:130,"R",list(TRUE,FALSE)) 
lista 
```


La flexibilidad de este objeto es una ventaja ya que nos permite contar con una herramienta versátil de almacenamiento para agrupar cualquier objeto. 

### Data frames.

Este tipo de objeto es la versión bi-dimensional de una lista donde las **columnas** son vectores (variables) y cada **renglón** observaciones. Este es el tipo de objeto más útil para realizar el análisis de datos. Podemos pensar en un data frame como el equivalente de R a una hoja de cálculo de excel.

Un data frame agrupa los **vectores en columnas**, de tal forma que cada vector de un data frame puede contener un tipo de datos específico, pero cada celda dentro un vector tendrá la misma información. Asímismo, los vectores agrupados en un **data frame** son de la misma longitud. La figura siguiente muestra un ejemplo de esta configuración.

Ejemplo 1

![](/dataframe.jpg)

Ejemplo 2

![](/dataframe2.jpg)

#### Práctica.

Cargue en **R** la base de datos:   `repda_2021.csv` y determine que tipo de variables contiene así cmoo la estructura (ej. corte transversal, panel  o series de tiempo).

Cargamos un data frame (df) con la función read.csv(). Este df  esta alojado en un archivo de texto separado por comas **commas separeted values**  (.csv) nombrado **repda_2021.csvv** en la ruta indicada entre comillas: **"C:/Users/..."**. 

```{r}
library(tidyverse)
agua<-read.csv("C:/Users/josel/Desktop/on/web/MDR-intersemestral-2021/content/post/repda_2021.csv")

names(agua)
glimpse(agua)
str(agua)
class(agua)
```

Este contiene información consesiones para extracción de agua subterránea en el territorio nacional. Note que contiene 15 vectores (variables). Hemos  utilizado la función `glimpse()` del paquete `tidyverse`  para conocer el tipo de vectores almacenados en el DF y una función alternativa para conocer esta información  mediante la función `str()` structure.

Note que la clase del objeto `agua` es data.frame. También hemos extraído con la función `names()` los nombres de los vectores contenidos en el df.


## Scripts

Para evitar escribir todo el análisis nuevamente, el *work flow* recomendado en **R** es trabajar con **scripts**, estos son archivos de texto en donde almacenamos todo el código utilizado en nuestro análisis.

Aún mejor si deseamos podemos almacenar el código en un archivo R Markdown  [R Markdown](https://rmarkdown.rstudio.com/), lo que nos permite la flexibilidad de crear el resultado del análisis en diversos formatos incluido html. Sí, una página web para consultarla en internet que podemos alojar en servidores como [Netlify](https://www.netlify.com/) o repositorios como [Github](https://github.com/) y publicar el contenido usando **githubweb pages** .

![](/scripts.jpg)

Una vez que almacenamos el código en un script podemos ejecutar cada linea de este código (just hit enter en frente de la linea de código a ejecutar), seleccionar una porción  (y lo ejecutamos con ctr+enter) o bien ejecturar todo el **code chunk** (como le decimos en la comunidad **R** a las porciones de código de un script.) utilizando la función **Run** del menú superior. 


### Creación de objetos y lectura de archivos

Ara iniciar el análisis de datos cargamos una base que puede presentarse en una variaedad de formatos (uno muy comun es .csv ) o bien Podemos crear un objeto (ej. un dataframe o una lista de variables) en R y almacenarlo para su análisis, para lo cual asignamos un nombre usando el simbolo $<-$ y tenemos  los datos almacenados en la memoria, a esto le denominamos objetos. El simbolo será el equivalente a el $=$. Se lee igual a...
Esta notación es un estandar en R.

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
Importante: 
**Note:** You can name an object in R almost anything you want, but there are a few rules. First,
a name **cannot start with a number**. Second, a name cannot use some special symbols,
like **^, !, $, @, +, -, /, or * **: Note también que  los nombres son sensibles al uso de mayúsculas. Note que si el nombre asignado ya existe, el nuevo objeto sobre escribirá el objeto anterior.


Ejercicio 


Genere  un **dado virtual:**

```{r}
1:6
```

Este notación nos permite tener  un lista de números entre 1 y 6, pero es necesario almacenarlos. Para lo cual asignamos un nombre usando el simbolo $<-$ 

```{r}
Dado<-1:6
Dado
```

**Note:** Cuando creamos un objeto este aparece en la parte superior derecha en el área de environment

![](/environment.jpg)


```{r }
dado<-1:10
dado


dado<-1:6
dado

dice<-1:6
dice
```

¿Qué podemos hacer con el dado?


Comencemos por algunas operaciones aritméticas.


```{r}
dado-1

dado/2

dado*dado
```

Note que el resultado en cada caso es un vector del mismo tamaño  (en este caso 1x6). Si multiplicamos un vector de un tamaño inferior al primer factor, R replica los valores del vector de menor tamaño hasta alcanzar el tamaño del primero vertor y así aplica la operación para ambos vectores del mismo tamaño. 


Ahora que ya hemos realizado algo de artimética con el dado, veamos como podemos lanzarlo para obtener un número aleatorio. PAra este proposito necesitamos una función. 


## Funciones

Para realizar esta tarea de selección de un número aleatorio, necesitamos una función, en R tener una función es fácil únicamente necesitamos el **nombre** y los **argumentos** (entre paréntesis) sobre los cuales se aplicará dicha función. Algunos ejemplos de funciones disponibles de forma automática en R, incluyen :

```{r}
round(5.8)

round(3.1416)

factorial(3)
```

Los datos que pasamos en la función los denominamos **argumentos**. Estos pueden ser datos, funciones o resultados de otras funciones. 

Ejemplo: 

```{r}
mean(1:6)

mean(dado)

round(mean(dado))
```

Para nuestro propósito de obtener un número aleatorio en un lanzamiento de dado, podemos utilizar la funciòn sample, esta toma **dos argumentos**, el vector x y el tamaño de la muestra. 


```{r}
sample(x=dado,size=1)

sample(x=1:6,size=1)

```

Es posible omitir la etiqueta del argumetno si recordamos que argumento corresponde con la posicion, pero en funciones de mayor tamaño es de ayuda anotar el nombre ya que no siempre recordamos los nombres de todos los argumentos. 

```{r}
sample(dado,1)

sample(1:6,1)
```

Si necesitamos conocer los nombres de los argumentos de alguna funciòn pasamos el nombre de la funciona la funciòn `args()`, Ejemplo  `args(round)` 


```{r}
args(round)
```

**Note** que las funciones incluyen valores predeterminados para algunos argumentos, en el caso anterior el valor del argumento *digits* es 0, de modo que si omitimos este argumento, el resultado será el redondeo al entero próximo, sin decimales. 

```{r}
# Redondeo con dos digitos 
round(3.1416,2)
# Redondeo con un digito
round(3.1416,1)

# redondeo con parametro predeterminado.
round(3.1416)

```
## Muestreo con reemplazo.

Cuando aplicamos la función `sample(dado, size = 2)` notemos que nunca obtenemos dos veces el mismo valor, esto es la función de forma predeterminada considera una muestra aleatoria pero sin reemplazo, para evitar este comportamiento y poder simular el lanzamiento de un dado en realidad en donde podemos obtener por ejemplo el valor 3 y luego otro 3, es necesario inlcuir el argumeto `replace = TRUE`, esto permite que una vez que lanzamos el primer dado, sea posible obtener el mismo valor en el segundo lanzamiento, tal como sucede en el caso real.


```{r}
sample(dado, size = 2, replace = TRUE)
```

El muestreo con reemplazo es una manera fácil de crear muestras aleatorias simples. POr ejemplo simular correctamente el lanzamiento de un dado en el que obtenemos un numero aleatorio  independiente cada vez. 


Si deseas sumar el valor del dado para los dos lanzamientos, unicametne aplicamos la función de suma y tenemos el resultado de esta simulación con números aleatorios. 

```{r}
dados <- sample(dado, size = 2, replace = TRUE)
dados

dadosuma<-sum(dados)
dadosuma
```

Qué pasaria si indicamos el valor de *dados* varias veces, cambiará el valor obtenido cada vez que indicamos el nombre del objeto?

```{r}
dados

dados

dados 
```

Vemos que no obtenemos una nueva muestra aleatoria cada vez que indicamos el nombre del objeto, esto es lo que esperamos ya que una vez que aplicamos una función a un conjunto de argumentos y asignamos un nombre creamos un objeto y al llamarlo obtenemos el  resultado permanentemente.

Si queremos obtener un resultado distinto cada vez que lanzamos el dado podemos especificarlo por medio de una funciòn. 

## Escribe tus propias funciones.


Hasta ahora hemos creado estos objetos:

`dado<-1:6`  

`dados<-(dado,2,replace=TRUE)`

`sum(dados)`

No sería conveniente que escribiésemos estos objetos cada vez que necesitamos el resultado del lanzamiento. Para simplificar este proceso podemos construir una función que haga el trabajo por nosotros de manera automática.

Hagamos una funciòn llama `lanzar()`, esta función nos permitirá tener un el valor nuevo  para cada vez que lancemos los dados, sin tener que reescribir cada objeto. 


**Every function in R has three basic parts:** a **name**, **a body of code**, and **a set of arguments**.

To make your own function, you need to replicate these parts and store them in an R
object, which you can do with the *function* function. To do this, call function() and
follow it with a pair of **braces**, {}:

`mi_función <- function() {}`

```{r}
lanzar <- function() {
dado <- 1:6
dados <- sample(dado, size = 2, replace = TRUE)
sum(dados)
}

lanzar()
```

## Argumentos

Ahora vamos a incluir  argumentos a nuestra función.
Veamos que sucede cuando incluimos un objeto que no hemos definido, llamémos a este elemento  **tipo**, en lugar del objeto $dado<-1:6$. 

```{r}
lanzar2 <- function() {
dados <- sample(tipo, size = 2, replace = TRUE)
sum(dados)
}
```

`lanzar2()`

Obtenemos un error: **Error: object 'lanzar2' not found**. esto debido a que no existe el objeto **tipo**.

Este comportamiento de hecho nos permite incluir argumentos, para aplicar la función lo único que necesitamos hacer es indicar este elemento (tipo) como argumento. Al incluir argumentos en nuestra función, podemos en nuestro ejemplo, especificar diferentes tipos de **dados**. 

Recordemos que estamos haciendo dos lanzamientos con un dato de 6 lados, pero podemos especificar otros tipos de dados, como uno con 20 lados, uno con 4 o 3,etc. Esta información la indicamos mediante los argumentos.

```{r }
lanzar2 <- function(tipo) {
dados <- sample(tipo, size = 2, replace = TRUE)
sum(dados)
}

lanzar2(tipo=1:4)
lanzar2(tipo=1:20)
lanzar2(1:6)
```

`lanzar2(tipo)`

Note que no es necesario nombrar tipo explicitamente, aunque lo podemos hacer para mayor claridad, esto no es necesario por que  tipo es el único argumento de nuestra función `lanzar2()`.

Note que la función resulta en un Error, cuando no proporcionamos  el argumento tipo  ej. `lanzar2()`. Esto es interesante por que de hecho podemos especificar **argumentos predeterminados** al momento de construir la función de tal forma que podemos dejar vacio este espacio cuando estimamos la función. 

```{r}
lanzar2 <- function(tipo=1:6) {
dados <- sample(tipo, size = 2, replace = TRUE)
sum(dados)
}

lanzar2()

lanzar2(1:12)
```

Ahora cuando llamamos la función, obtenemos la información solicitada!

Ahora es posible proporcionar un tipo de dado particular cada vez que lanzamos el dado o bien si preferimos dejar el argumento en blanco y la función aplicará el valor predeterminado para el argumento tipo.


En síntesis el proceso para crear una función involucra las siguientes partes:

![](/Funciones.jpg)




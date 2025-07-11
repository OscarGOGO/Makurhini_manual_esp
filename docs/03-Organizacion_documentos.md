# Organización de documentos y carpetas en el repositorio

Este repositorio se puede usar para la generación de tablas, vectores, raster, etc. que sirven principalmente de entrada para las gráficas en la plataforma Biodiversidades.

En el repositorio se incluyen entradas, scripts y salidas para el tablero de datos y el tablero geoespacial.

Probablemente los usuarios más frecuentes del repositorio sean las personas que programen en la SEE, es por eso que sería de gran valía sugerir un arreglo de archivos y carpetas del repositorio. Si el repositorio y su arreglo se realiza por parte de un externo sería bueno considerar las sugerencias aquí propuestas.

Se sugiere que las carpetas y archivos tengan un órden jerárquico y que los nombres de las carpetas inicien con una numeración a dos dígitos y guión bajo (p. ej., 00\_, 01\_, 02\_) seguido de nombres cortos, sin espacios y sin acentos.

A continuación, se enumeran algunas de las sugerencias de arreglo en repositorio:

1.  Cuatro carpetas principales, **00_Admin, 01_Entradas, 02_Scripts, 03_Salidas**.

![](C:/Users/ogodinez/Documents/CnM/PruebaLibro/Libro_Prueba1/images/31.png){width="400"}

2.  La carpeta **00_Admin** contiene información general que puede ser relevante para entender los archivos de entrada. Los archivos pueden ser, por ejemplo, presentaciones, metadatos de insumos, metadatos de scripts, pruebas, documentos, archivos README, etc. Debido a las limitaciones de almacenamiento en los administradores de repositorios se sugiere no incorporar archivos de gran tamaño; los archivos de gran tamaño pueden destinarse a la carpeta de trabajo en el disco **e\$(\\gap) (Ver siguiente sección)**.

![](C:/Users/ogodinez/Documents/CnM/PruebaLibro/Libro_Prueba1/images/32.png){width="500"}

3.  La carpeta **01_Entradas** contiene las subcarpetas **01_Funciones** y **02_Temporales**.

![](C:/Users/ogodinez/Documents/CnM/PruebaLibro/Libro_Prueba1/images/33.png){width="500"}

La subcarpeta **01_Funciones** contiene funciones de R (formatos: .R, .RData o .rds que se ejecutan con source()) que son usados comúnmente en los scripts de diversas secciones de la plataforma (p.ej., archivo de R que contiene las funciones de consulta al SNIB que se usan en varios indicadores). Mientras que en la subcarpeta **02_temporales** se encuentran archivos temporales (archivos vectoriales, raster, tablas o funciones) que no son de gran tamaño y que son de utilidad para correr de forma fluida los scripts de R. Los archivos de gran tamaño se recomienda alojarlos en la carpeta de trabajo en el disco **e\$(\\gap) (Ver sección 4)**.

4.  La carpeta **02_Scripts** tiene dos subcarpetas que corresponden al Tablero de datos (**01_Tablero_datos**) y al Tablero geoespacial (**02_Tablero_geoespacial**). Dentro de cada carpeta existe un archivo .R o script ("Leader") con las líneas de código necesarias para el procesamiento de todos los elementos/indicadores que permiten obtener las salidas para implementar los gráficos o mapas de los tableros. Para correr los scripts de los temas basta con usar la función source() (para obtener más información consultar la presentación Arreglo jerárquico).

![](C:/Users/ogodinez/Documents/CnM/PruebaLibro/Libro_Prueba1/images/34.png){width="500"}

En las subcarpetas **01_Tablero_datos** y **02_Tablero_geoespacial**, se integran otras cuatro carpetas que corresponden a los cuatro grandes temas de la plataforma BiodiversidadES (**01_Conocimiento, 02_Cambio_global, 03_Avances_hacia_sustentabilidad, 04_Escenarios**).

![](C:/Users/ogodinez/Documents/CnM/PruebaLibro/Libro_Prueba1/images/35.png){width="500"}

5.  La carpeta **03_Salidas** contiene las salidas de los *scripts* de R contenidos en la carpeta **02_Scripts**. Los formatos de salida serán acordados con el programador de la plataforma BriodiversidadES, sin embargo, los formatos más usuales son *vectoriales, tablas e imágenes*. La carpeta **03_Salidas** contiene dos subcarpetas que corresponden al Tablero de datos (**01_Tablero_datos**) y al Tablero geoespacial (**02_Tablero_geoespacial**). Cada carpeta contiene cuatro carpetas que corresponden a los cuatro grandes temas de la plataforma BiodiversidadES y a su vez estas cuatro carpetas contienen carpetas con el nombre de las secciones.

![](C:/Users/ogodinez/Documents/CnM/PruebaLibro/Libro_Prueba1/images/36.png){width="600"}

### Ventajas

-   Tenemos un script principal (*00_Lider\_*) que tiene las condicionales y funciones generales guardadas en archivos .R y que se corren como *sources*

-   Cada source corresponde a una sección

-   Cada source tiene cientos de líneas que se pueden trabajar de forma independiente

-   Se evita tener un único script con miles de líneas difícil de manejar

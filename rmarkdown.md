
# R Markdown

## Introduction
## Introducción


R Markdown provides an unified authoring framework for data science, combining your code, its results, and your prose commentary. R Markdown documents are fully reproducible and support dozens of output formats, like PDFs, Word files, slideshows, and more. 

R Markdown provee  un marco de referencia para la ciencia de datos, combinando tu código, sus resultados, y tus comentarios en prosa. Los documentos de R Markdown son completamente reproducibles y soportan docenas de formatos de salida tales como PDFs, archivos de Word, presentaciones y más.

R Markdown files are designed to be used in three ways:
Los archivos R Markdown están diseñados para ser usados de tres maneras:

1.  For communicating to decision makers, who want to focus on the conclusions,
    not the code behind the analysis.
    
1.  Para comunicarse con los tomadores de decisiones, quienes desean enfocarse en las     conclusiones, no en el código que subyace al análisis.

1.  For collaborating with other data scientists (including future you!), who
    are interested in both your conclusions, and how you reached them (i.e.
    the code).
    
1. Para colaborar con otros científicos de datos (incluyendo a tu yo futuro !!),         quienes están interesados tanto en tus conclusiones como en el modo en el que         llegaste a ellas (es decir, el código).

    
1.  As an environment in which to _do_ data science, as a modern day lab 
    notebook where you can capture not only what you did, but also what you
    were thinking.
    
1.  Como un ambiente en el cual _hacer_ ciencia de datos, como un *notebook* de           laboratorio moderno donde puedes capturar no sólo que hiciste, sino también           estabas pensando cuando lo hacías.    

R Markdown integrates a number of R packages and external tools. This means that help is, by-and-large, not available through `?`. Instead, as you work through this chapter, and use R Markdown in the future, keep these resources close to hand:

R Markdown integra una cantidad de paquetes de R y herramientas externas. Esto implica que la ayuda ,en general, no está disponible a través de ` ?`. En su lugar, mientras trabajas a lo largo de este capitulo, y utilizas R Markdown en el futuro, mantén estos recursos cerca:

*   R Markdown Cheat Sheet: _Help > Cheatsheets > R Markdown Cheat Sheet_,

*   R Markdown Reference Guide: _Help > Cheatsheets > R Markdown Reference 
    Guide_.
    
*   Hoja de referencia de R Markdown : _Help > Cheatsheets > R Markdown Cheat Sheet_

*   Guía de referencia R Markdown  : _Help > Cheatsheets > R Markdown Reference 
    Guide_

Both cheatsheets are also available at <http://rstudio.com/cheatsheets>.
Ambas hojas también se encuentran disponibles en http://rstudio.com/cheatsheets>.


### Prerequisites
### Prerequisitos

You need the __rmarkdown__ package, but you don't need to explicitly install it or load it, as RStudio automatically does both when needed.

Necesitas el paquete __rmarkdown__, pero no necesitas cargarlo o instalarlo explícitamente ya que RStudio hace ambas acciones automaticamente cuando es necesario.





## R Markdown basics
## R Markdown básico

This is an R Markdown file, a plain text file that has the extension `.Rmd`:

Este es un archivo R Markdown, un archivo de texto plano que tiene la extensión `.Rmd`:

````
---
title: "Diamond sizes"
date: 2016-08-25
output: html_document
---

```{r setup, include = FALSE}
library(ggplot2)
library(dplyr)

smaller <- diamonds %>%
  filter(carat <= 2.5)
```

We have data about `r nrow(diamonds)` diamonds. Only 
`r nrow(diamonds) - nrow(smaller)` are larger than
2.5 carats. The distribution of the remainder is shown
below:

```{r, echo = FALSE}
smaller %>%
  ggplot(aes(carat)) +
  geom_freqpoly(binwidth = 0.01)
```
````

It contains three important types of content:

1.  An (optional) __YAML header__ surrounded by `---`s.
1.  __Chunks__ of R code surrounded by ```` ``` ````.
1.  Text mixed with simple text formatting like `# heading` and `_italics_`.

Contiene tres tipos importantes de contenido:
  1. Un encabezado YAML (opcional) rodeado de `---` 
  1. __Bloques__ de código de R rodeado de ```` ``` ````.
  1. Texto mezclado con texto simple formateado con `# Encabezado` e `_itálicas_`.

When you open an `.Rmd`, you get a notebook interface where code and output are interleaved. You can run each code chunk by clicking the Run icon (it looks like a play button at the top of the chunk), or by pressing Cmd/Ctrl + Shift + Enter. RStudio executes the code and displays the results inline with the code:

Cuando abres un archivo `.Rmd`, obtienes una interfaz de *notebook* donde el código y el *output* están intercalados. Puedes ejecutar cada bloque de código haciendo clic el ícono ejecutar ( se parece a un botón de reproducir en la parte superior del bloque de código), o presionando Cmd/Ctrl + Shift + Enter. RStudio ejecuta el código y muestra los resultados incustrados en el código:
  

<img src="rmarkdown/diamond-sizes-notebook.png" width="75%" style="display: block; margin: auto;" />

To produce a complete report containing all text, code, and results, click "Knit" or press Cmd/Ctrl + Shift + K.  You can also do this programmatically with `rmarkdown::render("1-example.Rmd")`. This will display the report in the viewer pane, and create a self-contained HTML file that you can share with others.

Para producir un reporte completo que contenga todo el texto, código y resultados, hacerclic en "Knit" o presionar Cmd/Ctrl + Shift + K. Puede hacerse tambien de manera programática con `rmarkdown::render("1-example.Rmd")`. Esto mostrará el reporte en el panel  *viewer* y crea un archivo HTML independiente que puedes compartir con otros.

<img src="rmarkdown/diamond-sizes-report.png" width="75%" style="display: block; margin: auto;" />

When you __knit__ the document, R Markdown sends the .Rmd file to __knitr__, http://yihui.name/knitr/, which executes all of the code chunks and creates a new markdown (.md) document which includes the code and its output. The markdown file generated by knitr is then processed by __pandoc__, <http://pandoc.org/>, which is responsible for creating the finished file. The advantage of this two step workflow is that you can create a very wide range of output formats, as you'll learn about in [R markdown formats].

Cuando haces *knit* el documento (knit en español significa tejer), R Markdown envía el .Rmd a _knitr_, http://yihui.name/knitr/, que ejecuta todos los bloques de código y crea un nuevo documento markdown (.md) que incluye el código y su output. El archivo markdown generado por _knitr_ es procesado entonces por pandoc, http://pandoc.org/, que es el responsable de crear el archivo terminado. La ventaja de este flujo de trabajo en dos pasos es que puedes crear un muy amplio rango de formatos de salida, como aprenderás en [Formatos de R markdown ].

<img src="images/RMarkdownFlow.png" width="75%" style="display: block; margin: auto;" />

To get started with your own `.Rmd` file, select *File > New File > R Markdown...* in the menubar. RStudio will launch a wizard that you can use to pre-populate your file with useful content that reminds you how the key features of R Markdown work. 

Para comenzar con tu propio archivo `.Rmd`, selecciona *File > New File > R Markdown...* en la barra de menú. Rstudio iniciará un asistente que puedes usar para pre-rellenar tu archivo con contenido útil que te recuerde como funcionan las principales características de R Markdown.



The following sections dive into the three components of an R Markdown document in more details: the markdown text, the code chunks, and the YAML header.

Las siguientes secciones profundizan en los tres componentes de un documento de R Markdown en más detalle: el texto markdown, los bloques de código y el encabezado YAML.

### Exercises

1.  Create a new notebook using _File > New File > R Notebook_. Read the 
    instructions. Practice running the chunks. Verify that you can modify
    the code, re-run it, and see modified output.
    
1.  Crea un nuevo *notebook* usando _File > New File > R Notebook_. Lee las               instrucciones. Practica ejecutando los bloques. Verifica que puedes modificar el       código,re-ejecútalo, y observa la salida modificada.
        
    
1.  Create a new R Markdown document with _File > New File > R Markdown..._
    Knit it by clicking the appropriate button. Knit it by using the 
    appropriate keyboard short cut. Verify that you can modify the
    input and see the output update.
    
1.  Crea un nuevo documento R Markdown con _File > New File > R Markdown..._
    Haz clic en el icono apropiado de *Knit*. Haz *Knit* usando  el atajo de teclado      apropiado. Verifica que puedes modificar el *input*  y  la actualizacion del         *output*.
    
1.  Compare and contrast the R notebook and R markdown files you created
    above. How are the outputs similar? How are they different? How are
    the inputs similar? How are they different? What happens if you
    copy the YAML header from one to the other?

1.  Compara y contrasta el *notebook* de R con los archivos de R markdown que has         creado antes. ¿Cómo son similares los outputs? ¿Cómo son diferentes? ¿Cómo son        similares los inputs? ¿En qué se diferencian? ¿Qué ocurre si copias el encabezado     YAML de uno al otro?

1.  Create one new R Markdown document for each of the three built-in
    formats: HTML, PDF and Word. Knit each of the three documents.
    How does the output differ? How does the input differ? (You may need
    to install LaTeX in order to build the PDF output --- RStudio will
    prompt you if this is necessary.)
    
1.  Crea un nuevo documento R Markdown para cada uno de los tres formatos                 incorporados: HTML, PDF and Word. Haz *knit* en cada uno de estos tres documentos.     ¿Como difiere el output? ¿Cómo difiere el input? (Puedes necesitar instalar LaTeX     para poder compilar el output en PDF--- RStudio preguntará si esto es necesario).    

## Text formatting with Markdown
## Formateo de texto con Markdown

Prose in `.Rmd` files is written in Markdown, a lightweight set of conventions for formatting plain text files. Markdown is designed to be easy to read and easy to write. It is also very easy to learn. The guide below shows how to use Pandoc's Markdown, a slightly extended version of Markdown that R Markdown understands.

La prosa en los archivos `.Rmd` está escrita en Markdown, un set liviano de convenciones para dar formato a archivos de texto plano. Markdown está diseñado para ser fácil de leer y fácil de escribir. Es tambien muy fácil de aprender. La guía abajo muestra como usar el Markdown de Pandoc, una version ligeramente extendida de markdown que R Markdown comprende.


```
Text formatting 
------------------------------------------------------------

*italic*  or _italic_
**bold**   __bold__
`code`
superscript^2^ and subscript~2~

Headings
------------------------------------------------------------

# 1st Level Header

## 2nd Level Header

### 3rd Level Header

Lists
------------------------------------------------------------

*   Bulleted list item 1

*   Item 2

    * Item 2a

    * Item 2b

1.  Numbered list item 1

1.  Item 2. The numbers are incremented automatically in the output.

Links and images
------------------------------------------------------------

<http://example.com>

[linked phrase](http://example.com)

![optional caption text](path/to/img.png)

Tables 
------------------------------------------------------------

First Header  | Second Header
------------- | -------------
Content Cell  | Content Cell
Content Cell  | Content Cell
```

The best way to learn these is simply to try them out. It will take a few days, but soon they will become second nature, and you won't need to think about them. If you forget, you can get to a handy reference sheet with *Help > Markdown Quick Reference*.

La mejor manera de aprender es simplemente probar. Tomará unos días, pero pronto se convertirá en algo natural, y no necesitarás pensar en ellas. Si te olvidas, puedes tener una útil hoja de referencia con *Help > Markdown Quick Reference*.

### Exercises
### Ejercicios


1.  Practice what you've learned by creating a brief CV. The title should be
    your name, and you should include headings for (at least) education or
    employment. Each of the sections should include a bulleted list of
    jobs/degrees. Highlight the year in bold.
    
1.  Practica lo que has aprendido crando un CV breve. El título debería ser tu nombre,     y  deberías incluir encabezados para (por lo menos) educación o empleo. Cada una      de las secciones debería incluir una lista punteada de trabajos/ títulos              obtenidos.  Resalta año en negrita.    
    
1.  Using the R Markdown quick reference, figure out how to:
1.  Usando  la referencia rapida de R Markdown, descubre como:

    1.  Add a footnote.
    1.  Add a horizontal rule.
    1.  Add a block quote.
    
    1.  Agregar una nota al pie.
    1.  Agregar una linea horizontal.
    1.  Agregar una cita en bloque.    
    
1.  Copy and paste the contents of `diamond-sizes.Rmd` from
    <https://github.com/hadley/r4ds/tree/master/rmarkdown> in to a local
    R markdown document. Check that you can run it, then add text after the 
    frequency polygon that describes its most striking features.
    
1.  Copia y pega los contenidos de `diamond-sizes.Rmd` desde                              <https://github.com/hadley/r4ds/tree/master/rmarkdown> a un documento local de R      Markdown. Revisa que puedes ejecutarlo,  agrega texto despues del poligono de         frecuencias que describa sus caracteristicas más llamativas.    

## Code chunks
## Bloques de código

To run code inside an R Markdown document, you need to insert a chunk. There are three ways to do so:
Para ejecutar código dentro de un documento R Markdown, necesitas insertar un bloque.
Hay tres maneras para hacerlo:

1. The keyboard shortcut Cmd/Ctrl + Alt + I

1. El atajo de teclado Cmd/Ctrl + Alt + I

1. The "Insert" button icon in the editor toolbar.

1. El icono "Insertar" en la barra de edición 

1. By manually typing the chunk delimiters ` ```{r} ` and ` ``` `.

1. Tipeando manualmente los delimitadores de bloque ` ```{r} ` y ` ``` `.


Obviously, I'd recommend you learn the keyboard shortcut. It will save you a lot of time in the long run!

Obviamente, recomendaría que aprendieras a usar el atajo de teclado. A largo plazo, te ahorrará mucho tiempo.

You can continue to run the code using the keyboard shortcut that by now (I hope!) you know and love: Cmd/Ctrl + Enter. However, chunks get a new keyboard shortcut: Cmd/Ctrl + Shift + Enter, which runs all the code in the chunk. Think of a chunk like a function. A chunk should be relatively self-contained, and focussed around a single task. 

Puedes continuar ejecutando el código usando el atajo de teclado que para este momento (espero!) ya conoces y amas : Cmd/Ctrl + Enter. Sin embargo, los bloques de código tienen otro atajo de teclado: Cmd/Ctrl + Shift + Enter, que ejecuta todo el código en el bloque. Piensa el bloque como una función. Un bloque debería ser relativamente autónomo,y enfocado alrededor de una sola tarea.


The following sections describe the chunk header which consists of ```` ```{r ````, followed by an optional chunk name, followed by comma separated options, followed by `}`. Next comes your R code and the chunk end is indicated by a final ```` ``` ````.

Las siguientes secciones decriben el encabezado de bloque que consiste en ```` ```{r ````, seguido por un nombre opcional para el bloque, seguido entonces por opciones separadas por comas, y concluyendo con `}`. Inmediatamente después sigue tu código de R el bloque y el fin del bloque se indica con un  ```` ``` ```` final.

### Chunk name
### Nombres en bloques

Chunks can be given an optional name: ```` ```{r by-name} ````. This has three advantages:
Los bloques puede tener opcionalmente nombres : ```` ```{r nombre} ````. Esto presenta tres ventajas:

1.  You can more easily navigate to specific chunks using the drop-down
    code navigator in the bottom-left of the script editor:
    
1.  Puedes navegar más fácilmente a bloques específicos usando el navegador de código     desplegable abajo a la izquierda en el editor de *script*:
    <img src="screenshots/rmarkdown-chunk-nav.png" width="30%" style="display: block; margin: auto;" />

1.  Graphics produced by the chunks will have useful names that make
    them easier to use elsewhere. More on that in [other important options].
1.  Los gráficos producidos por los bloques tendrán nombres útiles que hace que sean      más fáciles de utilizar en otra parte.  Máa sobre esto en [otras opciones             importantes].    
    
1.  You can set up networks of cached chunks to avoid re-performing expensive
    computations on every run. More on that below.
1.  Puedes crear redes de bloque cacheados para evitar re-ejecutar computos costosos      en cada ejecucion. Más sobre esto mas adelante.     

There is one chunk name that imbues special behaviour: `setup`. When you're in a notebook mode, the chunk named setup will be run automatically once, before any other code is run.

Hay un nombre de bloque que tiene comportamiento especial: `setup`. Cuando te encuentras en modo *notebook*, el bloque llamado setup se ejecutará automáticamente una vez, antes de ejecutar cualquier otro código.


### Chunk options
### Opciones los bloques

Chunk output can be customised with __options__, arguments supplied to chunk header. Knitr provides almost 60 options that you can use to customize your code chunks. Here we'll cover the most important chunk options that you'll use frequently. You can see the full list at <http://yihui.name/knitr/options/>. 

La salida de los bloques puede personalizarse con __options__, argumentos suministrados al encabezado del bloque. Knitr provee casi 60 opciones para que puedas usar para personalizar tus bloques de código. Aqui cubriremos las opciones de bloques mas imporantes que usaras más frecuentemente. Puedes ver la lista completa en <http://yihui.name/knitr/options/>. 

The most important set of options controls if your code block is executed and what results are inserted in the finished report:

El set de opciones más importantes  controla si tu bloque de código es ejecutado y que resultados estarán insertos en el reporte terminado: 
  
*   `eval = FALSE` prevents code from being evaluated. (And obviously if the
    code is not run, no results will be generated). This is useful for 
    displaying example code, or for disabling a large block of code without 
    commenting each line.
    
*   `eval = FALSE` evita que código sea evaluado. (Y obviamente si el código no es         ejecutado no se generaran resultados). Esto es útil para mostrar códigos de           ejemplo,o para deshabilitar un gran bloque de código sin comentar cada línea.   

*   `include = FALSE` runs the code, but doesn't show the code or results 
    in the final document. Use this for setup code that you don't want
    cluttering your report.
    
*   `include = FALSE` ejecuta el código, pero no muestra el código o los resultados       en el documento final. Usa esto para que código de configuracion que no quieres       que abarrote tu reporte.    

*   `echo = FALSE` prevents code, but not the results from appearing in the 
    finished file. Use this when writing reports aimed at people who don't
    want to see the underlying R code.
    
*   `echo = FALSE` evita que se vea el código, pero no los resultados en el archivo       final. Utiliza esto cuando quieres escribir reportes enfocados a personas que no      quieren ver el código subyacente de R.    

    
*   `message = FALSE` or `warning = FALSE` prevents messages or warnings 
    from appearing in the finished file.

*   `message = FALSE` o `warning = FALSE` evita que aparezcan mensajes o advertencias      en el archivo final.

*   `results = 'hide'` hides printed output; `fig.show = 'hide'` hides
    plots.
    
*   `results = 'hide'` oculta el *output* impreso; `fig.show = 'hide'` oculta             graficos.    

*   `error = TRUE` causes the render to continue even if code returns an error.
    This is rarely something you'll want to include in the final version
    of your report, but can be very useful if you need to debug exactly
    what is going on inside your `.Rmd`. It's also useful if you're teaching R
    and want to deliberately include an error. The default, `error = FALSE` causes 
    knitting to fail if there is a single error in the document.
    
*   `error = TRUE`  causa que el *render* continúe incluso si el código devuelve un error. Esto es algo que raramente quieres incluir en la version final de tu reporte, pero puede ser muy útil si necesitas depurar exactamente que ocurre dentro de tu `.Rmd`. Es también útil si estas enseñando R y quieres incluir deliberadamente un error. Por defecto, `error = FALSE` provoca que el *knitting* falle si hay incluso un error en el documento.    
    
The following table summarises which types of output each option supressess:
La siguiente tabla resume que tipos de *output*suprime cada opción:

Option             | Run code | Show code | Output | Plots | Messages | Warnings 
-------------------|----------|-----------|--------|-------|----------|---------
`eval = FALSE`     | -        |           | -      | -     | -        | -
`include = FALSE`  |          | -         | -      | -     | -        | -
`echo = FALSE`     |          | -         |        |       |          |
`results = "hide"` |          |           | -      |       |          | 
`fig.show = "hide"`|          |           |        | -     |          |
`message = FALSE`  |          |           |        |       | -        |
`warning = FALSE`  |          |           |        |       |          | -


Opción             | Ejecuta  | Muestra   | Output | Graficos | Mensajes |Advertencias                    | código   | código    |        |          |          |
-------------------|----------|-----------|--------|----------|----------|---------
`eval = FALSE`     | -        |           | -      | -        | -        | -
`include = FALSE`  |          | -         | -      | -        | -        | -
`echo = FALSE`     |          | -         |        |          |          |
`results = "hide"` |          |           | -      |          |          | 
`fig.show = "hide"`|          |           |        | -        |          |
`message = FALSE`  |          |           |        |          | -        |
`warning = FALSE`  |          |           |        |          |          | -

### Table
### Tablas
By default, R Markdown prints data frames and matrices as you'd see them in the console:
Por defecto, R Markdown imprime data frames y matrices tal como se ven en la consola:


```r
mtcars[1:5, ]
#>                    mpg cyl disp  hp drat   wt qsec vs am gear carb
#> Mazda RX4         21.0   6  160 110 3.90 2.62 16.5  0  1    4    4
#> Mazda RX4 Wag     21.0   6  160 110 3.90 2.88 17.0  0  1    4    4
#> Datsun 710        22.8   4  108  93 3.85 2.32 18.6  1  1    4    1
#> Hornet 4 Drive    21.4   6  258 110 3.08 3.21 19.4  1  0    3    1
#> Hornet Sportabout 18.7   8  360 175 3.15 3.44 17.0  0  0    3    2
```

If you prefer that data be displayed with additional formatting you can use the `knitr::kable` function. The code below generates Table \@ref(tab:kable).
Si prefieres que los datos tengan formato adicional puedes usar la función `knitr::kable`. El siguente código genera una Tabla \@ref(tab:kable).


```r
knitr::kable(
  mtcars[1:5, ], 
  caption = "Un kable de knitr."
)
```



Table: (\#tab:kable)Un kable de knitr.

                      mpg   cyl   disp    hp   drat     wt   qsec   vs   am   gear   carb
------------------  -----  ----  -----  ----  -----  -----  -----  ---  ---  -----  -----
Mazda RX4            21.0     6    160   110   3.90   2.62   16.5    0    1      4      4
Mazda RX4 Wag        21.0     6    160   110   3.90   2.88   17.0    0    1      4      4
Datsun 710           22.8     4    108    93   3.85   2.32   18.6    1    1      4      1
Hornet 4 Drive       21.4     6    258   110   3.08   3.21   19.4    1    0      3      1
Hornet Sportabout    18.7     8    360   175   3.15   3.44   17.0    0    0      3      2

Read the documentation for `?knitr::kable` to see the other ways in which you can customise the table. For even deeper customisation, consider the __xtable__, __stargazer__, __pander__, __tables__, and __ascii__ packages. Each provides a set of tools for returning formatted tables from R code.

Lee la documentación para `?knitr::kable` para ver los otros modos en los que puedes personalizar la tabla. Para una mayor personalización, considera los paquetes  __xtable__, __stargazer__, __pander__, __tables__, y __ascii__. Cada uno provee un set de herramientas para generar tablas con formato a partir código de R.

There is also a rich set of options for controlling how figures are embedded. You'll learn about these in [saving your plots].
Hay tambien una gran cantidad de opciones para controlar como las figuras estan embebidas o incrustadas. Aprenderás sobre esto en [ guardando tus gr<ficos].

### Caching
### Caching

Normally, each knit of a document starts from a completely clean slate. This is great for reproducibility, because it ensures that you've captured every important computation in code. However, it can be painful if you have some computations that take a long time. The solution is `cache = TRUE`. When set, this will save the output of the chunk to a specially named file on disk. On subsequent runs, knitr will check to see if the code has changed, and if it hasn't, it will reuse the cached results.

Normalmente, cada *knit* de un documento empieza desde una sesión limpia. Esto es genial para reproducibilidad, porque se asegura que has capturado cada cómputo importante en el código. Sin embargo, puede ser dolorosos si tienes cómputos que toman mucho tiempo. La solución es `cache = TRUE`. Cuando está funcionando, esto guarda el output del bloque a un archivo especialmente en el disco. En corridas subsecuentes, _knitr_ revisara si el código ha cambiado y si no ha cambiado, reutilizará los resultados del cache.

The caching system must be used with care, because by default it is based on the code only, not its dependencies. For example, here the `processed_data` chunk depends on the `raw_data` chunk:


El sistema de cache debe ser usado con cuidado, porque por defecto está solo basado en el código, no en sus dependencias. Por ejemplo , aqui el bloque `datos_procesados` depende del bloque `datos_crudos`:


    ```{r datos_crudos}
    datosCrudos <- readr::read_csv("un_archivo_muy_grande.csv")
    ```
    
    ```{r datos_procesados, cache = TRUE}
    datosProcesados <- datosCrudos %>% 
      filter(!is.na(variableImportada)) %>% 
      mutate(nuevaVariable = transformacionComplicada(x, y, z))
    ```


Caching the `processed_data` chunk means that it will get re-run if the dplyr pipeline is changed, but it won't get rerun if the `read_csv()` call changes. You can avoid that problem with the `dependson` chunk option:

    ```{r processed_data, cache = TRUE, dependson = "raw_data"}
    processed_data <- rawdata %>% 
      filter(!is.na(import_var)) %>% 
      mutate(new_variable = complicated_transformation(x, y, z))
    ```

*Cacheing* el bloque `processed_data` significa que tendrá que re-ejecutar si cambia el  pipeline de _dplyr_, pero no podra reejecutarlo si cambia el `read_csv()`. Puedes evitar este problema con la opción de bloque  `dependson`:

    ````{r datos_procesados, cache = TRUE, dependson = "raw_data"}
    datosProcesados <- datosCrudos %>% 
      filter(!is.na(variableImportada)) %>% 
      mutate(nuevaVariable = transformacionComplicada(x, y, z))
    ```

`dependson` should contain a character vector of *every* chunk that the cached chunk depends on. Knitr will update the results for the cached chunk whenever it detects that one of its dependencies have changed.

`dependson` deberia incluir un vector de caracteres para *cada* bloque que el bloque cached depende. _Knitr_ actualizará los resultados para el vector cached cada vez que detecta que una de sus dependencias ha cambiado.

Note that the chunks won't update if `a_very_large_file.csv` changes, because knitr caching only tracks changes within the `.Rmd` file. If you want to also track changes to that file you can use the `cache.extra` option. This is an arbitrary R expression that will invalidate the cache whenever it changes. A good function to use is `file.info()`: it returns a bunch of information about the file including when it was last modified. Then you can write:

    ```{r raw_data, cache.extra = file.info("a_very_large_file.csv")}
    rawdata <- readr::read_csv("a_very_large_file.csv")
    ```
    
    
Nota que los bloques de código no se actualizaran si el archivo `un_archivo_muy_grande.csv` cambia, porque _knitr_ hace *cache* solo los cambios dentro del archivo `.Rmd`. Si quieres seguir los cambios a ese archivo puedes usar la opción `cache.extra`. Esta es una expresión arbritaria de R que invalidará el *cache* cada vez que cambie. Una buena función a usar es `file.info()`: genera mucha información sobre el archivo incluyendo cuando fue su última modificación. Puedes escribir entonces:

    ```{r raw_data, cache.extra = file.info("a_very_large_file.csv")}
    rawdata <- readr::read_csv("a_very_large_file.csv")
    ```
    
    ```{r datos_crudos, cache.extra = file.info("un_archivo_muy_grande.csv")}
    datosCrudos <- readr::read_csv("un_archivo_muy_grande.csv")
    ```    

As your caching strategies get progressively more complicated, it's a good idea to regularly clear out all your caches with `knitr::clean_cache()`.

A medida que tus estrategias de *caching* se vuelven progresivamente mas complicadas, es una buena idea limpiar regularmente todos tus *caches* con `knitr::clean_cache()`.

I've used the advice of [David Robinson](https://twitter.com/drob/status/738786604731490304) to name these chunks: each chunk is named after the primary object that it creates. This makes it easier to understand the `dependson` specification.

Seguiendo el consejo de [David Robinson](https://twitter.com/drob/status/738786604731490304) para nombrar estos bloques: cada bloque esta nombrado por el objeto primario que crea. Esto hace mucho más fácil entender la especificacion `dependson`.

### Global options
### Opciones globales

As you work more with knitr, you will discover that some of the default chunk options don't fit your needs and you want to change them. You can do this by calling `knitr::opts_chunk$set()` in a code chunk. For example, when writing books and tutorials I set:

A medida que trabajes más con _knitr_, descubrirás que algunas de las opciones de bloque por defecto no se ajustan a tus necesidades y querrás cambiarlas. Puedes hacer esto incluyendo
`knitr::opts_chunk$set()` en un bloque de código. Por ejemplo, cuando escribo libros y tutoriales seteo:


```r
knitr::opts_chunk$set(
  comment = "#>",
  collapse = TRUE
)

```

This uses my preferred comment formatting, and ensures that the code and output are kept closely entwined. On the other hand, if you were preparing a report, you might set:

Esto utiliza mi formato preferido de comentarios, y se asegura que el código y el *output* se mantienen entrelazados. Por otro lado, si preparas un reporte, puedes setear:

```r
knitr::opts_chunk$set(
  echo = FALSE
)
```

That will hide the code by default, so only showing the chunks you deliberately choose to show (with `echo = TRUE`). You might consider setting `message = FALSE` and `warning = FALSE`, but that would make it harder to debug problems because you wouldn't see any messages in the final document.

Esto ocultara el código por defecto, asi que solo mostrará los bloques que deliberadamente has elegido mostrar( con `echo = TRUE`). Puedes considerar setear `message = FALSE` y `warning = FALSE`, pero eso puede hacer mas díficil de depurar problemas porque no verías ningun mensajes en el documento final.

### Inline code
### Código en la línea

There is one other way to embed R code into an R Markdown document: directly into the text, with:  `` `r ` ``. This can be very useful if you mention properties of your data in the text. For example, in the example document I used at the start of the chapter I had:

Hay otro modo de incrustar código R en un documento R Markdown: directamente en el texto, con:`` `r ` ``. Esto  puede ser muy útil si mencionas propiedades de tu datos en el texto. Por ejemplo, en el documento de ejemplo que utilice al comienzo del capitulo tenia:

> We have data about `` `r nrow(diamonds)` `` diamonds. 
> Only `` `r nrow(diamonds) - nrow(smaller)` `` are larger 
> than 2.5 carats. The distribution of the remainder is shown below:

> Tenemos datos sobre `` `r nrow(diamonds)` `` diamantes. 
> Solo `` `r nrow(diamonds) - nrow(smaller)` `` son mayores que 
>  2.5 quilates. La distribucion de lo restante se muestra abajo:

When the report is knit, the results of these computations are inserted into the text:


Cuando hacemos *knit*, los resultados de estos computós estan insertos en el texto:

> We have data about 53940 diamonds. Only 126 are larger than 
> 2.5 carats. The distribution of the remainder is shown below:

> Tenemos datos de 53940 diamantes. solo 126 son mas grandes que
> 2.5 quilates. La distribucion de lo restante se muestra abajo:

When inserting numbers into text, `format()` is your friend. It allows you to set the number of `digits` so you don't print to a ridiculous degree of accuracy, and a `big.mark` to make numbers easier to read. I'll often combine these into a helper function:
Cuando insertas números en el texto, `format()` es tu amigo. Esto permite que se seten el número de `digitos` para que no imprimas con un grado rídiculo de precision, y una `big.mark` para hacer que los números sean mas fáciles de leer. Siempre combino estos en una funcion de ayuda:



```r
comma <- function(x) format(x, digits = 2, big.mark = ",")
comma(3452345)
#> [1] "3,452,345"
comma(.12358124331)
#> [1] "0.12"
```

### Exercises
### Ejercicios

1.  Add a section that explores how diamond sizes vary by cut, colour,
    and clarity. Assume you're writing a report for someone who doesn't know
    R, and instead of setting `echo = FALSE` on each chunk, set a global 
    option.

1.  Incluye una seccion que explore como los tamaños de diamantes varian por corte,       color  y claridad. Asume que escribes un reporte para alguien que no conoce R, y      en lugar de setear `echo = FALSE` en cada bloque, setear una opción global.    

1.  Download `diamond-sizes.Rmd` from
    <https://github.com/hadley/r4ds/tree/master/rmarkdown>. Add a section
    that describes the largest 20 diamonds, including a table that displays
    their most important attributes.
    
1.  Descarga `diamond-sizes.Rmd` de                                                       <https://github.com/hadley/r4ds/tree/master/rmarkdown>. Agrega una sección que        describa los 20 diamantes mas grandes, incluyendo una tabla que muestre sus           atributos  más importantes.

1.  Modify `diamonds-sizes.Rmd` to use `comma()` to produce nicely
    formatted output. Also include the percentage of diamonds that are
    larger than 2.5 carats.
    
1.  Modifica `diamonds-sizes.Rmd` para usar `comma()` para producir un formato de         *output* ordenado. Tambien incluye el porcentaje de diamantes que son mayores a        2.5 quilates. 

1.  Set up a network of chunks where `d` depends on `c` and `b`, and
    both `b` and `c` depend on `a`. Have each chunk print `lubridate::now()`,
    set `cache = TRUE`, then verify your understanding of caching.

1.  Setea una red de bloques donde `d` depende de `c` y `b`, y
    tanto `b` y `c` dependen de `a`. Haz que cada bloque imprima `lubridate::now()`,      set `cache = TRUE`, y verifica entonces tu comprension del almacenamiento en          *cache*.

## Troubleshooting
## Solucionando problemas

Troubleshooting R Markdown documents can be challenging because you are no longer in an interactive R environment, and you will need to learn some new tricks. The first thing you should always try is to recreate the problem in an interactive session. Restart R, then "Run all chunks" (either from Code menu, under Run region), or with the keyboard shortcut Ctrl + Alt + R. If you're lucky, that will recreate the problem, and you can figure out what's going on interactively.

Los documentos de solución de problemas en R Markdown pueden ser un desafío porque no te encuentras en un ambiente de R interactivo, y necesitarás saber algunos trucos nuevos. La primer cosa que debes intentar es recrear el problema en una sesión interactiva. Reinicia R, después "Ejecuta todos los bloques" (ya sea en el menú de código , bajo la zona de Ejecutar ), o con el atajo del teclado Ctrl + Alt + R. Si tienes suerte, eso recreará el problema, y podrás descubrir lo que esta ocurriendo interactivamente.

If that doesn't help, there must be something different between your interactive environment and the R markdown environment. You're going to need to systematically explore the options. The most common difference is the working directory: the working directory of an R Markdown is the directory in which it lives. Check the working directory is what you expect by including `getwd()` in a chunk.

Si eso no ayuda, debe haber algo diferente entre tu ambiente interactivo y el ambiente de R Markdown. Tendrás que explorar sistemáticamente las opciones. La diferencia más común es el directorio de trabajo: el directorio de trabajo de R Markdown es el directorio en el que se encuentra. Revisa que el directorio de trabajo es el que esperas incluyendo `getwd()` en un bloque.

Next, brainstorm all the things that might cause the bug. You'll need to systematically check that they're the same in your R session and your R markdown session. The easiest way to do that is to set `error = TRUE` on the chunk causing the problem, then use `print()` and `str()` to check that settings are as you expect.

A continuación, piensa todas las cosas que pueden causar el error.  Necesitarás revisar sistemáticamente que   tu sesión de R y tu sesión de R Markdown son lo mismo. La manera mas fácil de hacer esto es setear `error = TRUE` en el bloque que causa problemas, usa entonces `print()` y `str()` para revisar que la configuración es la esperada.

## YAML header
## Encabezado YAML

You can control many other "whole document" settings by tweaking the parameters of the YAML header.  You might wonder what YAML stands for: it's "yet another markup language", which is designed for representing hierarchical data in a way that's easy for humans to read and write. R Markdown uses it to control many details of the output. Here we'll discuss two: document parameters and bibliographies.

Puedes controlar otras configuraciones de "documento completo" retocando los parametros del encabezado YAML. Estarás preguntandote que significa YAML:  en inglés *"yet another markup language"*  signifca algo como *"otro lenguaje markup"*, el cual esta diseñado  para representar datos jerárquicos de modo  tal que es fácil de  escribir y leer para humanos. R Markdown utiliza esto para controlar muchos detalles del *output.* Aqui discutiremos dos: parametros del documento y bibliografías. 

### Parameters

R Markdown documents can include one or more parameters whose values can be set when you render the report. Parameters are useful when you want to re-render the same report with distinct values for various key inputs. For example, you might be producing sales reports per branch, exam results by student, or demographic summaries by country. To declare one or more parameters, use the `params` field. 

Los documentos pueden incluir uno o mas parámetros cuyos valores pueden ser seteado cuando haces render al reporte. Los parámetros son útiles cuandos quieres re-renderizar el mismo reporte con valores distintos con varios inputs clave. Por ejemplo, podrias querer producir reportes de venta por ramas, resultados de examen por alumno, resumenes demograficos por pais. Para declarar uno o mas parametros, utiliza el campo `params`.

This example uses a `my_class` parameter to determine which class of cars to display:

Este ejemplo utiliza el parametro `my_class` para determinar que clase de auto mostrar:

````
---
output: html_document
params:
  my_class: "suv"
---

```{r setup, include = FALSE}
library(ggplot2)
library(dplyr)

class <- mpg %>% filter(class == params$my_class)
```

# Fuel economy for `r params$my_class`s

```{r, message = FALSE}
ggplot(class, aes(displ, hwy)) +
  geom_point() +
  geom_smooth(se = FALSE)
```
````



As you can see, parameters are available within the code chunks as a read-only list named `params`.

Como puedes ver, los parámetros estan disponibles dentro de los bloques de código como una lista de solo lectura llamada `params`.

You can write atomic vectors directly into the YAML header. You can also run arbitrary R expressions by prefacing the parameter value with `!r`. This is a good way to specify date/time parameters.

Puedes escribir vectores átomicos directamente en el encabezado YAML. Puedes tambien ejecutar arbitrariamente expresiones de R introduciendo previamente el valor del parámetro con `!r`. Esta es una buena manera de especificar parametros de fecha/hora.

```yaml
params:
  start: !r lubridate::ymd("2015-01-01")
  snapshot: !r lubridate::ymd_hms("2015-01-01 12:30:00")
```

In RStudio, you can click the "Knit with Parameters" option in the Knit dropdown menu to set parameters, render, and preview the report in a single user friendly step. You can customise the dialog by setting other options in the header. See <http://rmarkdown.rstudio.com/developer_parameterized_reports.html#parameter_user_interfaces> for more details.

En RStudio, puedes hacer clic en la opción "Knit with Parameters en el menú desplegable *Knit* para setear parámetros,renderizar y previsualizar en un un simple paso amigable para el usuario. Puedes personalizar el diálogo seteando otras opciones en el encabezado. Ver para mas detalles <http://rmarkdown.rstudio.com/developer_parameterized_reports.html#parameter_user_interfaces>. 

Alternatively, if you need to produce many such paramterised reports, you can call `rmarkdown::render()` with a list of `params`:
De manera alternativa, si necesitas producir varios reportes parametrizados puedes incluir `rmarkdown::render()` con una lista de `params`:


```r
rmarkdown::render("fuel-economy.Rmd", params = list(my_class = "suv"))
```

This is particularly powerful in conjunction with `purrr:pwalk()`. The following example creates a report for each value of `class` found in `mpg`. First we create a data frame that has one row for each class, giving the `filename` of the report and the `params`:

Esto es particularmente poderoso en conjuncion con `purrr:pwalk()`. El siguiente ejemplo crea un reporte para cada valor de `class` que se encuentra `mpg`. Primero creamos un data frame que tiene una fila para cada clase, dando el `filename` del reporte y los  `params`:


```r
reports <- tibble(
  class = unique(mpg$class),
  filename = stringr::str_c("fuel-economy-", class, ".html"),
  params = purrr::map(class, ~ list(my_class = .))
)
reports
#> # A tibble: 7 x 3
#>   class   filename                  params    
#>   <chr>   <chr>                     <list>    
#> 1 compact fuel-economy-compact.html <list [1]>
#> 2 midsize fuel-economy-midsize.html <list [1]>
#> 3 suv     fuel-economy-suv.html     <list [1]>
#> 4 2seater fuel-economy-2seater.html <list [1]>
#> 5 minivan fuel-economy-minivan.html <list [1]>
#> 6 pickup  fuel-economy-pickup.html  <list [1]>
#> # … with 1 more row
```


Then we match the column names to the argument names of `render()`, and use purrr's **parallel** walk to call `render()` once for each row:

Entonces unimos los nombres de las columnas con los nombres de los argumentos de `render()`, y utiliza **parallel** del paquete purrr para  `render()` una vez para cada fila:


```r
reports %>% 
  select(output_file = filename, params) %>% 
  purrr::pwalk(rmarkdown::render, input = "fuel-economy.Rmd")
```

### Bibliographies and Citations
### Bibliografías y citas
Pandoc can automatically generate citations and a bibliography in a number of styles. To use this feature, specify a bibliography file using the `bibliography` field in your file's header. The field should contain a path from the directory that contains your .Rmd file to the file that contains the bibliography file:

Pandoc puede generar automaticamente citas y bibliografia en varios estilos. Para usar esta caracteristica, especifica un archivo de bibliografia usando el campo `bibliography` en el encabezado de tu archivo. El campo debe incluir una ruta del directorio que contiene tu archivo .Rmd al archivo que contiene el archivo de la bibliografía:


```yaml
bibliography: rmarkdown.bib
```

You can use many common bibliography formats including BibLaTeX, BibTeX, endnote, medline.
Puedes usar muchos formatos comunes de biliografía incluyendo BibLaTeX, BibTeX, endnote, medline.

To create a citation within your .Rmd file, use a key composed of ‘@’ + the citation identifier from the bibliography file. Then place the citation in square brackets. Here are some examples:
Para crear una cita dentro de tu archivo .Rmd, usa una clave compuesta de ‘@’ + el identificador de la cita del archivo de la bibliografia. Despues ubica esta cita entre corchetes. Aqui hay algunos ejemplos:

```markdown
Separate multiple citations with a `;`: Blah blah [@smith04; @doe99].

You can add arbitrary comments inside the square brackets: 
Blah blah [see @doe99, pp. 33-35; also @smith04, ch. 1].

Remove the square brackets to create an in-text citation: @smith04 
says blah, or @smith04 [p. 33] says blah.

Add a `-` before the citation to suppress the author's name: 
Smith says blah [-@smith04].
```

```markdown
 multiple citas se separan con un `;`: Bla bla[@smith04; @doe99].

Puedes incluir comentarios arbritarios dentro de los corchetes:
Bla bla [ver @doe99, pp. 33-35; tambiée @smith04, ch. 1].

Remover los corchetes para crear una cita dentro del texto  @smith04 
dice bla, o @smith04 [p. 33] says bla.

Agrega un signo `-` antes de la cita para eliminar el nombre del autor:

Smith dice bla [-@smith04].
```

When R Markdown renders your file, it will build and append a bibliography to the end of your document. The bibliography will contain each of the cited references from your bibliography file, but it will not contain a section heading. As a result it is common practice to end your file with a section header for the bibliography, such as `# References` or `# Bibliography`.

Cuando R Markdown hace *render* de tu archivo, construirá y agregará una bibliografía al final del documento. La bibliografia contendrá cada una de las referencias citadas de tu archivo de bibliografia, pero no contendrá un encabezado de sección. Como resultado, es una práctica común finalizar el archivo con un encabezado de sección para la bibliografía, tales como `# Referencias` or `# Bibliografia`.

You can change the style of your citations and bibliography by referencing a CSL (citation style language) file in the `csl` field:

Puedes cambiar el estilo de tus citas y bibliografia referenciando un archivo CSL (del ingles,"citation style language", lengaje  de estilo de citas ) en el campo `csl`:

```yaml
bibliography: rmarkdown.bib
csl: apa.csl
```

As with the bibliography field, your csl file should contain a path to the file. Here I assume that the csl file is in the same directory as the .Rmd file. A good place to find CSL style files for common bibliography styles is  <http://github.com/citation-style-language/styles>.

Tal  y como en el campo de bilbiografia, tu archivo csl deberia contener una ruta al archivo. Aqui asumo que el archivo csl esta en el mismo directorio que el archivo .Rmd. Un buen lugar para encontrar archivos de estilos para estilos de bilbiografia comunes es
<http://github.com/citation-style-language/styles>.

## Learning more
## Aprendiendo más

R Markdown is still relatively young, and is still growing rapidly. The best place to stay on top of innovations is the official R Markdown website: <http://rmarkdown.rstudio.com>.

R Markdown es todavía relativamente reciente, y todavia esta creciendo rápidamente. El mejor lugar para estar al tanto de las innovaciones es el sitio oficial de R Markdown: <http://rmarkdown.rstudio.com>.

There are two important topics that we haven't covered here: collaboration, and the details of accurately communicating your ideas to other humans. Collaboration is a vital part of modern data science, and you can make your life much easier by using version control tools, like Git and GitHub. We recommend two free resources that will teach you about Git:

Hay dos tópicos importantes que no hemos mencionado aquí: colaboraciones y los detalles de comunicar de manera precisa tus ideas a otros humanos.  La colaboración es una parte vital de la ciencia de datos moderna, podria hacer tu vida mucho mas facil usando herramientas de control de versión, tales como Git y GitHub. Recomendamos dos recursos gratuitos que te enseñaran Git:

1.  "Happy Git with R": a user friendly introduction to Git and GitHub from 
    R users, by Jenny Bryan. The book is freely available online:
    <http://happygitwithr.com>
    
1.  "Happy Git with R": una introduccion amigable al usario a Git and GitHub a usarios     de R, de Jenny Bryan. El libro esta disponible de manera libre online en:
    <http://happygitwithr.com>  
    
1.  The "Git and GitHub" chapter of _R Packages_, by Hadley. You can also 
    read it for free online: <http://r-pkgs.had.co.nz/git.html>.

1.  El capitulo "Git and GitHub"  de _R Packages_, de Hadley Wickham. Puedes también     leerlo online: <http://r-pkgs.had.co.nz/git.html>.      
    
    

I have also not touched on what you should actually write in order to clearly communicate the results of your analysis. To improve your writing, I highly recommend reading either [_Style: Lessons in Clarity and Grace_](https://amzn.com/0134080416) by Joseph M. Williams & Joseph Bizup, or [_The Sense of Structure: Writing from the Reader's Perspective_](https://amzn.com/0205296327) by George Gopen. Both books will help you understand the structure of sentences and paragraphs, and give you the tools to make your writing more clear. (These books are rather expensive if purchased new, but they're used by many English classes so there are plenty of cheap second-hand copies). George Gopen also has a number of short articles on writing at <https://www.georgegopen.com/the-litigation-articles.html>. They are aimed at lawyers, but almost everything applies to data scientists too. 
  
Tampoco he mencionado lo que deberías en realidad escribir  para poder comunicar claramente los resultados de tu análisis. Para mejorar tu escritura, recomiendo leer cualquiera de estos libros: [_Style: Lessons in Clarity and Grace_](https://amzn.com/0134080416) de Joseph M. Williams & Joseph Bizup, or [_The Sense of Structure: Writing from the Reader's Perspective_](https://amzn.com/0205296327) de  George Gopen. Ambos libros te ayudarán a entender la estructura de oraciones y párrafos, y te dar<n las herramienta para hacer mas clara tu escritura ( Estos libros son bastante caros si son comprados nuevos, pero dado que son usados en muchas clases de inglés hay muchas copias baratas de segunda mano). George Gopen tambien a escrito varios articulos cortos sobre escritura en <https://www.georgegopen.com/the-litigation-articles.html>. Están dirigidos a abogados, pero casi todo también se aplica a los científicos de datos.

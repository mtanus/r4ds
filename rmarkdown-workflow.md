
# R Markdown workflow
# Flujo de trabajo en R Markdown

Earlier, we discussed a basic workflow for capturing your R code where you work interactively in the _console_, then capture what works in the _script editor_. R Markdown brings together the console and the script editor, blurring the lines between interactive exploration and long-term code capture. You can rapidly iterate within a chunk, editing and re-executing with Cmd/Ctrl + Shift + Enter. When you're happy, you move on and start a new chunk.

Antes, discutimos un flujo de trabajo básico para capturar tu código de R cuando trabjas interactivamente en la _consola_, la cual captura lo que trabaja en el _editor de script_. R Markdown une la _consola_ y el _editor de script_, desdibujando los limites entre exploración interactiva y captura de código a largo plazo. Puedes iterar rápidamente dentro un bloque, editando y re-ejecutando con Cmd/Ctrl + Shift + Enter. Cuando estés conforme, sigue adelante y inicia un nuevo bloque.

R Markdown is also important because it so tightly integrates prose and code. This makes it a great __analysis notebook__ because it lets you develop code and record your thoughts. An analysis notebook shares many of the same goals as a classic lab notebook in the physical sciences. It:

R Markdown es también importante ya que integra firmemente prosa y código. Esto hace que sea un gran __notebook de analísis__, porque permite desarrollar código y registrar tus pensamientos. Un *notebook* de analísis comparte muchos de los mismos objetivos que tiene un *notebook* de laboratorio clasico en las ciencias físicas. Puede:

*   Records what you did and why you did it. Regardless of how great your
    memory is, if you don't record what you do, there will come a time when
    you have forgotten important details. Write them down so you don't forget!

*   Registrar qué se hizo y por qué se hizo. Independientemente de cuan buena sea tu memoria, si no registras lo que haces, llegará un momento cuando hayas olvidado detalles importantes.

*   Supports rigorous thinking. You are more likely to come up with a strong
    analysis if you record your thoughts as you go, and continue to reflect
    on them. This also saves you time when you eventually write up your
    analysis to share with others.

*   Apoyar el pensamiento riguroso. Es mas probable que logres un análisis fuerte si registras tus pensamientos mientras avanzas, y continuas reflexionando sobre ellos. Esto también te ahorra tiempo cuando eventualmente escribes tu analisis para compartir con otros.

*   Helps others understand your work. It is rare to do data analysis by
    yourself, and you'll often be working as part of a team. A lab notebook
    helps you share not only what you've done, but why you did it with your
    colleagues or lab mates.
    
*   Ayudar a que otros comprendan tu trabajo. Es raro hacer un analisis de datos por sí sola, dado que muy seguido trabajarás como parte de un equipo. Un *notebook* de laboratorio ayuda a que compartas no solo lo que has hecho, sino también por qué lo hiciste con tus colegas o compañeros de laboratorio. 

Much of the good advice about using lab notebooks effectively can also be translated to analysis notebooks. I've drawn on my own experiences and Colin Purrington's advice on lab notebooks (<http://colinpurrington.com/tips/lab-notebooks>) to come up with the following tips:

Muchos de estos buenos consejos sobre el uso más efectivo de *notebooks* de laboratorio pueden también ser trasladados para utilizar un *notebooks* de analísis. He extraído de mis propias experiencias y los consejos de Colin Purrington sobre *notebooks* de laboratorio (<http://colinpurrington.com/tips/lab-notebooks>) para sugerir los siguientes consejos:


*   Ensure each notebook has a descriptive title, an evocative filename, and a
    first paragraph that briefly describes the aims of the analysis.

*   Asegúrate de que cada *notebook* tenga un titulo descriptivo, un nombre de archivo evocativo, y un primer parrafo que describa brevemente los objetivos del analisis.

*   Use the YAML header date field to record the date you started working on the
    notebook:
*   Utiliza el campo para fecha del encabezado YAML para registrar la fecha en la que comienzas a trabajar en el *notebook*: 

    ```yaml
    title: My title
    date: 2016-08-23
    ```

    Use ISO8601 YYYY-MM-DD format so that's there no ambiguity. Use it
    even if you don't normally write dates that way!
    
    Utiliza el formato ISO8601 AAAA-MM-DD para que no haya ambiguidad. ¡Utilízalo incluso si no escribes normalmente fechas de ese modo!

*   If you spend a lot of time on an analysis idea and it turns out to be a
    dead end, don't delete it! Write up a brief note about why it failed and
    leave it in the notebook. That will help you avoid going down the same
    dead end when you come back to the analysis in the future.

*   Si pasas mucho timepo en una idea de analísis y resulta ser un callejón sin salida, ¡no lo elimines! Escribe una nota breve sobre por qué falló y déjala en el *notebook* .Esto te ayudará a evitar ir por el mismo callejon sin salida cuando regreses a ese analisis en el futuro. 

*   Generally, you're better off doing data entry outside of R. But if you 
    do need to record a small snippet of data, clearly lay it out using
    `tibble::tribble()`.
    
*   Generalmente, es mejor que hagas la entrada de datos fuera de R. Pero si necesitas registrar un pequeño bloque de datos, establécelo de modo claro usando `tibble::tribble()`. 

*   If you discover an error in a data file, never modify it directly, but
    instead write code to correct the value. Explain why you made the fix.

*   Si descubres un error en un archivo de datos, nunca lo modifiques directamente, 
    en su lugar escribe código para corregir el valor. Explica por qué lo corregiste. 

*   Before you finish for the day, make sure you can knit the notebook
    (if you're using caching, make sure to clear the caches). That will
    let you fix any problems while the code is still fresh in your mind.
    
*   Antes de concluir por el día, asgurate de que puedes *knit* el *notebook* (si utilizas cacheo, asgurate de limpiar los caches). Esto te permitirá corregir cualquier problema mientras el código esta todavia fresco en tu mente. 

*   If you want your code to be reproducible in the long-run (i.e. so you can
    come back to run it next month or next year), you'll need to track the
    versions of the packages that your code uses. A rigorous approach is to use
    __packrat__, <http://rstudio.github.io/packrat/>, which stores packages 
    in your project directory, or __checkpoint__,
    <https://github.com/RevolutionAnalytics/checkpoint>, which will reinstall
    packages available on a specified date. A quick and dirty hack is to include
    a chunk that runs `sessionInfo()` --- that won't let you easily recreate 
    your packages as they are today, but at least you'll know what they were.
    
*   Si quieres que tu código sea reproducible a largo plazo (esto quiere decir que puedas regresar a ejecutarlo el mes próximo o el año próximo), necesitarás registrar las versiones de los paquetes que tu código usa. Un enfoque riguroso es usar __packrat__, <http://rstudio.github.io/packrat/>, el cual almacena paquetes en tu directorio de proyecto, or __checkpoint__, <https://github.com/RevolutionAnalytics/checkpoint>, el cual reinstala paquetes disponibles en una fecha determinada . Un truco rápido y sucio es incluir un bloque que ejecute `sessionInfo()` --- , esto no te permitirá recrear fácilmente tus paquetes tal y como estan hoy, pero por lo menos sabrás cuales eran. 

*   You are going to create many, many, many analysis notebooks over the course
    of your career. How are you going to organise them so you can find them
    again in the future? I recommend storing them in individual projects,
    and coming up with a good naming scheme.
    
*   Crearás muchos, muchos, muchos *notebooks* de analisis a lo largo de tu carrera. ¿Cómo puedes organizarlos de modo tal que puedas encontrarlos otra vez en el futuro? Recomiendo almacenarlos en proyectos individuales, y tener un buen esquema de nombrado. 

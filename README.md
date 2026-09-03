# HBGT_2026

<script src="https://jsdelivr.net"></script>
<!-- Initialize quizdown automatically -->
<script>
    window.onload = function() {
        quizdown.init();
    };
</script>

<div class="quizdown">

# Cuestionario: Desafío de Linux y HPC en Bioinformática (Formato Google Forms)

Este cuestionario contiene 15 preguntas de opción múltiple organizadas en 5 bloques conceptuales (3 preguntas por bloque), listas para ser copiadas e importadas a **Google Forms** o utilizadas en dinámicas tipo **Kahoot**. Se incluyen explicaciones pedagógicas detalladas basadas en los principios de **CABANAnet** y el material oficial del curso.

---

## BLOQUE 1: ARQUITECTURA Y TERMINOLOGÍA (HPC vs. Local)

### Pregunta 1
Estás corriendo un alineamiento que requiere cargar en memoria temporal un índice de genoma de 40 GB. ¿Qué componente de hardware de tu servidor se encargará de almacenar estos datos temporalmente mientras el programa se ejecuta?
* [ ] A) La Unidad de Procesamiento Central (CPU)
* [x] B) La Memoria de Acceso Aleatorio (RAM)
* [ ] C) El Núcleo (Core)
* [ ] D) El Disco de Estado Sólido (SSD) en modo de almacenamiento secundario

**Respuesta correcta:** B  
**Comentarios de retroalimentación (Feedback):**  
La Memoria de Acceso Aleatorio (RAM) es el componente del hardware que almacena de forma temporal los datos que están siendo procesados activamente, mientras que la CPU o los Cores se encargan de ejecutar las instrucciones matemáticas y lógicas del programa.

---

### Pregunta 2
En la infraestructura de Cómputo de Alto Rendimiento (HPC) del INECOL, ¿qué es exactamente un "Nodo de procesamiento"?
* [ ] A) Un cable de red de fibra óptica de alta velocidad que une los clústeres.
* [ ] B) Un usuario activo que está conectado simultáneamente al sistema.
* [x] C) Un servidor individual que forma parte del clúster y posee sus propios recursos de CPU, RAM y almacenamiento.
* [ ] D) Un programa que organiza jerárquicamente las carpetas de los alumnos.

**Respuesta correcta:** C  
**Comentarios de retroalimentación (Feedback):**  
Un nodo de procesamiento es un servidor físico e independiente que forma parte de un equipo HPC y que cuenta con recursos de hardware dedicados (como CPU, RAM y almacenamiento) para realizar tareas de procesamiento pesado.

---

### Pregunta 3
Varios estudiantes del curso envían análisis pesados al servidor de HPC al mismo tiempo. ¿Qué software se encarga de gestionar la cola de espera y de asignar los nodos de procesamiento correspondientes a cada usuario según los recursos solicitados?
* [ ] A) El Kernel de Linux
* [x] B) El Administrador de trabajos (Scheduler)
* [ ] C) La interfaz de línea de comandos (Shell)
* [ ] D) Un proceso serializado de multithreading

**Respuesta correcta:** B  
**Comentarios de retroalimentación (Feedback):**  
El Administrador de trabajos o Scheduler (como Slurm) es el software que gestiona la cola de trabajos de los distintos usuarios del HPC y los asigna a determinados nodos de procesamiento según los requerimientos declarados (Cores, RAM, tiempo).

---

## BLOQUE 2: NAVEGACIÓN DE ARCHIVOS Y DIRECTORIOS

### Pregunta 4
Estás trabajando en la terminal del HPC del INECOL y te das cuenta de que no sabes con certeza en qué carpeta del sistema de archivos te encuentras parado en ese momento. ¿Cuál es el comando que debes teclear para averiguarlo?
* [ ] A) `ls -l`
* [ ] B) `whoami`
* [x] C) `pwd`
* [ ] D) `cd ~`

**Respuesta correcta:** C  
**Comentarios de retroalimentación (Feedback):**  
El comando `pwd` significa "print working directory" (imprimir directorio de trabajo) y nos permite visualizar la ruta absoluta de la carpeta en la que estamos interactuando en ese preciso instante.

---

### Pregunta 5 (POP QUIZ de Nelle Nemo)
Te encuentras posicionado dentro del directorio de datos crudos de Nelle: `/Users/nelle/data`. ¿Cuál de los siguientes comandos **NO** te llevará de regreso a su directorio personal de usuario (`/Users/nelle`)?
* [ ] A) `cd ..`
* [ ] B) `cd ~`
* [ ] C) `cd`
* [x] D) `cd /`

**Respuesta correcta:** D  
**Comentarios de retroalimentación (Feedback):**  
`cd ..` sube un nivel en la jerarquía (de `data` a `nelle`). `cd` (sin argumentos) y `cd ~` te devuelven directamente al directorio "home" o personal de usuario. En cambio, `cd /` te lleva al directorio raíz ("root") del sistema de archivos, no al home de Nelle.

---

### Pregunta 6 (POP QUIZ de Rutas)
A partir del sistema de archivos de la terminal, si te encuentras parado en la ruta `/Users/thing`, ¿qué resultado te mostrará el comando `ls -F ../backup`?
* [ ] A) `../backup: No such file or directory`
* [ ] B) Un mensaje de error porque no se pueden usar rutas relativas con `..`
* [x] C) `original/ pnas_final/ pnas_sub/` (los nombres de las carpetas con una barra diagonal `/` al final)
* [ ] D) `original.txt pnas_final.txt pnas_sub.txt`

**Respuesta correcta:** C  
**Comentarios de retroalimentación (Feedback):**  
El comando `ls -F ../backup` utiliza una ruta relativa que sube de `/Users/thing` a `/Users` y entra al directorio `/Users/backup`. La opción `-F` clasifica visualmente los elementos agregando una barra diagonal `/` al final de los nombres de los directorios para distinguirlos de archivos regulares.

---

## BLOQUE 3: CREACIÓN, ORGANIZACIÓN Y BORRADO SEGURO

### Pregunta 7
Deseas crear la estructura de carpetas jerárquica `/resultados/blast` para organizar tus alineamientos. ¿Cuál es el comando correcto para generar ambas carpetas de forma segura en un solo paso, incluso si la carpeta `/resultados` aún no existe?
* [ ] A) `mkdir /resultados/blast`
* [x] B) `mkdir -p /resultados/blast`
* [ ] C) `touch /resultados/blast`
* [ ] D) `mkdir -all /resultados/blast`

**Respuesta correcta:** B  
**Comentarios de retroalimentación (Feedback):**  
La opción `-p` (parents) del comando `mkdir` permite crear subdirectorios de forma jerárquica y recursiva en un solo paso, creando los directorios padres necesarios si estos no existen previamente en el sistema de archivos.

---

### Pregunta 8
¿Cuál es la diferencia operativa fundamental entre los comandos `mv` y `cp` al organizar archivos de secuenciación?
* [ ] A) `mv` se utiliza para ver archivos pesados y `cp` para editarlos.
* [x] B) `mv` mueve o renombra el archivo original sin duplicarlo; `cp` crea una copia exacta en el destino, manteniendo el original intacto.
* [ ] C) `cp` solo puede utilizarse con archivos de texto y `mv` solo funciona con carpetas.
* [ ] D) `mv` borra temporalmente los archivos enviándolos a la papelera y `cp` los restaura.

**Respuesta correcta:** B  
**Comentarios de retroalimentación (Feedback):**  
`mv` (move) traslada archivos de una ubicación a otra o cambia su nombre (origen de datos único). `cp` (copy) duplica la información, consumiendo el doble de almacenamiento en disco al generar una entidad independiente en el destino.

---

### Pregunta 9
Estás haciendo limpieza de archivos de secuenciación FASTQ corruptos en el HPC. Como la eliminación en Linux es permanente e irreversible, ¿cuál de las siguientes opciones deberías usar para confirmar interactivamente cada archivo antes de que sea eliminado?
* [ ] A) `rm -rf *`
* [ ] B) `rm -f *.fastq`
* [x] C) `rm -i *.fastq`
* [ ] D) `delete --confirm *.fastq`

**Respuesta correcta:** C  
**Comentarios de retroalimentación (Feedback):**  
Dado que la Shell de UNIX no cuenta con una papelera de reciclaje y la eliminación de datos es definitiva, la opción interactiva `-i` de `rm` (remove) obliga al sistema a pedir una confirmación manual (sí/no) al usuario antes de proceder con el borrado.

---

## BLOQUE 4: REDIRECCIÓN Y TUBERÍAS (PIPES)

### Pregunta 10
Ejecutas un programa para identificar adaptadores de secuenciación y deseas guardar el reporte de salida directamente en un archivo de texto nuevo llamado `adaptadores.txt` en lugar de imprimir las miles de líneas en la pantalla de la terminal. ¿Qué operador debes utilizar?
* [ ] A) El pipe o tubería (`|`)
* [x] B) El operador de redirección de salida (`>`)
* [ ] C) El asterisco comodín (`*`)
* [ ] D) El operador de concatenación (`&&`)

**Respuesta correcta:** B  
**Comentarios de retroalimentación (Feedback):**  
El símbolo de mayor que (`>`) es el operador que le indica a la shell que redirija la salida de un comando hacia un archivo nuevo en disco, en lugar de desplegarlo en la interfaz gráfica de la terminal.

---

### Pregunta 11
En tu flujo de procesamiento bioinformático, deseas combinar comandos. ¿Cuál es el papel principal del operador pipe o tubería (`|`)?
* [ ] A) Duplicar la potencia del procesador para acelerar la ejecución paralela.
* [x] B) Conectar directamente la salida (output) del primer comando con la entrada (input) del segundo comando, evitando crear archivos temporales.
* [ ] C) Enviar un comando a ejecutarse en segundo plano (background) en el HPC.
* [ ] D) Convertir formatos de archivos FASTA a FASTQ de forma automática.

**Respuesta correcta:** B  
**Comentarios de retroalimentación (Feedback):**  
El pipe o tubería (`|`) actúa como un conducto de datos en tiempo real, conectando la salida estándar del comando de la izquierda a la entrada estándar del comando de la derecha, permitiendo encadenar flujos analíticos ágiles.

---

### Pregunta 12
Tienes un archivo gigante llamado `genes.txt` y quieres ordenarlo alfabéticamente para visualizar en la pantalla únicamente los primeros 5 genes resultantes. ¿Cuál de las siguientes combinaciones de comandos es la correcta?
* [ ] A) `head -n 5 genes.txt > sort`
* [x] B) `sort genes.txt | head -n 5`
* [ ] C) `genes.txt | sort | head -5`
* [ ] D) `grep -n 5 genes.txt | sort`

**Respuesta correcta:** B  
**Comentarios de retroalimentación (Feedback):**  
`sort genes.txt` procesa las líneas ordenándolas alfabéticamente; el operador `|` pasa el resultado directamente al comando `head -n 5`, el cual restringe la visualización final a las primeras 5 líneas de la salida ordenada.

---

## BLOQUE 5: BÚSQUEDAS Y AUTOMATIZACIÓN

### Pregunta 13
Necesitas buscar rápidamente la secuencia exacta de un promotor bacteriano ("ATGCA") dentro de un archivo de nucleótidos gigante. ¿Qué comando es el adecuado para buscar este patrón de texto específico línea por línea?
* [ ] A) `find`
* [ ] B) `cat`
* [x] C) `grep`
* [ ] D) `locate`

**Respuesta correcta:** C  
**Comentarios de retroalimentación (Feedback):**  
El comando `grep` (global/regular expression/print) busca patrones de texto específicos línea por línea dentro de uno o varios archivos de texto plano. Por el contrario, el comando `find` sirve para localizar archivos físicos y directorios en el disco, no contenido dentro de ellos.

---

### Pregunta 14
El pipeline de Nelle Nemo requiere procesar 1520 archivos individuales usando el script `goostats.sh`. Para evitar teclear el comando de forma manual 1520 veces, ¿qué estructura de programación debes emplear en la shell?
* [ ] A) Un condicional `if [ -f archivo ]`
* [x] B) Un bucle o ciclo `for` (loop)
* [ ] C) Un redireccionamiento secuencial con `>>`
* [ ] D) Un pipe masivo `| xargs`

**Respuesta correcta:** B  
**Comentarios de retroalimentación (Feedback):**  
Los loops o bucles `for` son estructuras lógicas indispensables en bioinformática que permiten automatizar tareas repetitivas sobre un conjunto de archivos o datos, permitiendo que la computadora procese los archivos de forma iterativa y autónoma.

---

### Pregunta 15
¿Qué es un "Script de Shell" (como un archivo `.sh`) y cuál es su principal ventaja dentro del flujo de trabajo de un bioinformático?
* [ ] A) Un programa binario compilado de alta velocidad inaccesible para edición.
* [x] B) Un archivo de texto plano que reúne una secuencia ordenada de comandos de terminal, garantizando la reproducibilidad y el intercambio de flujos de análisis completos.
* [ ] C) Una base de datos que almacena índices de genomas de manera estructurada.
* [ ] D) Una interfaz gráfica que reemplaza a la consola de comandos de Linux.

**Respuesta correcta:** B  
**Comentarios de retroalimentación (Feedback):**  
Un script de shell es un archivo que consolida un pipeline o flujo de comandos secuenciales. Esto permite ejecutar tareas bioinformáticas complejas con un solo comando, facilitando la reproducibilidad, la depuración y el intercambio transparente de metodologías científicas.

</div>

---
layout: default
title: "Día 03 · Control y procesamiento de lecturas"
---

<span class="eyebrow">Lunes · 21 septiembre</span>

### 🔬 Día 3: Tecnologías de Secuenciación NGS y Librerías

El análisis de genomas se sustenta en la generación de datos de alta fidelidad mediante tecnologías de Secuenciación de Siguiente Generación (NGS).

### Tipos de Librerías y Química de Secuenciación
*   **Librerías de Secuenciación:** Preparación del ADN o ARN fragmentado al cual se le ligan adaptadores moleculares específicos en sus extremos para permitir su anclaje y amplificación en las plataformas de secuenciación.
*   **Secuenciación por Síntesis:** Adición secuencial de nucleótidos fluorescentes que son detectados por una cámara de alta resolución al integrarse en la cadena complementaria en tiempo real.
*   **Datos Generados:** El resultado estándar son archivos en formato **FASTQ**, los cuales contienen tanto la secuencia de nucleótidos (letras A, C, T, G, N) como el valor de calidad de cada base llamado **Phred Score**.

---

# Práctica 01 — Ejercicios de Preprocesamiento de Secuencias

---

## Ejercicio 1 — Carpeta 1.SingleEnd

### Ejercicio01 - Bash Instructions

Primer ejercicio de la práctica 01

```bash
mkdir Ejercicio01
cd Ejercicio01
```

#### Carpeta 1.SingleEnd

Para descomprimir y comprimir archivos en formato .gz

(Utilizar la ayuda para mostrar opciones)

```bash
gunzip -h
```

**Descomprimir**

```bash
srun --mem 8G -n1 -p q1 gunzip IlluminaReads_NewStyle.fastq.gz
```

**Comprimir**

```bash
srun --mem 8G -n1 -p q1 gzip IlluminaReads_NewStyle.fastq
```

Para ver el contenido del archivo "IlluminaReads_NewStyle.fastq"
(presione la tecla q para salir del visualizador)

```bash
less Archivo.fastq
```

> **NOTA:** También es posible utilizar comandos como `head` o `tail` para mostrar en pantalla las 10 primeras/últimas líneas del archivo (utilizar la ayuda para ver otras opciones disponibles para estos comandos).

Es a menudo importante saber cuántas secuencias se encuentran contenidas en un archivo (ya sean fasta o fastq); en ambos casos es importante encontrar caracteres específicos que formen parte de los identificadores únicos de cada una de las secuencias, dichos caracteres idealmente deben estar repetidos en todas las secuencias contenidas en el archivo. Para nuestro ejemplo, es posible contar el número de secuencias contenidas en el archivo "IlluminaReads_NewStyle.fastq" utilizando la siguiente línea de comando:

```bash
grep -c "@NB501110" IlluminaReads_NewStyle.fastq
```

Para cambiar los valores de calidad del formato ASCII (acrónimo inglés de American Standard Code for Information Interchange) a valores numéricos de calidad en la escala de Phred:

- ASCII: [tabla de códigos](http://ascii.cl/es/)
- Phred: valor numérico conocido como la escala de valor de calidad, logarítmico, ligado a la probabilidad de error (Phred Score = 10, probabilidad de error de lectura en esa base 1/10; Score 20, probabilidad 1/100, etc.)

Primero habilitar el módulo que contiene los ejecutables de este ejercicio (fastx):

```bash
module load fastx-toolkit/0.0.14/gcc/8.3.1-6qup
```

[FASTX-Toolkit](http://hannonlab.cshl.edu/fastx_toolkit/) es una colección de herramientas de línea de comandos para el preprocesamiento de archivos FASTA/FASTQ.

Convertir y cambiar entre diferentes tipos de formatos, cambiar los identificadores de las secuencias, filtrar con base a la calidad, recortar adaptadores y regiones de mala calidad son solo algunas de las herramientas disponibles.

Utilizar la ayuda para mostrar opciones:

```bash
fastq_quality_converter -h
```

Ejecutar el siguiente trabajo en modo interactivo:

> `srun` es el comando para lanzar un job interactivo con SLURM; las opciones `--mem` y `-n` son utilizadas para asignar los recursos de memoria (16GB) y de procesamiento (1 CPU) respectivamente.

```bash
srun --mem 16000 -n 1 -p q2 fastq_quality_converter -n -Q33 -i IlluminaReads_NewStyle.fastq -o IlluminaReads_Phred.fastq
```

Ver el interior del archivo y anotar los cambios en el archivo de salida en relación con el original.

Para cambiar el nombre o identificador de las secuencias de la versión reciente a versiones anteriores, se empleará un procesador de datos (awk) para realizar algunos cambios sobre el archivo de entrada:

```bash
cat IlluminaReads_NewStyle.fastq | awk '{if (NR % 4 == 1) {split($1, arr, ":"); printf "%s_%s:%s:%s:%s:%s#0/%s (%s)\n", arr[1], arr[3], arr[4], arr[5], arr[6], arr[7], substr($2, 1, 1), $0} else if (NR % 4 == 3){print "+"} else {print $0} }' > IlluminaReads_OldStyle01.fastq
```

> **NOTA:** Tenga en cuenta que el encabezado original se agrega al final y entre paréntesis. Si no desea/necesita esto, simplemente elimine el espacio y el `(%s)` justo antes del `\n` en la línea de comando.

```bash
cat IlluminaReads_NewStyle.fastq | awk '{if (NR % 4 == 1) {split($1, arr, ":"); printf "%s_%s:%s:%s:%s:%s#0/%s\n", arr[1], arr[3], arr[4], arr[5], arr[6], arr[7], substr($2, 1, 1), $0} else if (NR % 4 == 3){print "+"} else {print $0} }' > IlluminaReads_OldStyle02.fastq
```

> **NOTA:** Con frecuencia, cuando se pretende analizar un conjunto de datos, una gran cantidad de herramientas/programas son necesarias; es importante tener en cuenta que en la mayoría de las ocasiones es posible realizar los análisis requeridos sin conocimientos amplios en lenguajes de programación. Repositorios como GitHub son una plataforma de desarrollo colaborativo de software para alojar proyectos, utilizando el sistema de control que permite ir siguiendo las diferentes versiones/modificaciones. Los códigos fuente se almacenan y por lo general son de acceso público.

Para generar los archivos fasta y qual a partir de un archivo fastq usaremos un script de Python `convert_fastaqual_fastq.py` disponible en Qiime. Para ello debemos cargar el ambiente de conda `qiime1-1.9.1`:

```bash
conda activate qiime1-1.9.1
```

Para mostrar el menú de ayuda:

```bash
python convert_fastaqual_fastq.py -h
```

A partir de un archivo fastq, generar los archivos fasta y qual:

```bash
srun --mem 16000 -n1 -p q2 convert_fastaqual_fastq.py -c fastq_to_fastaqual -f IlluminaReads_NewStyle.fastq
```

Como alternativa, se puede convertir un archivo fastq a fasta con EMBOSS:

```bash
module load emboss/6.6.0/gcc/9.3.0-4geh
srun --mem 8G -n1 -p q1 seqret -sequence IlluminaReads_NewStyle.fastq -outseq IlluminaReads_NewStyle.fasta
```

A partir de los archivos fasta y qual, generar un archivo fastq:

```bash
srun --mem 16000 -n1 convert_fastaqual_fastq.py -c fastaqual_to_fastq -f IlluminaReads_NewStyle.fna -q IlluminaReads_NewStyle.qual
```

Visualizar las diferencias entre los archivos generados.

Para analizar la calidad de las secuencias en el archivo fastq, utilice el programa FastQC. Como existen módulos cargados (`module list`) y para evitar interferencia entre programas, es recomendable, antes de cargar algún otro módulo, limpiar el ambiente de trabajo:

```bash
module purge
```

**Módulo q1:**

```bash
module load fastqc/0.11.7/gcc/9.3.0-o4ca
srun --mem 16000 -n1 -p q1 fastqc IlluminaReads_NewStyle.fastq
```

Debido a que a través de la línea de comandos no es posible visualizar archivos en ciertos formatos (p. ej. pdf, html, entre otros), importe a su máquina local el archivo en formato html generado como resultado del comando previo. Una vez transferido el archivo, acceda al mismo en su máquina local.

Para hacer la transferencia, utilice la siguiente línea de comando desde una terminal ubicada en el localhost:

```bash
rsync -av --progress --bwlimit=20000 -e 'ssh -p 49' $USUARIO@201.122.70.15:$PATH_AL_CURSO/Practica01/1.SingleEnd_Reads/*.html .
```

Analice todos los datos contenidos en el archivo .html utilizando algún navegador de Internet (Google Chrome, Firefox, etc.).

Para filtrar las secuencias con base a valores de calidad determinados, es posible utilizar alguna de las herramientas disponibles en el paquete FASTX-toolkit. Cargue el módulo correspondiente y ejecute el siguiente comando:

```bash
module load fastx-toolkit/0.0.14/gcc/8.3.1-gofi
srun --mem 16000 -n1 -p q2 fastq_quality_filter -Q33 -q 30 -p 100 -i IlluminaReads_NewStyle.fastq -o IlluminaReads_Filtered01.fastq
```

> **NOTA:** Puede utilizar la ayuda para ver otras opciones disponibles; analice el significado de las variables empleadas (`-q` y `-p`).

```bash
fastq_quality_filter -h
```

Otros filtros están disponibles dependiendo de las necesidades particulares de los datos con los que se trabaja. Ejecute la siguiente línea de comandos, analice el significado de las variables y compare/explique las salidas de ambas herramientas:

```bash
fastq_quality_trimmer -h
srun --mem 16000 -n1 -p q2 fastq_quality_trimmer -Q33 -t 25 -l 30 -i IlluminaReads_NewStyle.fastq -o IlluminaReads_Filtered02.fastq
```

Ejecute el programa FastQC para ambos archivos generados (IlluminaReads_Filtered01.fastq y IlluminaReads_Filtered02.fastq). Importe a su máquina local los archivos de salida (.html) y analícelos.

Finalmente, también es posible utilizar otro tipo de aproximaciones para hacer el filtrado de lecturas, como lo son las ventanas móviles. Para ello utilizaremos el programa Trimmomatic:

```bash
module load trimmomatic/0.38/gcc/8.3.1-jwk4
```

Ejecutar el comando:

```bash
srun --mem 8G -n2 -p q1 trimmomatic SE -threads 2 -phred33 IlluminaReads_NewStyle.fastq IlluminaReads_Filtered03.fastq LEADING:15 TRAILING:15 SLIDINGWINDOW:4:20 MINLEN:36
```

Se pueden realizar otros filtros modificando los parámetros de las ventanas móviles.

Al finalizar, comparar los resultados de ambas aproximaciones a través de los resultados de FastQC.

---

## Ejercicio 2 — Carpeta 2.Paired-End_Reads

Para filtrar reads pareados con base a valores de calidad determinados.

El programa a utilizar debe garantizar mantener siempre secuencias pareadas, eliminando aquellas que no cumplan con los valores asignados como umbral. En caso de que una de las secuencias sea eliminada (R1 o R2), el par correspondiente será eliminado para no retener secuencias huérfanas.

```bash
module load q1/ngstools/master
srun -n1 --mem 16000 -p q1 qualityControl.py -1 R1.fastq -2 R2.fastq -q 20 -p 90 -a 30 -o1 HQA_R1.fastq -o2 HQA_R2.fastq
```

Contar en los archivos de salida el total de secuencias y comparar vs. los archivos originales; analizar en el archivo de ayuda el significado de las variables `-q 20 -p 90 -a 30`. Discutir la importancia de manipular correctamente dichas variables.

Ejecute de nueva cuenta el trabajo anterior, pero ahora utilizando un script de bash (shell); vea el contenido del archivo "qualityControl.slurm", trabaje al interior del mismo y edítelo utilizando vim, y finalmente ejecútelo y compare la salida en razón de cómo afecta modificar las variables `-q`, `-p` y `-a`.

Ahora realizaremos un filtro a través de ventanas móviles con Trimmomatic:

```bash
module load trimmomatic/0.38/gcc/8.3.1-jwk4
```

Consultar la ayuda para estructurar el comando (utilizar los siguientes parámetros `LEADING:15 TRAILING:15 SLIDINGWINDOW:4:20 MINLEN:36`).

En ocasiones, y dependiendo del tipo de adaptadores empleados para construir las bibliotecas, una vez secuenciadas las mismas, dichos adaptadores deben ser identificados y eliminados. SeqPrep es un programa escrito para tales propósitos; además de remover los adaptadores, el programa también realiza un filtro de calidad en las lecturas y elimina reads huérfanos en caso de que alguna de las secuencias pareadas no cumpla con los criterios establecidos. SeqPrep es una herramienta también disponible en el repositorio GitHub: [https://github.com/jstjohn/SeqPrep](https://github.com/jstjohn/SeqPrep)

> **NOTA:** Para fines prácticos, el programa SeqPrep (y sus dependencias) se encuentran en el mismo módulo de FASTX-toolkit, por lo que puede ejecutarse cargando el módulo `seqprep/1.3.2/gcc/8.3.1-npl3`. Antes de ejecutar el trabajo (SeqPrep.slurm), visualice la tarea, y llame después al archivo de ayuda para interpretar las variables a utilizar.

```bash
SeqPrep -h
sbatch SeqPrep.slurm
```

Analice los archivos de error y mensajes generados como resultado de ejecutar la tarea antes mencionada.

---

## Ejercicio 3 — Carpeta 3.454_Reads

Cargar el módulo de newbler (utilizar el comando `module avail` para mostrar los módulos disponibles) y ejecutar las siguientes líneas de comando:

```bash
srun --mem 16000 -n1 -p q1 sffinfo -s GJ40EWU01.sff > GJ40EWU01.fasta
srun --mem 16000 -n1 -p q1 sffinfo -q GJ40EWU01.sff > GJ40EWU01.qual
```

Solicite el archivo de ayuda para conocer otras variables disponibles del programa `sffinfo`, vea el interior de los archivos para reconocer sus formatos y la información contenida en estos, y finalmente genere un archivo fastq a partir de los archivos generados (si olvidó la manera de hacerlo, consulte el archivo Ejercicio01.txt disponible para esta práctica).

---

## Ejercicio 4 — Manipulación de archivos BAM

Algunas plataformas de secuenciación generan los datos de salida en formato BAM (binary alignment mapping), es por ello que es importante saber manipular este tipo de datos y extraer información de secuencias y calidades. Para esto utilizaremos las herramientas de samtools y bedtools.

**Paso 1.** Convertiremos un archivo en formato BAM a formato SAM:

```bash
module load samtools/1.10/gcc/8.3.1-jqix
srun --mem 8G -n1 -p q2 samtools view -h -o pacbio.sam --threads 1 pacbio.bam
module purge
```

**Paso 2.** A partir del archivo en formato BAM, extraeremos la información referente a las secuencias y calidades en formato fastq:

```bash
module load bedtools2/2.27.1/gcc/8.3.1-7tc5
srun --mem 8G -n1 -p q2 bamToFastq -i pacbio.bam -fq pacbio.fastq
module purge
```

Finalmente, consultaremos el tamaño de las lecturas del archivo fastq con la ayuda de bioawk:

```bash
module load bioawk/1.0/gcc/8.3.1-moy3
srun --mem 8G -n1 -p q2 bioawk -c fastx '{ print $name, length($seq) }' pacbio.fastq > pacbio_length.tsv
```

Podemos consultar el rango de tamaños con ayuda de los comandos `head` y `tail`:

```bash
srun --mem 8G -n1 -p q2 sort -k2,2 -n pacbio_length.tsv | head -n 1
srun --mem 8G -n1 -p q2 sort -k2,2 -n pacbio_length.tsv | tail -n 1
```

También es posible determinar el tamaño promedio de las lecturas con awk:

```bash
srun --mem 8G -n1 -p q2 awk '{sum = sum + $2} END {print sum/NR}' pacbio_length.tsv
```


[← Volver a la portada](./)

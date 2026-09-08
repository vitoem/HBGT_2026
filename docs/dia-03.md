---
layout: default
title: "Día 03 · Control y procesamiento de lecturas"
---

<span class="eyebrow">Lunes · 21 septiembre</span>

# 🔬 Día 3: Control y Procesamiento de Lecturas

Bienvenid@s a la página de recursos del **Día 3** del curso **"Herramientas Bioinformáticas para el Análisis de Genomas y Transcriptomas"**. En esta jornada nos enfocaremos de manera integral en el control de calidad, procesamiento y preprocesamiento de lecturas de Secuenciación de Siguiente Generación (NGS). Aprenderemos a manipular formatos crudos, evaluar perfiles de calidad e implementar flujos de filtrado avanzados en sistemas de Cómputo de Alto Rendimiento (HPC).

###  Teoría: Tecnologías NGS, Librerías y Formato FASTQ

### 1. El Dogma Central y las Ciencias Ómicas
El análisis bioinformático moderno requiere comprender cómo fluye la información biológica y cómo las distintas disciplinas ómicas abordan este flujo:
*   **Genómica:** Estudia el genoma para responder a *lo que puede pasar*. Involucra el ensamblado de novo, mapeo y predicción de modelos génicos.
*   **Transcriptómica:** Examina el conjunto de transcritos (ARN) para revelar *lo que parece estar sucediendo* en un momento o bajo una condición biológica determinada.
*   **Proteómica y Metabolómica:** Estudian las proteínas y metabolitos respectivamente, representando *lo que hace que suceda* y *lo que ha sucedido/está sucediendo* a nivel celular.

### 2. Flujo Metodológico en Secuenciación NGS
Las tecnologías NGS procesan masivamente fragmentos de ácidos nucleicos a través de tres etapas principales:
1.  **Preparación de Bibliotecas (Librerías):** Fragmentación física o enzimática del ADN/ARN y ligación *in vitro* de adaptadores moleculares específicos a los extremos para permitir su posterior anclaje y secuenciación.
2.  **Amplificación Clonal:** Necesaria para incrementar la intensidad de la señal física detectable. Se realiza mediante **PCR en puente** (*bridge PCR*, sistema Illumina) o **PCR en emulsión** (sistemas como 454 o SOLiD).
3.  **Secuenciación Cíclica:** Adición ordenada de bases detectadas secuencialmente en tiempo real. Los métodos predominantes son:
    *   **Pirosecuenciación** (ej. Secuenciador 454).
    *   **Secuenciación por ligación** (ej. Plataforma SOLiD).
    *   **Secuenciación por síntesis** (ej. Tecnología Solexa/Illumina).

Las tecnologías de tercera generación, como **Pacific Biosciences (PacBio)** (secuenciación de molécula única en tiempo real) y **Oxford Nanopore** (medición del paso de nucleótidos a través de un poro proteico embebido en una membrana), permiten la secuenciación de moléculas largas sin necesidad de amplificación clonal previa.

### 3. Anatomía de un Archivo FASTQ y la Escala de Calidad Phred
La salida estándar de las plataformas NGS es un archivo de texto plano denominado **FASTQ**, el cual contiene la secuencia biológica y su calidad asociada base por base. Cada lectura ocupa estrictamente **4 líneas**:

1.  **Línea 1:** Comienza con `@` y contiene el identificador único de la secuencia junto con metadatos del secuenciador.
2.  **Línea 2:** La secuencia de nucleótidos leída (`A, C, T, G, N`).
3.  **Línea 3:** Comienza con `+` y actúa como un separador simple (opcionalmente puede repetir el identificador).
4.  **Línea 4:** Cadena de caracteres codificados en formato **ASCII** que representan los valores numéricos de calidad de la escala de Phred.

#### La Fórmula de Calidad Phred ($Q$)
La calidad Phred evalúa logarítmicamente la probabilidad de que una base haya sido llamada de forma incorrecta ($P$):

$$Q = -10 \log_{10}(P)$$

Un valor de **Phred Score ($Q$)** se interpreta bajo el estándar industrial de la siguiente forma:
*   **$Q = 10$**: Probabilidad de error de $1/10$ ($10\%$). Precisión de llamada del $90.0\%$.
*   **$Q = 20$**: Probabilidad de error de $1/100$ ($1\%$). Precisión de llamada del $99.0\%$.
*   **$Q = 30$**: Probabilidad de error de $1/1000$ ($0.1\%$). Precisión de llamada del $99.9\%$.
*   **$Q = 40$**: Probabilidad de error de $1/10000$ ($0.01\%$). Precisión de llamada del $99.99\%$.

---

## 💻 Guía Práctica 01: Preprocesamiento de Secuencias

Esta guía contiene los cuatro ejercicios de la **Práctica 01**, diseñados para ser ejecutados en el clúster de HPC de manera interactiva o mediante tareas en lote (*jobs*).

### 📂 Ejercicio 1: Exploración e Inspección de Datos Single-End

Este ejercicio se enfoca en el manejo inicial de archivos comprimidos, la inspección de la estructura FASTQ y la conversión elemental de calidad ASCII.

#### 1. Compresión y Descompresión
Los archivos de secuenciación crudos suelen ser masivos y se resguardan en formato comprimido (`.gz`). Para descomprimir un archivo en el clúster usando recursos gestionados por **SLURM**, ejecuta:

```bash
# Solicitar recursos interactivos para descompresión con gunzip
srun --mem 8G -n1 -p q1 gunzip IlluminaReads_NewStyle.fastq.gz
```

Si necesitas volver a comprimir el archivo para optimizar espacio en disco, puedes correr:

```bash
# Comprimir archivo fastq a formato comprimido gz
srun --mem 8G -n1 -p q1 gzip IlluminaReads_NewStyle.fastq
```

#### 2. Inspección Visual de Lecturas
Para visualizar la estructura interna del archivo sin saturar la memoria ni la terminal, puedes emplear los comandos `less`, `head` o `tail`:

```bash
# Ver contenido paginado (presiona 'q' para salir del visualizador)
less IlluminaReads_NewStyle.fastq

# Visualizar las primeras 12 líneas (equivalente a las primeras 3 secuencias)
head -n 12 IlluminaReads_NewStyle.fastq
```

#### 3. Conteo de Secuencias
Es fundamental corroborar el volumen total de datos crudos antes de filtrar. Podemos contar cuántas secuencias existen buscando un patrón constante en los encabezados únicos de la plataforma de secuenciación:

```bash
# Contar coincidencias con el identificador del secuenciador
grep -c "@NB501110" IlluminaReads_NewStyle.fastq
```

#### 4. Conversión de Calidad (FASTX-Toolkit)
Diferentes plataformas utilizan variantes de codificación ASCII (Phred+33 o Phred+64). Para homogeneizar los valores, cargamos el módulo correspondiente y ejecutamos el conversor:

```bash
# Cargar módulo de fastx-toolkit
module load fastx-toolkit/0.0.14/gcc/8.3.1-6qup

# Ver el menú de ayuda del conversor
fastq_quality_converter -h

# Ejecutar conversión de calidad interactiva asignando recursos
srun --mem 16000 -n 1 -p q2 fastq_quality_converter -n -Q33 -i IlluminaReads_NewStyle.fastq -o IlluminaReads_Phred.fastq
```

#### 5. Modificación de Identificadores por Terminal
A veces requerimos cambiar el formato de los encabezados de las secuencias para que sean compatibles con software bioinformático antiguo. Usaremos un procesador de datos de texto plano (`awk`) para realizar esta reestructuración:

```bash
# Generar versión OldStyle 01 (agregando el encabezado original al final entre paréntesis)
cat IlluminaReads_NewStyle.fastq | awk '{if (NR % 4 == 1) {split($1, arr, ":"); printf "%s_%s:%s:%s:%s:%s#0/%s (%s)\n", arr[1], arr[3], arr[4], arr[5], arr[6], arr[7], substr($2, 1, 1), $0} else if (NR % 4 == 3){print "+"} else {print $0} }' > IlluminaReads_OldStyle01.fastq

# Generar versión OldStyle 02 (limpia, sin agregar el encabezado original al final)
cat IlluminaReads_NewStyle.fastq | awk '{if (NR % 4 == 1) {split($1, arr, ":"); printf "%s_%s:%s:%s:%s:%s#0/%s\n", arr[1], arr[3], arr[4], arr[5], arr[6], arr[7], substr($2, 1, 1), $0} else if (NR % 4 == 3){print "+"} else {print $0} }' > IlluminaReads_OldStyle02.fastq
```

#### 6. Separar Archivos FASTQ en FASTA y QUAL (y viceversa)
Para dividir los datos de secuencias de sus calidades numéricas asociadas, empleamos un script de Python disponible en el entorno Qiime:

```bash
# Activar ambiente de conda de qiime1
conda activate qiime1-1.9.1

# Generar archivos .fna (fasta) y .qual (calidades) a partir del FASTQ
srun --mem 16000 -n1 -p q2 python convert_fastaqual_fastq.py -c fastq_to_fastaqual -f IlluminaReads_NewStyle.fastq
```

Como alternativa, si solo deseas convertir FASTQ a FASTA de forma directa, puedes utilizar la suite **EMBOSS**:

```bash
# Cargar el módulo EMBOSS
module load emboss/6.6.0/gcc/9.3.0-4geh

# Ejecutar conversión seqret
srun --mem 8G -n1 -p q1 seqret -sequence IlluminaReads_NewStyle.fastq -outseq IlluminaReads_NewStyle.fasta
```

Si necesitas realizar el proceso inverso, es decir, acoplar archivos independientes de FASTA (`.fna`) y calidad (`.qual`) para reconstruir un archivo FASTQ unificado:

```bash
# Reconstruir archivo FASTQ a partir de fasta y qual
srun --mem 16000 -n1 convert_fastaqual_fastq.py -c fastaqual_to_fastq -f IlluminaReads_NewStyle.fna -q IlluminaReads_NewStyle.qual
```

---

### 📊 Ejercicio 2: Diagnóstico y Filtrado de Lecturas Single-End y Paired-End

#### 1. Análisis de Calidad Automatizado con FastQC
Para obtener un reporte visual detallado de la calidad de nuestras bibliotecas crudas, ejecutamos **FastQC**:

```bash
# Limpiar ambiente de módulos previos para evitar interferencia
module purge

# Cargar módulo oficial de FastQC en el clúster
module load fastqc/0.11.7/gcc/9.3.0-o4ca

# Ejecutar análisis en el clúster
srun --mem 16000 -n1 -p q1 fastqc IlluminaReads_NewStyle.fastq
```

Dado que la terminal no despliega archivos interactivos `.html`, debemos transferir el reporte generado a nuestro host local usando **rsync** o comandos equivalentes desde la terminal de nuestra máquina personal:

```bash
# EJECUTAR ESTO DESDE TU MÁQUINA LOCAL (reemplazar variables del servidor)
rsync -av --progress --bwlimit=20000 -e 'ssh -p PORT' $USUARIO@IP:$PATH_AL_CURSO/Practica01/1.SingleEnd_Reads/*.html .
```

#### 2. Filtrado de Calidad con FASTX-Toolkit
Podemos filtrar lecturas descartando aquellas de baja calidad o recortando extremos empleando herramientas del paquete FASTX:

```bash
# Cargar módulo compatible de FASTX
module load fastx-toolkit/0.0.14/gcc/8.3.1-gofi

# Filtrado estricto por umbrales (-q 30 indica calidad mínima Phred de 30; -p 100 indica que el 100% de la lectura debe cumplirlo)
srun --mem 16000 -n1 -p q2 fastq_quality_filter -Q33 -q 30 -p 100 -i IlluminaReads_NewStyle.fastq -o IlluminaReads_Filtered01.fastq

# Recorte de extremos por calidad (fastq_quality_trimmer)
# -t 25: Recorta extremos si la calidad cae de 25. -l 30: Elimina lecturas remanentes menores a 30 pb.
srun --mem 16000 -n1 -p q2 fastq_quality_trimmer -Q33 -t 25 -l 30 -i IlluminaReads_NewStyle.fastq -o IlluminaReads_Filtered02.fastq
```

#### 3. Recorte Avanzado por Ventanas Móviles (Trimmomatic - SE)
Trimmomatic permite evaluar la calidad a través de una ventana deslizable, recortando tan pronto como la calidad promedio del fragmento decae:

```bash
# Cargar Trimmomatic
module load trimmomatic/0.38/gcc/8.3.1-jwk4

# Ejecutar Trimmomatic en modo Single End (SE)
# Evaluamos en ventanas de 4 bases (SLIDINGWINDOW:4:20), recortando si el promedio de calidad cae de 20.
# Conservamos únicamente lecturas resultantes con un tamaño mínimo de 36 nucleótidos (MINLEN:36).
srun --mem 8G -n2 -p q1 trimmomatic SE -threads 2 -phred33 IlluminaReads_NewStyle.fastq IlluminaReads_Filtered03.fastq LEADING:15 TRAILING:15 SLIDINGWINDOW:4:20 MINLEN:36
```

#### 4. Procesamiento de Lecturas Pareadas (Paired-End_Reads)
Al filtrar archivos de extremos pareados (Forward `R1` y Reverse `R2`), debemos garantizar que los pares de secuencias se mantengan alineados. Si una secuencia correspondiente a un par es eliminada, el par huérfano remanente debe ser segregado o descartado para evitar colapsos en las herramientas de ensamblado o mapeo río abajo:

```bash
# Cargar el módulo de herramientas NGS del curso
module load q1/ngstools/master

# Filtrar reads manteniendo el pareado con qualityControl.py
# -q 20: Calidad mínima. -p 90: % mínimo de bases que deben cumplir la calidad. -a 30: Longitud mínima aceptada.
srun -n1 --mem 16000 -p q1 qualityControl.py -1 R1.fastq -2 R2.fastq -q 20 -p 90 -a 30 -o1 HQA_R1.fastq -o2 HQA_R2.fastq
```

También podemos correr estos análisis a través de un script de lote (`sbatch qualityControl.slurm`) o configurar filtros PE equivalentes con Trimmomatic empleando los parámetros: `LEADING:15 TRAILING:15 SLIDINGWINDOW:4:20 MINLEN:36`.

#### 5. Remoción de Adaptadores Moleculares (SeqPrep)
Cuando identificamos contaminación por adaptadores mediante FastQC, empleamos herramientas dedicadas como **SeqPrep** para limpiar nuestras bibliotecas:

```bash
# Cargar el módulo que contiene SeqPrep
module load seqprep/1.3.2/gcc/8.3.1-npl3

# Consultar el menú de ayuda
SeqPrep -h

# Someter la tarea del pipeline de limpieza a la cola de procesamiento
sbatch SeqPrep.slurm
```

---

### 📼 Ejercicio 3: Extracción de Secuencias 454 (Archivos SFF)

Las lecturas provenientes del secuenciador Roche 454 se almacenan de forma nativa en un formato binario estructurado llamado **SFF** (Standard Flowgram Format). Para poder utilizarlas en herramientas estándar de análisis, debemos extraer su contenido de nucleótidos y calidades en formatos independientes:

```bash
# Cargar el módulo Newbler disponible en el clúster (verifica con 'module avail' su versión exacta)
# Usar sffinfo para extraer la secuencia biológica a FASTA
srun --mem 16000 -n1 -p q1 sffinfo -s GJ40EWU01.sff > GJ40EWU01.fasta

# Usar sffinfo para extraer las calidades asociadas a formato QUAL
srun --mem 16000 -n1 -p q1 sffinfo -q GJ40EWU01.sff > GJ40EWU01.qual
```

---

### 📂 Ejercicio 4: Extracción y Manipulación de Archivos BAM (Lecturas PacBio)

Algunas plataformas avanzadas como PacBio generan sus salidas crudas en formato **BAM** (un mapeo binario comprimido). Aprender a interactuar con estos archivos es crucial para rescatar la información de longitud y calidad de secuencias de moléculas largas.

#### Paso 1. Conversión de BAM a SAM (Formato Legible)
Para realizar una inspección directa de los datos en un formato legible por humanos, convertimos el archivo binario BAM a un formato SAM (Sequence Alignment Map):

```bash
# Cargar Samtools
module load samtools/1.10/gcc/8.3.1-jqix

# Convertir conservando el encabezado (-h) utilizando un hilo
srun --mem 8G -n1 -p q2 samtools view -h -o pacbio.sam --threads 1 pacbio.bam

# Limpiar ambiente
module purge
```

#### Paso 2. Extracción de FASTQ a partir de BAM
Para rescatar la información original de secuencias y calidades en formato FASTQ, empleamos la herramienta `bamToFastq` de la suite **bedtools**:

```bash
# Cargar bedtools
module load bedtools2/2.27.1/gcc/8.3.1-7tc5

# Extraer secuencias crudas directamente a un archivo fastq
srun --mem 8G -n1 -p q2 bamToFastq -i pacbio.bam -fq pacbio.fastq

# Limpiar ambiente
module purge
```

#### Paso 3. Análisis de Longitud de Lecturas con Bioawk
Para evaluar la distribución del tamaño de secuencias de lecturas largas, empleamos la herramienta de procesamiento biológico **bioawk**:

```bash
# Cargar bioawk
module load bioawk/1.0/gcc/8.3.1-moy3

# Generar un archivo de dos columnas tabulado conteniendo el identificador y su longitud en pb
srun --mem 8G -n1 -p q2 bioawk -c fastx '{ print $name, length($seq) }' pacbio.fastq > pacbio_length.tsv
```

#### Paso 4. Determinar Rangos y Promedios de Tamaño
Con el reporte tabulado de tamaños, podemos interrogar rápidamente la distribución de longitudes empleando comandos básicos de Linux:

```bash
# Encontrar la lectura con el tamaño mínimo (más pequeña)
srun --mem 8G -n1 -p q2 sort -k2,2 -n pacbio_length.tsv | head -n 1

# Encontrar la lectura con el tamaño máximo (más grande)
srun --mem 8G -n1 -p q2 sort -k2,2 -n pacbio_length.tsv | tail -n 1

# Calcular la longitud promedio de todas las lecturas contenidas en el archivo usando awk
srun --mem 8G -n1 -p q2 awk '{sum = sum + $2} END {print sum/NR}' pacbio_length.tsv
```
---

[← Volver a la portada](./)

---
layout: default
title: "Día 06 · Predicción génica y elementos repetitivos"
---

<span class="eyebrow">Jueves · 24 septiembre</span>

# Día 6: Identificación de RNAs No Codificantes (ncRNAs) y Elementos Repetitivos.

Bienvenid@s a la página de recursos del **Día 6** del curso **"Herramientas Bioinformáticas para el Análisis de Genomas y Transcriptomas"**. En esta jornada exploraremos los componentes más abundantes y dinámicos de los genomas eucariotas: la fracción repetitiva dominada por los **elementos transponibles (TEs)** y la fracción no codificante funcional representada por los **RNAs no codificantes (ncRNAs)**.

---

## 🔬 Sección 1: Elementos Transponibles (TEs) y DNA Repetitivo

Los **Elementos Transponibles (TEs)** son secuencias de ADN capaces de moverse o duplicarse dentro de un genoma. Constituyen una proporción masiva del ADN repetitivo en plantas y animales, desempeñando un papel clave en la evolución, reestructuración cromosómica y regulación génica.

### 1. Clasificación General de los Elementos Transponibles
Los elementos transponibles se dividen en dos clases principales según su mecanismo de transposición:

*   **Clase I (Retrotransposones):** Se mueven mediante un mecanismo de *"copiar y pegar"* a través de un intermediario de ARN que se retranscribe a ADN mediante la enzima **transcriptasa reversa (RT)**.
*   **Clase II (Transposones de ADN):** Se desplazan mediante un mecanismo de *"cortar y pegar"* catalizado por una enzima **transposasa**, o mediante duplicación por círculo rodante (Helitrones).

### 2. Estructura Molecular de los Retrotransposones LTR
Los retrotransposones con repeticiones largas terminales (**LTR**) son especialmente abundantes en genomas vegetales. Su tamaño oscila entre **1,000 y 20,000 pares de bases** y poseen dominios funcionales altamente conservados:

```text
  [TSR]--[LTR]--[PBS]--[gag]--[pol (PR - RT - RH - INT)]--[PPT]--[LTR]--[TSR]
```

#### Componentes Estructurales Clave:
*   **LTR (Long Terminal Repeat):** Regiones repetidas en los extremos que no codifican proteínas, pero contienen los promotores y terminadores de la transcripción.
*   **PBS (Primer Binding Site):** Sitio de unión del iniciador, complementario a tRNAs celulares que sirven como cebadores para la síntesis de cDNA.
*   **PPT (Polypurine Tract):** Canal rico en purinas necesario para el inicio de la síntesis de la segunda cadena de ADN.
*   **TSR (Target Site Repeat):** Repetición directa corta (4 a 6 pb) que flanquea los extremos del transposón, generada como huella durante la integración en el sitio blanco.

#### Dominios Proteicos Codificados:
1.  **gag:** Codifica proteínas estructurales involucradas en la maduración y empaquetamiento del complejo ribonucleoproteico.
2.  **pol:** Poliproteína que es procesada por una proteasa (**PR**) y que incluye:
    *   **RT (Transcriptasa Reversa):** Sintetiza ADN a partir del molde de ARN.
    *   **RH (RNAsa H):** Degrada la hebra de ARN del híbrido ARN:ADN.
    *   **INT (Integrasa):** Cataliza la inserción del nuevo cDNA en una posición genómica diferente.

---

## Sección 2: El Transcriptoma No Codificante y los lncRNAs

Tradicionalmente se consideraba que el ARN solo actuaba como un intermediario pasivo entre el ADN y las proteínas (mRNAs). Sin embargo, la secuenciación masiva del transcriptoma reveló que aproximadamente el **90% del genoma se transcribe**, pero únicamente entre el **1% y 2% corresponde a mRNAs codificantes**. El resto, anteriormente etiquetado como "materia oscura" o "ADN basura", cumple funciones regulatorias esenciales.

### 1. Definición y Propiedades de los lncRNAs
Los **RNAs largos no codificantes (lncRNAs)** son moléculas de ARN con una longitud **mayor a 200 nucleótidos** que no se traducen a proteínas pero poseen capacidades regulatorias complejas.

#### Tabla Comparativa: mRNA vs. lncRNA

| Característica | mRNA | lncRNA |
| :--- | :--- | :--- |
| **Tamaño** | Largos (variable según la proteína) | Cortos o medianos, pero **> 200 nt** |
| **Especificidad de Expresión** | Mayoritariamente constitutiva o tisular amplia | **Altamente tejido-específicos** y dependientes de estadio de desarrollo |
| **Nivel de Expresión** | Niveles de abundancia moderados a altos | **Bajos niveles de expresión** en comparación con mRNAs |
| **Biogénesis** | RNA Polimerasa II | RNA Polimerasa I, II, III, IV y V (especialmente en plantas) |
| **Procesamiento** | Caperuza 5' (5' cap) y cola Poli-A en 3' | Caperuza 5' y cola Poli-A; algunos carecen de cola Poli-A |
| **Conservación de Secuencia** | Alta conservación entre especies | **Baja conservación de secuencia** (evolución rápida) |

### 2. Origen Evolutivo de los lncRNAs
Los lncRNAs surgen a través de diversos mecanismos genómicos:
*   **Duplicación Genómica:** Duplicación de genes codificantes seguida de pérdida de la capacidad de traducción.
*   **Pseudogenización:** Acumulación de mutaciones que inactivan el marco abierto de lectura (ORF).
*   **Exaptación de Elementos Transponibles:** Reutilización de secuencias de TEs como promotores o módulos de ARN.
*   **Exaptación de ADN Intergénico:** Transcripción de regiones previamente no codificantes que adquieren función.

### 3. Clasificación Genómica de los lncRNAs
Según su posición relativa respecto a los genes codificantes vecinos, los lncRNAs se clasifican en:

```text
  Intergénico (lincRNA):  [Gen A] -------- [lncRNA] -------- [Gen B]
  Intrónico:              [Exón 1] --- (lncRNA) --- [Exón 2]
  Antisentido (lncNAT):   [--- Gen Codificante --->]
                          [<--- lncRNA Antisentido -]
  Asociado a TEs/Enhancers: Coincide o solapa con elementos reguladores o repetitivos.
```

1.  **lincRNAs (Long Intergenic ncRNAs):** Ubicados en regiones intergénicas, alejados de genes codificantes.
2.  **lncRNAs Intrónicos:** Transcritos completamente dentro de los intrones de un gen codificante.
3.  **lncRNAs Sentido y Antisentido (lncNATs):** Transcritos desde la hebra opuesta a un gen codificante, solapando parcial o totalmente con sus exones o intrones.
4.  **lncRNAs Asociados a Enhancers o TEs:** Derivados de secuencias reguladoras o elementos repetitivos.

---

## 💻 Sección 3: Flujos de Trabajo y Herramientas Bioinformáticas

Debido a su baja conservación de secuencia y sus bajos niveles de expresión, la identificación de lncRNAs requiere pipelines rigurosos para descartar transcritos codificantes o artefactos de ensamblaje.

```text
  [Transcritos Assemblados (RNA-Seq)]
                 │
                 ▼  Filtrar por Longitud (>200 nt)
  [Transcritos Largos]
                 │
                 ▼  Evaluar Potencial Codificante (Eliminar ORFs >100 aa / Homología)
  [Candidatos No Codificantes]
                 │
                 ▼  Clasificación Genómica y Funcional
  [lncRNAs Validados (lincRNA, lncNAT, Intrónicos)]
```

### 1. Herramientas Especializadas de Predicción
*   **FEELnc:** Diseñado para ensamblajes *de novo* y genomas anotados; utiliza modelos de aprendizaje automático para evaluar el potencial codificante y clasificar la posición genómica.
*   **PLncPRO:** Herramienta especializada en transcriptomas vegetales basada en Random Forest.
*   **PLEK:** Basado en frecuencias de $k$-meros, ideal para datos de RNA-Seq sin genoma de referencia.
*   **Evolinc:** Pipeline integral que identifica lncRNAs y evalúa su conservación evolutiva entre múltiples especies.

### 2. Estrategia de Inferencia Funcional
Dado que los lncRNAs no poseen dominios proteicos conservados, su función biológica se infiere mediante:
*   **Análisis de Genes Vecinos:** Inspección de la función de los genes codificantes situados en la proximidad genómica del lncRNA.
*   **Redes de Co-expresión:** Cálculo de la correlación de expresión (p. ej., coeficiente de Pearson) entre el lncRNA y los mRNAs a lo largo de diferentes tejidos o condiciones de estrés.
*   **Enriquecimiento Gene Ontology (GO):** Evaluación de las categorías GO de los genes codificantes altamente correlacionados con el lncRNA.

---

## Prácticas 06–07 — RNAs no codificantes largos, ncRNAs y Elementos Transponibles

Después de haber predicho los modelos génicos "codificantes" del genoma (Práctica05), estas dos prácticas amplían el análisis hacia otros elementos del genoma que no codifican proteínas de forma directa o que no son genes en el sentido clásico: los **RNAs largos no codificantes (lncRNAs)**, otros **RNAs no codificantes (ncRNAs)** como tRNAs, y los **elementos transponibles (TEs)**, cuya identificación y enmascaramiento es frecuentemente un paso previo indispensable para una predicción génica más precisa.

---

## <span id="practica-06"> Práctica06: Identificación de lncRNAs con Evolinc-I </span>

En este ejercicio se identificarán transcritos correspondientes a RNAs largos no codificantes (lncRNAs) a partir de un ensamblado de transcriptoma y la anotación del genoma, utilizando el pipeline **Evolinc-I**. Posteriormente se explorará la relación espacial de estos lncRNAs con los genes vecinos en el genoma.

**Paso 1.** Crea un directorio llamado `01.Practica_lncRNAs` y mueve a él los siguientes archivos (si ya los tienes en una carpeta aparte, omite este paso y solo cambia tu directorio de trabajo a donde se encuentren):

- `annotation_chr38.gtf`
- `genome_chr38.fa`
- `transcript_chr38.gtf`

**Paso 2.** Crea, con tu editor de texto preferido en la terminal (nano, vim), un script llamado `Evolinc.slurm`.

**Paso 3.** En el script copia lo siguiente:

```bash
#!/bin/sh
#SBATCH -J EvolincI
#SBATCH -n 10
#SBATCH -N 1
#SBATCH --mem 10000
#SBATCH -t 365-00
#SBATCH -e evolinci.e%j
#SBATCH -o evolinci.o%j
#SBATCH -p q1

#q1 module
module load evolinc-i-git/1.7.5/gcc/9.3.0-bep2

GENOMEANNOTATION=annotation_chr38.gtf
GENOME=genome_chr38.fa
TRANSCRIPTS=transcript_chr38.gtf

#####Ejecutar Evolinc-I#######

evolinc-part-I.sh -c ${TRANSCRIPTS} -g ${GENOME} -u ${GENOMEANNOTATION} -o Results -n 10
```

**Paso 4.** Guarda los cambios, carga el módulo de Evolinc y abre el manual. Ejecuta el script.

**Paso 5.** Cambia tu directorio de trabajo a "Results", explora los archivos que se generaron y revisa los archivos de error y salida (`evolinci.o*`, `evolinci.e*`).

**Paso 6.** Regresa al directorio de trabajo anterior y crea un nuevo script llamado `Sequence_lenght.slurm` con el siguiente contenido:

```bash
#!/bin/bash
#SBATCH -J SeqLen
#SBATCH -n 1
#SBATCH --mem 1000
#SBATCH -t 365-00
#SBATCH -e seqlenght.e%j
#SBATCH -o seqlenght.o%j
#SBATCH -p q2

module load emboss/6.6.0/gcc/8.3.1-7aag

FILE=/PATH/TO/03b.lncRNAs/08.Ejercicio_HBGT/02.Evolinc/Results/transcript_chr38.gtf.lincRNAs.fa

	infoseq ${FILE} -only -name -length -pgc -outfile SL_lncRNAs.txt
```

**Paso 7.** Guarda los cambios y ejecuta el script. Revisa el archivo que se acaba de generar.

**Paso 8.** Crea un nuevo script llamado `Gffread.slurm` con el siguiente contenido:

```bash
#!/bin/sh
#SBATCH -J Gffread
#SBATCH -n 20
#SBATCH -N 1
#SBATCH --mem 100000
#SBATCH -t 365-00
#SBATCH -e gffread.e%j
#SBATCH -o gffread.o%j
#SBATCH -p q1

module load gffread/0.12.7/gcc/9.3.0-nllg
module load  emboss/6.6.0/gcc/9.3.0-4geh

WDIR=$(pwd)
GENOMEANNOTATION=annotation_chr38.gtf
GENOME=genome_chr38.fa
lncRNA=/PATH/TO/03b.lncRNAs/08.Ejercicio_HBGT/02.Evolinc/Results/transcript_chr38.gtf.lincRNAs.bed

#########Extract sequences from genome

gffread -g ${GENOME} ${WDIR} -w NeighborSequences30Mb.fna --w-add 30000 ${lncRNA}
```

**Paso 9.** Ejecuta y revisa el archivo de salida.

**Paso 10.** Crea un nuevo script llamado `Bedtools.slurm` con el siguiente contenido:

```bash
#!/bin/sh
#SBATCH -J Bedtools
#SBATCH -n 1
#SBATCH --mem 1000
#SBATCH -t 365-00
#SBATCH -e bedtools.e%j
#SBATCH -o bedtools.o%j
#SBATCH -p q2

#q2 module
module load bedtools2/2.27.1/gcc/8.3.1-nh4a

LNCRNA=/PATH/TO/03b.lncRNAs/08.Ejercicio_HBGT/02.Evolinc/Results/transcript_chr38.gtf.lincRNAs.bed
GENOME=/PATH/TO/03b.lncRNAs/08.Ejercicio_HBGT/02.Evolinc/genome_chr38.fa


#grep -w "gene" /PATH/TO/03b.lncRNAs/08.Ejercicio_HBGT/02.Evolinc/annotation_chr38.gtf | awk '{OFS="\t"; print $1,$4-1,$5,$9,$6,$7}' > genes.bed
```

**Paso 11.** Guarda los cambios y ejecuta. Revisa el archivo de salida.

**Paso 12.** Abre nuevamente el script `Bedtools.slurm` y agrega la siguiente línea (no olvides comentar con `#` la línea de código anterior):

```bash
bedtools closest -a genes.bed -b ${LNCRNA} -D b > lncRNA_nearby_genes.txt
```

**Paso 13.** Ejecuta y revisa el archivo de salida. Agrega nuevamente otra línea de código al script:

```bash
#bedtools getfasta -fi ${GENOME} -bed lncRNA_nearby_genes.txt -fo NeighborGenes.fa
```

**Paso 14.** Cuenta las líneas en el archivo `lncRNA_nearby_genes.txt` y cuenta cuántas secuencias hay en `NeighborGenes.fa`.

---
## Práctica 06.1: Construyendo una red de co-expresión con WGNCA en menos de 20 pasos

**NOTA** Este script esta basado en este tutorial: https://bioinformaticsworkbook.org/tutorials/wgcna.html#gsc.tab=0

**Paso 1.** Preparación del entorno

Comencemos instalando los requerimientos necesarios para que WGCNA pueda instalarse y ejecutarse de manera adecuada.

```r
# Instalamos BiocManager

install.packages("BiocManager")

# Verificamos la versión de Bioconductor instalada

BiocManager::version()

# Cargamos las librerías que utilizaremos durante el análisis

library(impute)
library(preprocessCore)
library(tidyverse)
library(magrittr)
library(DESeq2)
library(genefilter)
library(WGCNA)

# Verificamos la versión de WGCNA instalada

packageVersion("WGCNA")
```

Una vez cargadas las librerías, podemos consultar el manual de WGCNA directamente desde R:

```r
??WGCNA
```

> **Nota:** Si alguno de los paquetes no está instalado, será necesario instalarlo antes de continuar. En este tutorial asumiremos que el entorno de trabajo ya se encuentra preparado.

**Paso 2.** Preparación del directorio de trabajo

Una vez que tenemos preparados los paquetes, vamos a establecer el directorio donde trabajaremos durante todo el tutorial.

En este caso utilizaremos un solo directorio y mantendremos todos los archivos del análisis dentro de él, para facilitar el seguimiento de las rutas de los archivos.

```r
# Establecemos el directorio de trabajo

setwd("/home/mpale/WGNCA_Tutorial") ###En este caso ese es mi directorio de trabajo, ajustalo al que más te convenga

# Verificamos que estamos trabajando en el directorio correcto

getwd()
```

**Paso 3.**. Carga de los datos

Una vez establecido el directorio de trabajo, vamos a cargar la matriz de conteos que utilizaremos para realizar el análisis.

Los datos corresponden al experimento de desarrollo de la lígula de maíz utilizado en el tutorial de WGCNA. La matriz contiene los genes en las filas y las muestras en las columnas.

En nuestro caso, el archivo `GSE61333_ligule_count.txt` ya se encuentra descomprimido dentro del directorio de trabajo.

```r
# Cargamos la matriz de conteos

data <- readr::read_delim(
  "GSE61333_ligule_count.txt",
  delim = "\t"
)

# Revisamos las primeras filas y columnas de la matriz

data[1:5, 1:10]
```

Primero revisamos la estructura de los datos para comprobar que la matriz se haya cargado correctamente.

```r
# Revisamos la estructura de los datos

str(data)
```

La primera columna corresponde a los identificadores de los genes, por lo que vamos a cambiar su nombre a `GeneId` para identificarla fácilmente durante los siguientes pasos.

```r
# Cambiamos el nombre de la primera columna a GeneId

names(data)[1] = "GeneId"

# Revisamos los nombres de las columnas

names(data)
```

De esta manera tendremos una matriz en la que `GeneId` identifica cada gen y las columnas restantes corresponden a las diferentes muestras del experimento.


**Paso 4.** Exploración y preparación de la matriz

Ahora que tenemos cargada la matriz de conteos, vamos a preparar los datos para poder explorar la distribución de los conteos entre las diferentes muestras.

Primero vamos a seleccionar los nombres de las muestras, excluyendo la columna que contiene los identificadores de los genes.

```r
# Tomamos los nombres de las muestras, excluyendo GeneId

col_sel = names(data)[-1]

# Revisamos los nombres de las muestras

col_sel
```

Para facilitar la exploración y visualización de los datos, vamos a transformar la matriz de un formato ancho a un formato largo. De esta manera tendremos una fila por cada combinación de gen y muestra.

```r
# Transformamos la matriz a formato largo

mdata <- data %>%
  tidyr::pivot_longer(
    col = all_of(col_sel)
  )

# Revisamos las primeras filas

mdata[1:10, ]
```

También vamos a obtener el grupo experimental al que pertenece cada muestra a partir de su nombre.

```r
# Extraemos el grupo experimental a partir del nombre de cada muestra

mdata <- mdata %>%
  mutate(
    group = gsub("-.*", "", name) %>%
      gsub("[.].*", "", .)
  )

# Revisamos nuevamente los datos

mdata[1:10, ]
```

Con esto tenemos una tabla que contiene el identificador del gen, el nombre de la muestra, el conteo correspondiente y el grupo experimental.

Esta transformación nos será útil para realizar una primera exploración de la distribución de los datos antes de iniciar la normalización.

**Paso 5.** Exploración de la distribución de los datos

Antes de continuar con la normalización, vamos a realizar una exploración inicial de los datos. Esto nos permite observar cómo se distribuyen los conteos entre las diferentes muestras y detectar posibles diferencias que posteriormente tendremos que considerar durante el análisis.

En este punto podemos utilizar un gráfico de violín para visualizar la distribución de los conteos de cada muestra.

```r
# Generamos un gráfico de violín para observar la distribución
# de los conteos en cada muestra

ggplot(mdata, aes(x = name, y = value)) +
  geom_violin() +
  theme_bw() +
  theme(
    axis.text.x = element_text(angle = 90)
  ) +
  labs(
    x = "Muestras",
    y = "Conteos de RNA-Seq"
  )
```

El gráfico nos permite observar de manera general la distribución de los conteos. En este punto todavía estamos trabajando con los datos originales, por lo que las diferencias en la distribución entre muestras no deben interpretarse como diferencias biológicas.

Más adelante normalizaremos los datos y volveremos a explorar su distribución para comprobar el efecto de este procedimiento.

**Paso 6.** Preparación de la matriz con DESeq2

Ahora vamos a preparar la matriz de conteos para realizar la normalización. Para esto utilizaremos `DESeq2`, que nos permitirá obtener una transformación de los datos adecuada para los análisis posteriores de expresión y co-expresión.

Primero conservamos únicamente la matriz de conteos, eliminando la columna que contiene los identificadores de los genes. Después utilizaremos esos identificadores como nombres de las filas.

```r
# Eliminamos la primera columna y convertimos los datos a una matriz

de_input = as.matrix(data[,-1])

# Asignamos los identificadores de los genes como nombres de las filas

row.names(de_input) = data$GeneId

# Revisamos una parte de la matriz

de_input[1:5, 1:10]
```

Ahora vamos a generar una tabla con la información correspondiente a cada muestra. A partir del nombre de las muestras recuperaremos el grupo experimental al que pertenece cada una.

```r
# Generamos la información de las muestras

meta_df <- data.frame(
  Sample = names(data[-1])
) %>%
  mutate(
    Type = gsub("-.*", "", Sample) %>%
      gsub("[.].*", "", .)
  )

# Revisamos la información de las muestras

meta_df
```

Esta información será utilizada por `DESeq2` para conocer la relación entre cada muestra y su grupo experimental.

Finalmente, construimos el objeto que utilizará `DESeq2` para trabajar con la matriz de conteos.

```r
# Generamos el objeto DESeqDataSet

dds <- DESeqDataSetFromMatrix(
  countData = round(de_input),
  colData = meta_df,
  design = ~Type
)

# Ejecutamos el procedimiento de normalización de DESeq2

dds <- DESeq(dds)
```

En este caso no estamos utilizando `DESeq2` para realizar un análisis diferencial. Lo utilizamos como parte de la preparación de los datos tomando en cuanta la varianza d los datos

**Paso 7.** Transformación y selección de genes variables

Ahora que tenemos preparado el objeto `DESeq2`, vamos a obtener los datos transformados mediante la **transformación de estabilización de la varianza** (*Variance Stabilizing Transformation*, VST).

Esta transformación reduce la dependencia de la varianza respecto al nivel de expresión y nos permite trabajar con valores de expresión más adecuados para el análisis de co-expresión.

```r
# Obtenemos los datos transformados mediante VST

wpn_vsd <- getVarianceStabilizedData(dds)

# Calculamos la varianza de cada gen

rv_wpn <- rowVars(wpn_vsd)

# Revisamos la distribución de las varianzas

summary(rv_wpn)
```

La matriz contiene miles de genes, pero no todos presentan suficiente variación entre las muestras para ser informativos en una red de co-expresión.

Por esta razón, vamos a conservar únicamente los genes que se encuentran por encima del **percentil 95 de la varianza**.

El tutorial original utiliza un umbral más bajo. En este caso utilizaremos el percentil 95 para reducir el número de genes y facilitar el procesamiento de la red.

```r
# Calculamos el percentil 95 de la varianza

q95_wpn <- quantile(rowVars(wpn_vsd), .95)

# Conservamos los genes cuya varianza se encuentra
# por encima del percentil 95

expr_normalized <- wpn_vsd[
  rv_wpn > q95_wpn,
]

# Revisamos una parte de la matriz resultante

expr_normalized[1:5, 1:10]

# Revisamos sus dimensiones

dim(expr_normalized)
```

Al finalizar este paso tendremos una matriz de expresión transformada y reducida a los genes con mayor variabilidad entre las muestras. Esta será la matriz que utilizaremos en los siguientes pasos para construir la red de co-expresión.

**Paso 8.** Exploración de los datos normalizados

Una vez que hemos realizado la transformación y seleccionado los genes más variables, vamos a revisar nuevamente la distribución de los datos.

Para esto transformaremos la matriz a formato largo y generaremos un gráfico de violín. A diferencia del gráfico del paso anterior, en este caso estamos utilizando los datos después de la transformación VST y del filtrado por varianza.

```r
id="n8k2fa"
# Convertimos la matriz normalizada a un data frame

expr_normalized_df <- data.frame(expr_normalized) %>%
  mutate(
    Gene_id = row.names(expr_normalized)
  ) %>%
  pivot_longer(-Gene_id)

# Revisamos las primeras filas

expr_normalized_df[1:10, ]
```

Ahora podemos visualizar la distribución de la expresión normalizada en cada muestra.

```r
id="q7m4tx"
# Generamos un gráfico de violín con los datos normalizados

expr_normalized_df %>%
  ggplot(aes(x = name, y = value)) +
  geom_violin() +
  theme_bw() +
  theme(
    axis.text.x = element_text(angle = 90)
  ) +
  labs(
    title = "Expresión normalizada",
    x = "Muestras",
    y = "Expresión normalizada"
  )
```

La transformación permite comparar las distribuciones de las muestras en una escala más apropiada para los análisis posteriores.

En este punto también podemos observar si alguna muestra presenta un comportamiento muy diferente al resto. Sin embargo, la identificación formal de posibles muestras atípicas la realizaremos posteriormente mediante el agrupamiento de las muestras, antes de construir la red de co-expresión.


**Paso 9.** Preparación de la matriz para WGCNA

Ahora que tenemos los datos normalizados y hemos seleccionado los genes más variables, vamos a preparar la matriz que utilizaremos para construir la red de co-expresión.

WGCNA trabaja con una matriz en la que **las filas corresponden a las muestras y las columnas a los genes**. Actualmente nuestra matriz `expr_normalized` tiene la orientación contraria: los genes se encuentran en las filas y las muestras en las columnas.

Por lo tanto, vamos a transponer la matriz.

```r
id="2q7vka"
# Transponemos la matriz para que las filas correspondan
# a las muestras y las columnas a los genes

input_mat = t(expr_normalized)

# Revisamos una parte de la matriz

input_mat[1:5, 1:10]

# Revisamos sus dimensiones

dim(input_mat)
```

Antes de comenzar la construcción de la red, también vamos a realizar un control de calidad de los genes y las muestras.

La función `goodSamplesGenes()` permite identificar genes o muestras que contienen demasiados valores faltantes o que pueden interferir con el análisis de la red.

```r
id="8p4m1c"
# Revisamos la calidad de los genes y las muestras

gsg = goodSamplesGenes(
  input_mat,
  verbose = 3
)

# Revisamos el resultado

gsg$allOK
```

Si `gsg$allOK` devuelve `TRUE`, podemos continuar porque no se identificaron problemas que requieran eliminar genes o muestras.

En caso de que el resultado sea `FALSE`, podemos conservar únicamente los genes y muestras considerados adecuados:

```r
id="t6zj4p"
# Si existen genes o muestras que no cumplen los criterios,
# conservamos únicamente los elementos considerados adecuados

if (!gsg$allOK) {
  input_mat = input_mat[
    gsg$goodSamples,
    gsg$goodGenes
  ]
}
```

Con esto dejamos preparada la matriz que utilizaremos en los siguientes pasos para evaluar la estructura de la red y determinar el valor de potencia que utilizaremos para construirla.

**Paso 10.** Agrupamiento de las muestras y detección de posibles valores atípicos

Antes de construir la red de co-expresión, vamos a revisar la relación entre las muestras mediante un análisis de agrupamiento jerárquico.

La idea es observar si las muestras presentan patrones de expresión similares y detectar posibles muestras que se comporten de manera muy diferente al resto.

```r
# Calculamos la distancia entre las muestras y realizamos
# un agrupamiento jerárquico

sampleTree = hclust(
  dist(input_mat),
  method = "average"
)

# Visualizamos el dendrograma de las muestras

plot(
  sampleTree,
  main = "Agrupamiento de las muestras",
  xlab = "",
  sub = "",
  cex = 0.8
)
```

En el dendrograma, las muestras que presentan perfiles de expresión similares se agrupan en ramas cercanas. Una muestra que se encuentre muy alejada del resto podría considerarse un posible valor atípico (*outlier*).

Este paso es importante porque una muestra atípica puede afectar las correlaciones entre genes y, por lo tanto, la estructura de los módulos que obtendremos posteriormente.

**Paso 11.** Selección del umbral de potencia

Una vez revisada la calidad de las muestras, vamos a determinar el valor de potencia que utilizaremos para construir la red de co-expresión.

En WGCNA, la potencia (*power*) controla la transformación de las correlaciones entre genes en una medida de conectividad. Buscamos un valor que permita aproximarnos a una **topología de red libre de escala**, sin perder excesivamente la conectividad de la red.

Primero definimos un conjunto de valores de potencia que vamos a evaluar.

```r
# Permitimos que WGCNA utilice procesamiento multihilo

allowWGCNAThreads()

# Definimos los valores de potencia que vamos a evaluar

powers = c(
  c(1:10),
  seq(from = 12, to = 20, by = 2)
)
```

Ahora utilizamos `pickSoftThreshold()` para evaluar cómo cambia la topología de la red con cada valor de potencia.

```r
# Evaluamos los diferentes valores de potencia

sft = pickSoftThreshold(
  input_mat,
  powerVector = powers,
  verbose = 5
)
```

Para facilitar la selección de la potencia, vamos a visualizar dos características de la red: el ajuste al modelo de topología libre de escala y la conectividad media.

```r
# Organizamos las dos gráficas en una misma figura

par(mfrow = c(1, 2))

cex1 = 0.9

# Gráfica del ajuste a la topología libre de escala

plot(
  sft$fitIndices[, 1],
  -sign(sft$fitIndices[, 3]) * sft$fitIndices[, 2],
  xlab = "Soft Threshold (power)",
  ylab = "Scale Free Topology Model Fit, signed R^2",
  main = "Scale independence"
)

text(
  sft$fitIndices[, 1],
  -sign(sft$fitIndices[, 3]) * sft$fitIndices[, 2],
  labels = powers,
  cex = cex1,
  col = "red"
)

abline(
  h = 0.90,
  col = "red"
)

# Gráfica de la conectividad media

plot(
  sft$fitIndices[, 1],
  sft$fitIndices[, 5],
  xlab = "Soft Threshold (power)",
  ylab = "Mean Connectivity",
  type = "n",
  main = "Mean connectivity"
)

text(
  sft$fitIndices[, 1],
  sft$fitIndices[, 5],
  labels = powers,
  cex = cex1,
  col = "red"
)
```

La primera gráfica nos permite observar qué valores de potencia producen un mayor ajuste al modelo de topología libre de escala. La segunda muestra cómo disminuye la conectividad media conforme aumenta la potencia.

Para este ejercicio seleccionaremos el valor de potencia **9**, que utilizaremos en la construcción de la red.

```r
# Seleccionamos la potencia que utilizaremos para construir la red

picked_power = 9
```

> **Nota:** La selección de `picked_power` debe realizarse a partir de las gráficas obtenidas para el conjunto de datos que estamos analizando. En este tutorial utilizaremos `9` como valor seleccionado para continuar con el ejercicio.

**Paso 12.** Construcción de la red de co-expresión

Ahora que hemos seleccionado el valor de potencia, podemos construir la red de co-expresión y detectar los módulos de genes que presentan patrones de expresión similares entre las muestras.

Utilizaremos `blockwiseModules()`, que permite construir la red y realizar la identificación de módulos en un mismo procedimiento.

En este caso construiremos una **red firmada** (`signed`), en la que las correlaciones positivas entre genes tienen mayor contribución a la conectividad de la red.

```r
id="p7n5cx"
# Guardamos temporalmente la función cor original

temp_cor <- cor

# Indicamos a WGCNA que utilice su propia función de correlación

cor <- WGCNA::cor

# Construimos la red de co-expresión y detectamos los módulos

netwk <- blockwiseModules(
  input_mat,

  # Parámetros de la red
  power = picked_power,
  networkType = "signed",

  # Parámetros para la detección de módulos
  deepSplit = 2,
  pamRespectsDendro = FALSE,
  minModuleSize = 30,
  maxBlockSize = 4000,

  # Ajuste de los módulos
  reassignThreshold = 0,
  mergeCutHeight = 0.25,

  # Guardamos los archivos TOM para poder reutilizarlos
  saveTOMs = TRUE,
  saveTOMFileBase = "ER",

  # Opciones de salida
  numericLabels = TRUE,
  verbose = 3
)

# Restauramos la función cor original

cor <- temp_cor
```

El parámetro `minModuleSize = 30` establece el número mínimo de genes que puede contener un módulo. Por otro lado, `mergeCutHeight = 0.25` controla el nivel de similitud utilizado para unir módulos cuyos perfiles de expresión son muy parecidos.

Como nuestra matriz contiene más genes que el valor definido en `maxBlockSize`, WGCNA puede dividir el análisis en diferentes bloques. Esto permite trabajar con conjuntos de genes grandes sin requerir que toda la red sea procesada como un único bloque.

Finalmente, vamos a revisar cuántos bloques fueron generados:

```r
id="7x8wqk"
# Revisamos el número de bloques generados

length(netwk$dendrograms)
```

Y podemos consultar cuántos genes fueron asignados a cada bloque:

```r
id="n6k3tp"
# Revisamos el número de genes presentes en cada bloque

sapply(
  netwk$blockGenes,
  length
)
```

El objeto `netwk` contiene ahora la información principal de la red, incluyendo los módulos identificados, los genes asignados a cada módulo y los dendrogramas utilizados para su construcción.

**Paso 13.** Visualización de los módulos identificados

Una vez construida la red, vamos a revisar los módulos que fueron identificados por WGCNA.

Primero convertimos las etiquetas numéricas de los módulos a nombres de colores. Estos colores son utilizados por WGCNA para facilitar la identificación y visualización de cada módulo.

```r
# Convertimos las etiquetas numéricas de los módulos a colores

mergedColors = labels2colors(netwk$colors)

# Revisamos los colores asignados a los genes

table(mergedColors)
```

Ahora podemos visualizar el dendrograma de los genes junto con los módulos identificados.

```r
# Visualizamos el dendrograma y los módulos identificados

plotDendroAndColors(
  netwk$dendrograms[[1]],
  mergedColors[netwk$blockGenes[[1]]],
  "Module colors",
  dendroLabels = FALSE,
  hang = 0.03,
  addGuide = TRUE,
  guideHang = 0.05
)
```

En esta gráfica, cada rama del dendrograma representa genes con perfiles de expresión similares. La barra de colores que aparece debajo permite identificar el módulo al que pertenece cada gen.

También podemos revisar directamente las etiquetas numéricas asignadas por WGCNA:

```r
# Revisamos las etiquetas de los módulos

table(netwk$colors)
```

Finalmente, vamos a generar una tabla que relacione cada gen con el módulo al que fue asignado. Esta tabla será útil para los análisis posteriores y también nos permitirá conservar esta información como resultado del análisis.

```r
# Generamos una tabla con el gen y el módulo al que pertenece

module_df <- data.frame(
  gene_id = names(netwk$colors),
  colors = labels2colors(netwk$colors)
)

# Revisamos las primeras filas

module_df[1:5, ]

# Guardamos la tabla en formato delimitado por tabulaciones

write_delim(
  module_df,
  file = "gene_modules.txt",
  delim = "\t"
)
```

A partir de este punto ya tenemos una relación entre cada gen y el módulo al que pertenece. En los siguientes pasos utilizaremos esta información para caracterizar los módulos y estudiar su relación con las características de las muestras.

**Paso 14.** Cálculo de los módulos eigengenes

Ahora vamos a obtener los **módulos eigengenes** (*Module Eigengenes*, MEs).

El módulo eigengene representa el principal patrón de expresión de los genes que pertenecen a un módulo. Podemos utilizarlo como una medida resumida de la actividad de cada módulo en cada muestra.

Esto será especialmente útil en los siguientes pasos, donde relacionaremos los módulos con los grupos experimentales.

```r
# Calculamos los módulos eigengenes a partir de la matriz de expresión
# y de los colores asignados a cada módulo

MEs0 <- moduleEigengenes(
  input_mat,
  mergedColors
)$eigengenes

# Reordenamos los módulos para colocar juntos aquellos
# que presentan patrones de expresión similares

MEs0 <- orderMEs(MEs0)

# Revisamos los nombres de los módulos

names(MEs0)

# Revisamos una parte de la matriz de módulos eigengenes

MEs0[1:5, 1:10]
```

Cada columna de `MEs0` corresponde a un módulo y cada fila corresponde a una muestra. Los valores representan el patrón de expresión resumido de cada módulo en cada muestra.

Podemos visualizar estos valores para tener una primera idea de cómo se comportan los módulos entre las diferentes muestras.

```r
# Agregamos el nombre de cada muestra

MEs0$treatment = row.names(MEs0)

# Transformamos la tabla a formato largo para facilitar su visualización

mME = MEs0 %>%
  pivot_longer(-treatment) %>%
  mutate(
    name = gsub("ME", "", name)
  )

# Visualizamos los módulos eigengenes

mME %>%
  ggplot(aes(x = treatment, y = name, fill = value)) +
  geom_tile() +
  theme_bw() +
  scale_fill_gradient2(
    low = "blue",
    high = "red",
    mid = "white",
    midpoint = 0
  ) +
  theme(
    axis.text.x = element_text(angle = 90)
  ) +
  labs(
    title = "Módulos eigengenes",
    x = "Muestras",
    y = "Módulos",
    fill = "Expresión"
  )
```

Esta gráfica nos permite observar de manera general los patrones de expresión de los módulos entre las muestras.

> **Importante:** esta gráfica muestra los valores de los módulos eigengenes. No representa todavía una relación estadística entre los módulos y los tratamientos. La relación **módulo–rasgo** se calculará en el siguiente paso.


**Paso 15.** Relación entre los módulos y los grupos experimentales

Ahora vamos a relacionar los módulos eigengenes con los grupos experimentales de las muestras.

Hasta este momento hemos observado el comportamiento de los módulos, pero todavía no hemos evaluado estadísticamente si alguno de ellos presenta una asociación con un grupo experimental determinado.

Para realizar esta comparación necesitamos convertir la información de los grupos en una matriz numérica. Utilizaremos una variable binaria para cada grupo experimental.

```r
# Generamos una tabla con la información de los grupos experimentales

trait_data <- data.frame(
  Type = meta_df$Type,
  row.names = meta_df$Sample
)

# Convertimos los grupos experimentales en variables binarias

trait_matrix <- model.matrix(
  ~ 0 + Type,
  data = trait_data
)

# Eliminamos el prefijo Type de los nombres de las columnas

colnames(trait_matrix) <- gsub(
  "^Type",
  "",
  colnames(trait_matrix)
)

# Revisamos la matriz de grupos experimentales

trait_matrix
```

Ahora vamos a calcular la correlación entre los módulos eigengenes y cada uno de los grupos experimentales.

```r
# Calculamos la correlación entre los módulos y los grupos experimentales

moduleTraitCor <- cor(
  MEs0[, !names(MEs0) %in% "treatment"],
  trait_matrix,
  use = "p"
)

# Calculamos los valores de significancia de las correlaciones

moduleTraitPvalue <- corPvalueStudent(
  moduleTraitCor,
  nSamples = nrow(input_mat)
)

# Revisamos las correlaciones

moduleTraitCor
```

Para facilitar la interpretación, vamos a representar las correlaciones mediante un mapa de calor. En cada celda mostraremos el valor de correlación y su valor de significancia.

```r
# Generamos una matriz de texto con la correlación y el valor de P

textMatrix <- paste(
  signif(moduleTraitCor, 2),
  "\n(",
  signif(moduleTraitPvalue, 1),
  ")",
  sep = ""
)

dim(textMatrix) <- dim(moduleTraitCor)

# Visualizamos la relación módulo-tratamiento

labeledHeatmap(
  Matrix = moduleTraitCor,
  xLabels = colnames(trait_matrix),
  yLabels = names(MEs0)[names(MEs0) != "treatment"],
  ySymbols = names(MEs0)[names(MEs0) != "treatment"],
  colorLabels = FALSE,
  colors = blueWhiteRed(50),
  textMatrix = textMatrix,
  setStdMargins = FALSE,
  cex.text = 0.7,
  zlim = c(-1, 1),
  main = "Relación módulo-tratamiento"
)
```

En esta gráfica, cada fila representa un módulo y cada columna un grupo experimental. Los valores positivos indican una asociación positiva entre el módulo y el grupo, mientras que los valores negativos indican una asociación negativa.

El valor de `P` nos permite evaluar la significancia estadística de cada correlación. Sin embargo, la interpretación biológica no debe basarse únicamente en el valor de `P`; también debemos considerar la magnitud de la correlación y el contexto experimental.

Esta información nos permitirá identificar los módulos que presentan los patrones de expresión más relacionados con los grupos que estamos estudiando.

**Paso 16.** Identificación de genes relacionados con los módulos

Ahora que hemos identificado los módulos que presentan una asociación con los grupos experimentales, podemos analizar con mayor detalle los genes que forman parte de cada módulo.

Para esto calcularemos la **membresía del módulo** (*Module Membership*, MM), que corresponde a la correlación entre la expresión de cada gen y el módulo eigengene correspondiente.

Un valor alto de MM indica que el patrón de expresión de un gen se encuentra estrechamente relacionado con el comportamiento general de su módulo.

```r
id="8qv3na"
# Calculamos la correlación entre cada gen y los módulos eigengenes

geneModuleMembership = as.data.frame(
  cor(
    input_mat,
    MEs0[, !names(MEs0) %in% "treatment"],
    use = "p"
  )
)

# Calculamos los valores de significancia de las correlaciones

MMPvalue = as.data.frame(
  corPvalueStudent(
    as.matrix(geneModuleMembership),
    nSamples = nrow(input_mat)
  )
)

# Revisamos los primeros resultados

geneModuleMembership[1:5, 1:5]
```

Ahora podemos agregar los nombres de los módulos a partir de la información que obtuvimos anteriormente.

```r
id="x9y7pw"
# Revisamos los nombres de las columnas

names(geneModuleMembership)
```

Para facilitar el análisis, vamos a utilizar la información de `module_df` para identificar qué módulo corresponde a cada gen.

```r
id="e8n4jc"
# Revisamos la asignación de los genes a los módulos

module_df[1:5, ]
```

La membresía del módulo será especialmente útil cuando queramos seleccionar genes representativos de un módulo. Los genes con valores altos de MM son candidatos para representar de manera adecuada el patrón de expresión del módulo y pueden ser considerados posteriormente en la identificación de genes centrales (*hub genes*).

En el siguiente paso utilizaremos esta información para explorar con mayor detalle uno de los módulos de interés.

**Paso 17.** Identificación de genes centrales de un módulo

Ahora vamos a utilizar la información de membresía del módulo para identificar los genes que presentan una mayor asociación con un módulo de interés.

Para este ejercicio seleccionaremos algunos módulos como ejemplo. Puedes modificar esta lista de acuerdo con los resultados obtenidos en el paso anterior.

```r
# Seleccionamos los módulos que queremos explorar

modules_of_interest = c(
  "green",
  "turquoise",
  "tan"
)

# Seleccionamos los genes que pertenecen a estos módulos

genes_of_interest = module_df %>%
  subset(colors %in% modules_of_interest)

# Revisamos cuántos genes contiene cada módulo

table(genes_of_interest$colors)
```

Ahora podemos calcular la membresía de los genes dentro de cada módulo y ordenar los genes de acuerdo con su valor de MM.

```r
# Revisamos los genes pertenecientes al módulo green

module = "green"

# Identificamos los genes que pertenecen al módulo seleccionado

inModule = module_df$colors == module

# Seleccionamos la columna correspondiente al módulo eigengene

column = match(
  paste0("ME", module),
  colnames(geneModuleMembership)
)

# Extraemos la membresía de los genes del módulo

module_membership = geneModuleMembership[
  inModule,
  column,
  drop = FALSE
]

# Ordenamos los genes de acuerdo con su membresía al módulo

module_membership = module_membership[
  order(
    abs(module_membership[, 1]),
    decreasing = TRUE
  ),
  ,
  drop = FALSE
]

# Mostramos los primeros genes

head(module_membership, 10)
```

Los genes que presentan valores elevados de MM son los que tienen una mayor similitud con el patrón de expresión general del módulo. Estos genes pueden utilizarse como candidatos para representar el comportamiento del módulo.

Podemos obtener directamente los identificadores de los genes con mayor membresía:

```r
# Seleccionamos los 10 genes con mayor membresía al módulo

hub_genes = row.names(module_membership)[1:10]

# Revisamos los genes seleccionados

hub_genes
```

> **Nota:** En este punto estamos utilizando `MM` como criterio para identificar genes centrales del módulo. Esto no significa necesariamente que estos genes tengan una función biológica central. Para una interpretación más completa, la selección de genes candidatos puede complementarse con su relación con el rasgo de interés, expresión diferencial, anotación funcional y otras evidencias biológicas.

**Paso 18.** Relación entre la MM y el grupo experimental

Ahora vamos a complementar el análisis anterior relacionando la **membresía del módulo (MM)** con la asociación de cada gen con un grupo experimental.

Para esto calcularemos la **significancia del gen respecto al rasgo** (*Gene Significance*, GS). En este ejemplo utilizaremos el grupo `green` como referencia.

```r
# Seleccionamos el grupo experimental que queremos analizar

trait_of_interest = "green"

# Calculamos la asociación de cada gen con el grupo seleccionado

geneTraitSignificance = as.data.frame(
  cor(
    input_mat,
    trait_matrix[, trait_of_interest],
    use = "p"
  )
)

# Calculamos los valores de significancia

GSPvalue = as.data.frame(
  corPvalueStudent(
    as.matrix(geneTraitSignificance),
    nSamples = nrow(input_mat)
  )
)

# Revisamos los primeros resultados

geneTraitSignificance[1:5, ]
```

Ahora podemos comparar la membresía de los genes al módulo con su asociación con el grupo experimental.

```r
# Extraemos la membresía de los genes al módulo green

MM_green = geneModuleMembership[
  ,
  match("MEgreen", colnames(geneModuleMembership))
]

# Extraemos la significancia de los genes respecto al grupo seleccionado

GS_green = geneTraitSignificance[, 1]

# Generamos la gráfica MM-GS

plot(
  abs(MM_green),
  abs(GS_green),
  xlab = "Membresía al módulo |MM|",
  ylab = "Significancia del gen |GS|",
  main = "Membresía del módulo vs. significancia del gen",
  pch = 19
)
```

En esta gráfica, cada punto representa un gen. La relación entre `MM` y `GS` nos permite observar si los genes que están más estrechamente relacionados con el patrón general del módulo también presentan una mayor asociación con el grupo experimental.

Una relación positiva entre ambas medidas puede ser útil para seleccionar genes candidatos dentro de un módulo de interés. Sin embargo, nuevamente debemos considerar que estas asociaciones son estadísticas y no demuestran por sí mismas una función biológica.


**Paso 19.** Construcción y exportación de la red de co-expresión

Ahora vamos a generar una red de co-expresión a partir de los módulos que seleccionamos como de interés.

Para este análisis utilizaremos la **TOM (Topological Overlap Matrix)**, que permite evaluar qué tan conectados están entre sí los genes considerando no solamente su correlación directa, sino también las conexiones que comparten con otros genes de la red.

Primero extraemos de la matriz de expresión los genes pertenecientes a los módulos que seleccionamos anteriormente.

```r
id="4f8q2m"
# Extraemos los genes pertenecientes a los módulos de interés

expr_of_interest = expr_normalized[
  genes_of_interest$gene_id,
]

# Revisamos una parte de la matriz

expr_of_interest[1:5, 1:5]
```

Ahora calculamos la matriz de similitud topológica para estos genes.

```r
id="z7c1pa"
# Calculamos la matriz de similitud topológica

TOM = TOMsimilarityFromExpr(
  t(expr_of_interest),
  power = picked_power
)

# Agregamos los identificadores de los genes
# a las filas y columnas de la matriz

row.names(TOM) = row.names(expr_of_interest)
colnames(TOM) = row.names(expr_of_interest)
```

La matriz `TOM` contiene la similitud topológica entre cada par de genes. Para facilitar su utilización en otros programas, vamos a convertirla en una lista de interacciones entre genes.

```r
id="2p9m6k"
# Convertimos la matriz TOM en una tabla de interacciones

edge_list = data.frame(TOM) %>%
  mutate(
    gene1 = row.names(.)
  ) %>%
  pivot_longer(
    -gene1
  ) %>%
  dplyr::rename(
    gene2 = name,
    correlation = value
  ) %>%
  unique() %>%
  subset(
    !(gene1 == gene2)
  ) %>%
  mutate(
    module1 = module_df[gene1, ]$colors,
    module2 = module_df[gene2, ]$colors
  )

# Revisamos las primeras interacciones

head(edge_list)
```

Finalmente, guardamos la lista de interacciones en un archivo delimitado por tabulaciones.

```r
id="5j3r8c"
# Exportamos la red para utilizarla posteriormente
# en programas como Cytoscape o VisANT

write_delim(
  edge_list,
  file = "edgelist.tsv",
  delim = "\t"
)
```

El archivo `edgelist.tsv` contiene las relaciones entre los genes seleccionados y puede utilizarse como entrada para realizar una visualización más detallada de la red en programas especializados.

> **Nota:** En este ejemplo estamos exportando las interacciones de los módulos seleccionados. En una red grande, la cantidad de interacciones puede aumentar considerablemente, por lo que posteriormente podemos aplicar un umbral de similitud TOM para conservar únicamente las conexiones más relevantes.

**Conclusiones.**

En este tutorial partimos de una matriz de conteos de RNA-Seq y seguimos un flujo de trabajo para construir una red de co-expresión utilizando WGCNA.

Durante el análisis realizamos los siguientes procedimientos:

* Exploramos la matriz de conteos y la distribución de las muestras.
* Normalizamos y transformamos los datos mediante DESeq2.
* Seleccionamos los genes con mayor variabilidad.
* Revisamos la calidad y el agrupamiento de las muestras.
* Determinamos un valor de potencia para la construcción de la red.
* Identificamos módulos de genes con patrones de expresión similares.
* Calculamos los módulos eigengenes.
* Evaluamos la relación entre los módulos y los grupos experimentales.
* Calculamos la MM de los genes dentro de los módulos.
* Identificamos genes hub.
* Construimos y exportamos una red de interacciones basada en la similitud topológica.

El objetivo de este análisis no es únicamente obtener grupos de genes, sino utilizar los patrones de co-expresión para explorar posibles relaciones entre los genes y las características biológicas de interés.

Los módulos identificados pueden utilizarse como punto de partida para análisis posteriores, como enriquecimiento funcional, identificación de genes candidatos, análisis de redes y visualización en herramientas como Cytoscape.

Finalmente, es importante considerar que las relaciones obtenidas mediante WGCNA representan **asociaciones de co-expresión**. Por sí mismas, estas asociaciones no demuestran relaciones causales ni funciones biológicas. Su interpretación debe complementarse con información experimental, funcional y biológica.

---

## <span id="practica-07"> Práctica07: Otros ncRNAs (Rfam) y Elementos Transponibles </span>

Complementando la búsqueda de lncRNAs del ejercicio anterior, esta práctica aborda dos tipos adicionales de elementos genómicos no codificantes: primero, otros RNAs no codificantes de menor tamaño (rRNAs, tRNAs, snRNAs, precursores de miRNAs, etc.) mediante comparación contra la base de datos Rfam; y segundo, los elementos transponibles (TEs), cuya identificación y enmascaramiento es relevante tanto por sí misma como para mejorar predicciones génicas posteriores.

### 2.1 Identificación de ncRNAs con Rfam/Infernal

**Ejercicio 01.** Asumamos que tenemos la secuencia parcial o completa de un genoma (`PartialGenome.fasta`) y que en esta deseamos identificar aquellos genes/loci cuyos transcritos corresponden a RNAs no codificantes (p. ej. RNAs ribosomales, RNAs de transferencia, RNAs nucleares, precursores de miRNAs, etc.). Para dicho propósito se comparará el genoma de interés contra la base de datos [Rfam](https://rfam.xfam.org/). Este comparativo lo realiza el programa `infernal` utilizando modelos ocultos de Markov, es decir, compara las secuencias mediante el modelado de procesos estocásticos donde la ocurrencia está asociada a la distribución de la probabilidad.

Revise las opciones a utilizar en el script `Rfam.slurm` (tiempo aproximado: 15 min) y analice el resultado.

**Script `Rfam.slurm`:**

```bash
#!/bin/sh
#SBATCH -J Rfam
#SBATCH -n 10
#SBATCH -N 1
#SBATCH --mem 75000
#SBATCH -o Rfam.o%j
#SBATCH -e Rfam.e%j
#SBATCH -p q1
#SBATCH -w nodo3

module load infernal/1.1.2/gcc/8.3.1-mnuk

time cmscan --cpu 10 --cut_ga --rfam --nohmmonly --tblout RfamResult.tblout --fmt 2 --clanin /tmp/databases/Rfam/Rfam.clanin /tmp/databases/Rfam/Rfam.cm PartialGenome.fasta > RfamResult.cmscan
```

**Ejercicio 02.** Una vez obtenido el resultado, "parsea" el archivo `*.tblout` para seleccionar únicamente los RNAs de transferencia (tRNA):

```bash
grep "tRNA" RfamResult.tblout > tRNAs.tblout
```

Utilizando las coordenadas de alguno de los loci, extrae la secuencia correspondiente al mismo. Para dicho propósito utiliza el programa `extractseq` de la paquetería de EMBOSS:

```bash
module load emboss/6.6.0/gcc/8.3.1-7aag
```

```bash
srun --mem 8G -n1 -p q2 extractseq -sequence PartialGenome.fasta -outseq tRNAs.fasta -regions "2354324..2354396 8322791..8322874" -separate
```

Para visualizar (solo si lo considera necesario) puede utilizar el siguiente servidor en línea: [RNAfold WebSuite](http://rna.tbi.univie.ac.at/cgi-bin/RNAWebSuite/RNAfold.cgi)

### 2.2 Elementos Transponibles: estructura con LTR_Finder y enmascaramiento con RepeatMasker

El archivo `DeNovoTEs.fasta` es un archivo multifasta que contiene elementos transponibles que fueron identificados y categorizados con el programa REPET. Tenga en cuenta que dicho programa (REPET) no es el único comúnmente utilizado para identificar/predecir elementos transponibles (TEs) de novo; otras opciones igualmente eficientes son los programas RepeatModeler o RepBox. El funcionamiento de ninguno de estos programas se mostrará durante el curso, pero trabajaremos con el archivo resultante de uno de ellos.

Asumiendo que, en su mayoría, los elementos contenidos en el archivo `DeNovoTEs.fasta` son retrotransposones, vamos a utilizar el programa [ltr_finder](https://github.com/xzhub/LTR_Finder) para analizar su estructura. Tanto el programa (un ejecutable) como los tRNAs a utilizar se encuentran en el directorio `LTR_FINDER.x86_64-1.0.5`. Estos últimos (los tRNAs) fueron identificados previamente, como se vio en prácticas anteriores, y se proporcionan en un archivo multifasta.

Revise las opciones, en especial con relación al tipo de formato de(los) archivo(s) de salida:

```bash
srun --mem 8G -n1 -p q1 ./ltr_finder -s Plant-tRNAs.fa -w 0 -x -E ../DeNovoTEs.fasta > LTRfinder_Results
```

Ahora, una vez confirmada la presencia de retrotransposones y otros elementos transponibles en nuestro archivo `DeNovoTEs.fasta`, "enmascaremos" las regiones correspondientes utilizando el programa **RepeatMasker**.

En el directorio `RepeatMasker`, utilice el siguiente script de Slurm para tal propósito. Antes de ejecutarlo, corrija y cambie las opciones en caso necesario.

**Script `RepeatMasker.slurm`:**

```bash
#!/bin/bash
#SBATCH -J RepeatMasker
#SBATCH -n 1
#SBATCH --mem 16G
#SBATCH -t 0
#SBATCH -e RepMask.e%j
#SBATCH -o RepMask.o%j
#SBATCH -p q1

module load repeatmasker/4.0.6/gcc/9.3.0-mw7b

RepeatMasker -q -x -gff -lib ../DeNovoTEs.fasta GenomeSequences.fasta
```
Una vez enmascarado el genoma, realice la predicción de modelos génicos utilizando evidencia transcripcional (`TranscriptomeAssembly.fasta`), tal y como se hizo en la Práctica05 (Ejercicio02). Utilice tanto el genoma enmascarado como el genoma sin enmascarar. Una vez parseados sus resultados, transfiera los archivos necesarios a su máquina local y compare utilizando JBrowse.

---

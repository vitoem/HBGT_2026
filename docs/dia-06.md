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
[← Volver a la portada](./)


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

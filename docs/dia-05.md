---
layout: default
title: "Día 05 · Evaluación y anotación de genomas"
---

<span class="eyebrow">Miércoles · 23 septiembre</span>

## 🏷️ Día 5: Anotación de Genomas, Métodos y Bases de Datos

Bienvenid@s a la página de recursos del **Día 5** del curso **"Herramientas Bioinformáticas para el Análisis de Genomas y Transcriptomas"**. En esta jornada nos enfocaremos en descifrar el significado biológico de las secuencias ensambladas: el proceso de **Anotación de Genomas**. Aprenderemos a identificar estructuralmente los genes y otros elementos funcionales, a predecir sus funciones biológicas mediante homología y modelos estadísticos, y a utilizar las bases de datos de referencia más importantes de la disciplina.

---

### Teoría: Fundamentos y Métodos de Anotación de Genomas

Una vez que un genoma ha sido ensamblado de la manera más completa y menos fragmentada posible, la pregunta biológica fundamental que surge es: **¿cuál es la información codificada en esa secuencia de nucleótidos?** La **Anotación** es el proceso a través del cual se lleva a cabo la identificación de los elementos que componen a los genomas (*features*) mediante la búsqueda de patrones particulares codificados en el ADN, permitiéndonos entender la función y evolución de los organismos.

```
                  GENOMA ENSAMBLADO (Secuencia de ADN)
                                   │
                      ┌────────────┴────────────┐
                      ▼                         ▼
            Anotación Estructural     Anotación Funcional
             (¿Dónde están los          (¿Qué hacen los
                 elementos?)               elementos?)
                      │                         │
         ┌────────────┴────────────┐            ├────────────────────────┐
         ▼                         ▼            ▼                        ▼
    Ab Initio                 Homología     Ontologías (GO)       Rutas (KEGG)
(Modelos HMM)              (Alineamientos)  Dominios (InterPro)   Dominios (CDD)
```

---

### 1. Prerrequisitos para iniciar la Anotación
Para garantizar el éxito de un pipeline de anotación, se requiere contar con tres pilares de información:
1.  **Genoma ensamblado de alta calidad:** Debe estar lo más completo posible y con el menor nivel de fragmentación molecular.
2.  **Información intrínseca:** Modelos de predicción estadística calibrados para el taxón de interés.
3.  **Información extrínseca:** Datos experimentales de soporte, tales como evidencia transcripcional de la misma especie (datos de RNA-seq o transcriptomas *de novo*) y bases de datos de proteínas de especies filogenéticamente cercanas.

---

### 2. Anotación Estructural: Identificación de Elementos (Features)
La anotación estructural consiste en identificar físicamente la ubicación y coordenadas de los componentes biológicos sobre el andamio genómico. Estos componentes incluyen:

*   **Genes codificantes de proteínas:** Identificación de exones, intrones y regiones no traducidas (UTRs).
*   **Elementos reguladores del ADN:** Mapeo de promotores, potenciadores (*enhancers*), silenciadores y sitios de unión a factores de transcripción.
*   **Genes de ARN no codificante (ncRNA):** Localización de ARN ribosomal (rRNA), ARN de transferencia (tRNA), microARNs (miRNA), ARN nuclear pequeño (snRNA), ARN nucleolar pequeño (snoRNA) y ARNs no codificantes largos (lncRNA).
*   **Pseudogenes:** Copias de genes que han perdido su capacidad funcional debido a mutaciones acumuladas.
*   **Elementos transponibles:** Transposones y secuencias repetitivas acumuladas evolutivamente.

En organismos eucariotas, la predicción de genes codificantes es un reto computacional sumamente complejo debido al tamaño variable de los intrones y a la presencia de variantes en el procesamiento alternativo (*splicing*).

---

### 3. Estrategias y Algoritmos de Anotación Estructural

#### A) Enmascaramiento de Repetidos (Repeat Masking)
Es la labor inicial de todo proceso de anotación. Consiste en identificar y enmascarar computacionalmente (reemplazando temporalmente por letras `N` o minúsculas `a, t, g, c`) los elementos transponibles y regiones altamente repetitivas. Esto evita que los algoritmos de predicción génica alineen erróneamente lecturas codificantes sobre elementos móviles redundantes, agilizando drásticamente la computación.

#### B) Aproximaciones Comparativas (Homología)
Este método se basa en alinear secuencias de ADN complementario (cDNA), etiquetas de secuencia expresadas (ESTs) o evidencia de proteínas de especies emparentadas contra el genoma ensamblado mediante alineamientos con huecos (*Gapped Alignments*) utilizando herramientas como **BLAT** o **HiSat2**.
*   **Premisa:** Asume que regiones con alta similitud de secuencia son potencialmente homólogas.
*   **Limitación:** Entre mayor sea la distancia genética de la especie en estudio con respecto a los organismos de referencia en las bases de datos, menor será la precisión y efectividad de la predicción.

#### C) Aproximaciones Estadísticas (Ab Initio)
Se sustenta en el uso de modelos estadísticos entrenados para reconocer señales biológicas en la secuencia de nucleótidos (sitios de splicing dadores y aceptores, codones de inicio y paro, cajas promotoras, etc.).
*   **Modelos de Markov Ocultos (Hidden Markov Models - HMM):** Son modelos probabilísticos basados en un número de estados estructurados bajo un sentido biológico (intrón, exón, UTR-5', etc.). La probabilidad de transición entre estos estados se define a partir de un **set de entrenamiento de genes previamente curados y anotados** para el taxón correspondiente.

| Programa | Aplicación y Algoritmo Principal |
| :--- | :--- |
| **AUGUSTUS** | Predicciones de genes eucariotas basadas en modelos HMM avanzados y soporte de evidencia extrínseca. |
| **GeneMark** | Modelos ab initio auto-entrenables de amplio uso en genomas procariotas, metagenomas y eucariotas. |
| **GlimmerHMM** | Buscador de genes eucariotas basado en árboles de interpolación de Markov generalizados. |
| **tRNAscan-SE** | Identificación de alta precisión de genes de ARN de transferencia (tRNA) utilizando modelos de covarianza. |
| **SNAP** | Predictor de genes ab initio adaptable tanto para genomas procariotas como eucariotas. |

---

### 4. Bases de Datos para la Anotación Estructural por Homología
*   **SRA (Sequence Read Archive):** Repositorio universal para almacenar los datos crudos de secuenciación de transcriptomas (RNA-seq) que sirven como soporte de alineamiento.
*   **Bases de datos especializadas por elemento:**
    *   *RNA no codificante:* **NONCODE** y **miRBase** (específica para miRNAs).
    *   *Pseudogenes:* **Pseudogene.org**.
    *   *Elementos Transponibles:* **Dfam** (colección de modelos de perfil HMM de familias de elementos repetidos).

---

## 🔍 Teoría: Anotación Funcional de Genomas

La anotación funcional consiste en **asociar información biológica real** (bioquímica, fisiológica y celular) a las estructuras génicas predichas durante la fase estructural.

### 1. El Principio de Transferencia de Función por Homología
La aproximación estándar asume que **la función biológica se retiene y conserva entre secuencias que provienen de un ancestro común** (homología). Por tanto, la función se transfiere mediante alineamientos de tipo **BLAST** contra bases de datos curadas.

*   **Límites de Confianza:** El punto de corte de significancia estadística (E-value) y porcentaje de identidad se define habitualmente de forma arbitraria.
*   **Propagación de Errores:** Si un gen fue anotado de manera errónea en una base de datos pública de referencia, ese error funcional se heredará y propagará exponencialmente a todos los genomas secuenciados posteriormente.
*   **Transferencia Excesiva:** Existe un alto riesgo de transferir funciones de forma errónea debido a similitudes locales de dominios no relacionados con la función global del gen.
*   **El Reto de la Certeza:** La única manera científica de tener certeza absoluta sobre la anotación funcional de un elemento genético es a través de su **comprobación experimental en laboratorio**.

---

### 2. Bases de Datos Clave para la Anotación Funcional

#### A) Gene Ontology (GO)
Es un consorcio internacional que estandariza la representación de los atributos de los productos génicos a lo largo de las especies utilizando tres ontologías estructuradas (independientes del taxón):
1.  **Función Molecular:** Actividades bioquímicas a nivel molecular (p. ej., actividad catalítica de quinasa o unión a ligando).
2.  **Componente Celular:** Lugares físicos y complejos macromoleculares dentro de la célula donde el producto actúa (p. ej., mitocondria o membrana plasmática).
3.  **Proceso Biológico:** El objetivo o serie de eventos biológicos coordinados a los que contribuye el gen (p. ej., transducción de señales o respuesta a choque térmico).

#### B) KEGG (Kyoto Encyclopedia of Genes and Genomes)
Es una base de datos de referencia en biología de sistemas diseñada para integrar información genómica con funciones biológicas de alto nivel, mapeando interacciones moleculares, reacciones enzimáticas y redes de relación metabólica celulares en diagramas de rutas bioquímicas (*pathways*).

#### C) Consorcio InterPro / InterProScan
Consorcio bioinformático del EMBL-EBI que unifica la información de múltiples bases de datos líderes especializadas en familias de proteínas, dominios conservados, sitios activos y regiones firmas moleculares bajo una sola plataforma de búsqueda.

*   **Bases de Datos Integradas en InterPro:**
    *   **Conserved Domains Database (CDD):** Repositorio del NCBI altamente curado de modelos de dominios conservados 3D.
    *   **Pfam:** Modelos de HMM que agrupan familias de dominios proteicos comunes.
    *   **PROSITE:** Perfiles de firmas químicas y patrones específicos de sitios activos de enzimas.
    *   **PANTHER, SMART, HAMAP, TIGRFAST, SUPERFAMILY, SFLD, PIRSF.**
*   **InterProScan:** Herramienta de software que permite escanear secuencias de nucleótidos o aminoácidos contra todos los modelos de firmas moleculares del consorcio InterPro en una sola corrida.

---

## Prácticas 03–05 — Evaluación, Anotación y Predicción de Genes

Estas tres prácticas continúan el flujo de trabajo iniciado en la Práctica02 (ensamblado de genomas con Newbler y MIRA). Una vez que se cuenta con un ensamblado, es necesario **evaluar su calidad** (Práctica03), **anotarlo** para identificar sus elementos funcionales (Práctica04) y, finalmente, realizar una **predicción de modelos génicos** más detallada sobre la secuencia genómica (Práctica05).

---

## Ejercicio 1 — Práctica03: Métricas de ensamblado y evaluación con BUSCO

Antes de anotar o utilizar un genoma ensamblado, es indispensable evaluar qué tan completo y contiguo resultó el ensamblado. Para ello se utilizarán dos aproximaciones complementarias: el cálculo de métricas de contigüidad (N50, número de contigs, tamaño total, etc.) y la evaluación de completitud génica con BUSCO.

### 1.1 Métricas de ensamblado

En esta práctica utilizaremos un script de perl ([assemblathon_stats.pl](https://github.com/KorfLab/Assemblathon/blob/master/assemblathon_stats.pl)) para calcular diversas métricas de dos genomas bacterianos.

**Paso 1.** Primero intentaremos correr el script con uno de los dos genomas:

```bash
srun --mem 8G -n1 -p q1 ./assemblathon_stats.pl Acidobacteria_bacterium.fna > ACBA_stats.txt
```

Los mensajes indican que el script requiere definir, antes de su ejecución, dos variables de entorno, sin las cuales se generan alertas y errores:

```bash
export PERL5LIB=$(pwd)
export LC_ALL=en_US.UTF-8
```

Una vez que el entorno de trabajo se ha configurado correctamente, se puede ejecutar el script:

```bash
srun --mem 8G -n1 -p q1 ./assemblathon_stats.pl Acidobacteria_bacterium.fna > ACBA_stats.txt
srun --mem 8G -n1 -p q1 ./assemblathon_stats.pl Borrelia_coriaceae.fna > BOCO_stats.txt
```

### 1.2 Evaluación de completitud con BUSCO

Complementando las métricas de contigüidad, BUSCO permite estimar qué tan "completo" está un ensamblado con base en la presencia de genes de copia única altamente conservados en el linaje correspondiente (en este caso, `bacteria_odb9`).

**Script `busco.slurm`:**

```bash
#!/bin/sh
#SBATCH -J busco
#SBATCH -n 1
#SBATCH --mem 16G
#SBATCH -t 0
#SBATCH -e err.%j.log
#SBATCH -o out.%j.log
#SBATCH -p q1
#SBATCH -w nodo3

module load busco/3.0.1/gcc/8.3.1-v6qn

# Si no existe el directorio de configuración, entonces:

if [[ ! -d config ]]
   then
        cp -r /lustre/apps/spack/opt/spack/linux-centos8-skylake_avx512/gcc-8.3.1/augustus-3.3.2-umjiaocposxtv2vs3ld7qaonaplsuxcy/config .
fi

MAIN_DIR=$(pwd)
export AUGUSTUS_CONFIG_PATH=${MAIN_DIR}/config

# Ejecutar BUSCO con los dos genomas bacterianos y comparar los resultados para determinar cuál está más completo.

run_BUSCO.py -m genome -i Acidobacteria_bacterium.fna -o ACBA -l bacteria_odb9 -c 1

run_BUSCO.py -m genome -i Borrelia_coriaceae.fna -o BOCO -l bacteria_odb9 -c 1
```

Compare los resultados de BUSCO entre ambos genomas (Acidobacteria_bacterium y Borrelia_coriaceae) y relaciónelos con las métricas de contigüidad obtenidas en el punto anterior para determinar cuál ensamblado es de mejor calidad.

---

## Ejercicio 2 — Práctica04: Anotación de genomas procariontes con herramientas en línea

Una vez evaluada la calidad del ensamblado, el siguiente paso es anotarlo, es decir, identificar genes y otros elementos funcionales sobre la secuencia. Para genomas procariontes (principalmente bacterianos) es común apoyarse en servidores en línea que agilizan considerablemente este proceso frente a instalar y configurar un pipeline completo de forma local.

Para llevar a cabo este ejercicio utilizaremos un par de servidores en línea, ambos herramientas rápidas y eficientes que ayudan a minimizar significativamente los tiempos cuando se trabaja con genomas procariontes: **DFAST** y **Prokka/Proksee**.

- DFAST: [https://dfast.ddbj.nig.ac.jp/](https://dfast.ddbj.nig.ac.jp/) — referencia: [https://academic.oup.com/bioinformatics/article/34/6/1037/4587587](https://academic.oup.com/bioinformatics/article/34/6/1037/4587587)
- Prokka/Proksee: [https://proksee.ca/](https://proksee.ca/) — referencia: [https://academic.oup.com/bioinformatics/article/30/14/2068/2390517](https://academic.oup.com/bioinformatics/article/30/14/2068/2390517)

Anotaremos el genoma ensamblado con MIRA en la Práctica02. Para tal objeto, importe a su máquina local el archivo resultante del proceso de ensamblado:

```bash
rsync -av --progress --bwlimit=20000 -e 'ssh -p PORT' usuario@IP:PATH/TO/archivo.fasta .
```

Una vez transferido el archivo, cárguelo en ambas plataformas (DFAST y Prokka/Proksee), compare los resultados de anotación obtenidos por cada una y discuta las diferencias.

---

## Ejercicio 3 — Práctica05: Predicción de modelos génicos con Augustus

Con el genoma ya evaluado y anotado a nivel general, esta práctica se enfoca en la predicción de modelos génicos utilizando **Augustus**, primero de forma *ab initio* (sin evidencia externa) y después refinando la predicción con evidencia transcripcional (un transcriptoma ensamblado).

### 3.1 Predicción ab initio (Ejercicio01)

En la medida de lo posible, instale en su equipo local el programa JBrowse para la visualización de resultados. Para su descarga, utilice el siguiente enlace: [https://jbrowse.org/jb2/download/](https://jbrowse.org/jb2/download/)

Una vez instalado, comencemos con el ejercicio. Se utilizará el programa "augustus" para llevar a cabo la predicción de modelos génicos en el genoma (GenomeSequence.fasta).

Si bien se proporciona un script que puede ser gestionado por Slurm, es fundamental revisar la ayuda del programa augustus y modificar el script según las instrucciones. Se generarán inicialmente dos predicciones ab initio: la primera evitando identificar posibles isoformas, y la segunda incluyéndolas.

**Script `Augustus.slurm`:**

```bash
#!/bin/bash
#SBATCH -J Augustus
#SBATCH -n 1
#SBATCH --mem 25G
#SBATCH -t 0
#SBATCH -p q1
#SBATCH -e Augustus.e%j
#SBATCH -o Augustus.o%j

module load augustus/3.4.0/gcc/9.3.0-chpq 

augustus --species=tomato --strand=both --alternatives-from-sampling=false --UTR=off --uniqueGeneId=true --codingseq=true --gff3=on GenomeSequence.fasta > AbInitioGeneModelsNoIsoforms_v1.0.gff

augustus --species=tomato --strand=both --alternatives-from-sampling=true --UTR=off --uniqueGeneId=true --codingseq=true --gff3=on GenomeSequence.fasta > AbInitioGeneModelsIsoforms_v1.0.gff
```

A partir de al menos uno de los archivos de salida (formato gff extendido), extraiga tanto las secuencias codificantes (CDS) como sus correspondientes proteínas traducidas. Utilice el siguiente script para tal propósito (asegúrese de tener cargado el módulo correspondiente):

```bash
srun --mem 16000 -n1 -p q1 getAnnoFasta.pl AbInitioGeneModelsNoIsoforms_v1.0.gff
```

Una vez obtenido el(los) resultado(s) (archivos gff), será importante "parsear" el resultado para eliminar comentarios en los archivos resultantes. Puede utilizar las siguientes líneas de comando para tal propósito:

```bash
grep -v "#" AbInitioGeneModelsNoIsoforms_v1.0.gff > AbInitioGeneModelsNoIsoforms_v1.1.gff
grep -v "#" AbInitioGeneModelsIsoforms_v1.0.gff > AbInitioGeneModelsIsoforms_v1.1.gff
```

Transfiera los siguientes archivos a su equipo local: `GenomeSequence.fasta`, `AbInitioGeneModels*_v1.1.gff`. Utilice JBrowse para analizar el resultado, identifique las diferencias y discútalas.

### 3.2 Predicción refinada con evidencia transcripcional (Ejercicio02)

Repetiremos el Ejercicio01, es decir, se llevará a cabo una predicción de modelos génicos, pero ahora refinando los mismos con base en evidencia transcripcional (un transcriptoma ensamblado).

Aun cuando se proporciona un script de Slurm para realizar este trabajo, es importante discutirlo línea por línea y, una vez generados los resultados, discutirlos en su totalidad. Compare estos resultados con los obtenidos en el ejercicio anterior (Ejercicio01, predicción ab initio). Para este último paso (el comparativo), utilice el programa JBrowse.

**Script `Augustus.slurm`:**

```bash
#!/bin/bash
#SBATCH -J Augustus
#SBATCH -n 1
#SBATCH --mem 25G
#SBATCH -t 0
#SBATCH -p q1
#SBATCH -e Augustus.e%j
#SBATCH -o Augustus.o%j

module load blat/35/gcc/9.3.0-rhki
module load kentutils/302.1/gcc/9.3.0-ctmb
module load augustus/3.4.0/gcc/9.3.0-chpq 

blat -minIdentity=80 GenomeSequence.fasta TranscriptomeAssembly.fasta TrainingSet.psl

pslCDnaFilter -maxAligns=1 TrainingSet.psl TrainingSet.f.psl

blat2hints.pl --in=TrainingSet.f.psl --out=TrainingSet_hints.E.gff

augustus --species=tomato --hintsfile=TrainingSet_hints.E.gff --extrinsicCfgFile=extrinsic.M.RM.E.W.cfg --UTR=off --alternatives-from-evidence=false --uniqueGeneId=true --codingseq=true --gff3=on GenomeSequence.fasta > mRNAevidenceGeneModelsNoIsoforms_v1.0.gff
```

> **Nota:** cuando se instala AUGUSTUS, en la carpeta `config/extrinsic/` vienen varios archivos de configuración listos para usarse, por ejemplo:
> - `extrinsic.M.RM.E.W.cfg`
> - `extrinsic.M.RM.cfg`
> - `extrinsic.E.RM.cfg`
> - `extrinsic.ME.cfg`
>
> Cada uno está configurado para diferentes combinaciones de fuentes de evidencia:
>
> | Letra | Fuente de evidencia |
> |---|---|
> | M | Manual anchor (obligatorio) |
> | P | Coincidencia con base de datos de proteínas |
> | E | Coincidencia con base de datos EST/cDNA |
> | C | Combinación de EST/proteína |
> | D | Dialign |
> | R | Genes retropuestos |
> | T | RefSeqs transMapped |
> | W | Información de cobertura de wiggle track (RNA-Seq) |

---

[← Volver a la portada](./)

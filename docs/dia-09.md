---
layout: default
title: "Día 09 · RNA-seq y expresión diferencial"
---

<span class="eyebrow">Martes · 29 septiembre</span>

# 📈 Día 9: Análisis de Expresión Diferencial (RNA-seq)

Bienvenid@s a la página de recursos del **Día 9** del curso **"Herramientas Bioinformáticas para el Análisis de Genomas y Transcriptomas"**. En esta jornada abordaremos de manera integral el análisis de **Expresión Diferencial de Genes (DEG)**, explorando desde la evolución metodológica (de microarreglos a RNA-seq) hasta las consideraciones de diseño experimental, modelos estadísticos de normalización, detección de genes significativos y su interpretación biológica y funcional.

---

## 🔬 Transición Tecnológica: De Microarreglos a RNA-seq

Para comprender la expresión diferencial moderna, es fundamental analizar la evolución histórica de las tecnologías transcriptómicas.

```
MICROARREGLOS DE ADN                        RNA-SEQ (NGS)
┌────────────────────────────────┐         ┌────────────────────────────────┐
│ Hibridación de sondas fijas    │         │ Secuenciación masiva directa   │
│ Intensidad de fluorescencia    │   ───►  │ Conteos discretos de lecturas  │
│ Ruido de fondo y saturación    │         │ Cobertura digital y sin sesgo  │
│ Limitado a genes conocidos     │         │ Descubrimiento de nuevos genes │
└────────────────────────────────┘         └────────────────────────────────┘
```

### 1. La Era de los Microarreglos de ADN
Desarrollada a finales de la década de 1990, esta tecnología permitió medir por primera vez la abundancia simultánea de miles de transcritos en una pequeña superficie sólida (~10,000 muestras por cm²).

#### Flujo Experimental Clásico:
1. **Fabricación:** Impresión de sondas de ADN en laminillas mediante robots aplicadores en ejes X, Y, Z.
2. **Síntesis y Marcaje:** Retrotranscripción del ARN a ADNc marcando las muestras con fluoróforos (generalmente **Cy3** en verde y **Cy5** en rojo) mediante marcaje directo o indirecto.
3. **Hibridación:** Combinación competitiva de muestras control y tratamiento sobre la laminilla.
4. **Escaneo e Imagen:** Captura de intensidades de fluorescencia en cada *spot*.
5. **Corrección de Fondo:** Tratamiento matemático para eliminar fluorescencia inespecífica (*Subtract*, *Half*, *Minimum*, *Edwards* o *Normexp*).
6. **Normalización:** Ajustes locales e intra-arreglo como el método **Loess** o **Print-Tip-Loess** para corregir sesgos sistemáticos de los aplicadores.

### 2. El Salto Cuantitativo a RNA-seq
Mientras que los microarreglos miden intensidades analógicas continuas de luz (sujetas a saturación y ruido de hibridación inespecífica), el **RNA-seq** convierte el transcriptoma en **datos digitales de conteo absoluto**.

| Parámetro | Microarreglos | RNA-seq (NGS) |
| :--- | :--- | :--- |
| **Naturaleza de la señal** | Analógica (Flujo de fluorescencia) | Digital (Conteo discreto de lecturas) |
| **Ruido de fondo** | Alto (Hibridación cruzada) | Prácticamente nulo |
| **Rango dinámico** | Limitado (< 10³) | Excepcional (> 10⁵) |
| **Dependencia de referencia** | Requerida (Sondas fijadas *a priori*) | Opcional (Permite análisis *de novo*) |
| **Detección de variaciones** | Solo abundancia general | Altura de isoformas, sustituciones y SNPs |

---

## Consideraciones Fundamentales en el Diseño Experimental

Un análisis bioinformático estricto no puede corregir las deficiencias de un diseño experimental mal planificado.

### 1. Réplicas Biológicas vs. Réplicas Técnicas
* **Réplicas Técnicas:** Múltiples mediciones o corridas de la misma muestra biológica. En RNA-seq, debido a la alta reproducibilidad técnica de las plataformas NGS, las réplicas técnicas son generalmente innecesarias.
* **Réplicas Biológicas:** Muestras provenientes de organismos o cultivos independientes sometidos a las mismas condiciones. Son **estrictamente obligatorias** para poder estimar la variabilidad biológica natural y calcular la significancia estadística ($p$-valor).

> **Aviso de diseño:** Diseñar experimentos con $N = 1$ o $N = 2$ réplicas imposibilita distinguir la variación biológica real del ruido estadístico. La literatura y las herramientas como **DESeq2** y **edgeR** recomiendan un mínimo de **3 a 4 réplicas biológicas** por condición experimental.

```
N = 1-2 Réplicas ───► Alta tasa de falsos positivos / Imposibilidad de estimar dispersión
N = 3-4 Réplicas ───► Mínimo estadístico para inferencia robusta de DEGs
N = 6+ Réplicas  ───► Máxima potencia estadística para detectar cambios sutiles (Log2FC bajo)
```

---

## Normalización en RNA-seq: De Conteos Crudos a Expresión Comparativa

En RNA-seq, el número de lecturas asignadas a un gen no depende únicamente de su nivel de expresión biológica. Existen dos sesgos sistemáticos principales que deben corregirse:

1. **Profundidad de Secuenciación (Tamaño de Biblioteca):** Una biblioteca secuenciada a 50 millones de lecturas tendrá sistemáticamente más conteos para todos sus genes que una secuenciada a 20 millones.
2. **Longitud del Transcrito:** Un gen de 10 kb generará de forma natural 5 veces más fragmentos que un gen de 2 kb expresado al mismo nivel molar.

### Métodos de Normalización Frecuentes

#### A. Métodos para Comparación de Transcritos dentro de la misma Muestra:
* **RPKM (Reads Per Kilobase Million):** Diseñado originalmente para datos de lecturas sencillas (*single-end*).
* **FPKM (Fragments Per Kilobase Million):** Análogo al RPKM pero aplicado a lecturas pareadas (*paired-end*), contando fragmentos completos.
* **TPM (Transcripts Per Million):** Normaliza primero por la longitud del transcrito y luego por la profundidad. **Es matemáticamente superior a RPKM/FPKM** porque la suma de todos los TPMs en cualquier muestra es siempre constante ($1,000,000$).

#### B. Métodos para Expresión Diferencial entre Muestras (Estadística de Conteo):
> **Atención:** Para análisis de expresión diferencial con herramientas como DESeq2 o edgeR, **NO se deben utilizar valores RPKM, FPKM o TPM**. Estas herramientas requieren **matrices de conteo crudo** (enteros) y aplican sus propios algoritmos de normalización basados en factores de tamaño (*Size Factors*).

* **Median of Ratios (DESeq2):** Calcula la media geométrica de cada gen a través de todas las muestras para estimar factores de escala globales resistentes a genes hiper-expresados.
* **TMM (Trimmed Mean of M-values - edgeR):** Elimina los genes con tasas de expresión extremas o varianza alta para calcular un factor de normalización basado en los genes de comportamiento medio.

---

## 📊 Inferencia Estadística: La Distribución Binomial Negativa

Los datos de conteo en RNA-seq son discretos y no negativos. Historicamente se asumió que seguían una distribución de Poisson, donde la media es igual a la varianza ($\mu = \sigma^2$).

Sin embargo, en muestras biológicas reales se observa el fenómeno de **Sobredispersión** (*Overdispersion*), donde la varianza es sustancialmente mayor que la media ($\sigma^2 > \mu$). Por esta razón, el estándar estadístico para modelar datos de RNA-seq es la **Distribución Binomial Negativa**:

$$	ext{Var}(Y) = \mu + lpha \mu^2$$

Donde $lpha$ representa el parámetro de **dispersión biológica**. Paquetes como DESeq2 estiman la dispersión compartiendo información entre genes con niveles de expresión similares, permitiendo pruebas de hipótesis robustas incluso con un número moderado de réplicas.

### Métricas Clave de Salida:
* **$	ext{Log}_2 	ext{Fold Change}$ ($	ext{Log}_2 	ext{FC}$):** Magnitud del cambio de expresión. Un $	ext{Log}_2 	ext{FC} = 1$ indica que el gen se expresó al doble (2 veces más) en la condición tratada; un $	ext{Log}_2 	ext{FC} = -1$ indica que se redujo a la mitad.
* **$p$-valor y $p$-valor Ajustado (FDR / Padj):** Medida de significancia estadística. Debido a que se realizan miles de pruebas de hipótesis simultáneas (una por cada gen), se aplica la corrección de pruebas múltiples de **Benjamini-Hochberg** para controlar la Tasa de Falsos Descubrimientos (**FDR**).

---

## 🎨 Visualización de Resultados e Interpretación Biológica

Una vez completado el contraste estadístico, los resultados se sintetizan mediante gráficos de alto impacto visual:

```
                  GRÁFICO VOLCANO (VOLCANO PLOT)
       10 ┌─────────────────────────────────────────┐
          │                  *                      │
          │             *         *  (DEGs)         │
   -Log10 │                *   *                    │
   p-value│ ─────────────────────────────────────── │ (Umbral FDR < 0.05)
        0 └──────────────┬───────────┬──────────────┘
                        -2           0           2
                               Log2 Fold Change
                     (Reprimidos)        (Sobreexpresados)
```

1. **MA-Plot:** Muestra la relación entre la abundancia media de conteos ($A$, eje X) y la magnitud del cambio en escala logarítmica ($M = 	ext{Log}_2	ext{FC}$, eje Y), identificando sesgos dependientes de la abundancia.
2. **Volcano Plot (Gráfico de Volcán):** Integra la significancia estadística ($-\log_{10} 	ext{Padj}$ en eje Y) y la magnitud del cambio ($	ext{Log}_2 	ext{FC}$ en eje X). Permite ubicar de un vistazo los genes más drásticamente sobreexpresados y reprimidos.
3. **Heatmap de Agrupamiento Jerárquico (Hierarchical Clustering):** Mapa de calor que agrupa tanto genes como muestras según sus perfiles de expresión normalizados ($Z$-scores), evaluando si las réplicas biológicas co-agrupan correctamente.
4. **Enriquecimiento Funcional (GO & KEGG):** Análisis posterior para evaluar si los conjuntos de genes diferencialmente expresados están enriquecidos significativamente en categorías biológicas específicas (**Gene Ontology**) o rutas metabólicas (**KEGG Pathways**).

---

## <span id="practica-11"> Práctica 11: Análisis de Expresión Diferencial </span>

Este documento reúne el instructivo de la práctica junto con los cinco scripts de SLURM utilizados en el análisis de expresión diferencial (RSEM + Trinity/DESeq2), de modo que se pueda seguir toda la secuencia de pasos sin tener que saltar entre archivos.

Este ejercicio consiste en realizar un análisis de expresión diferencial. Se utiliza como referencia el transcriptoma ensamblado resultante de Trinity y las lecturas iniciales utilizadas para generar dicho ensamblado.

**Flujo general de la práctica:**

1. Se enlaza el ensamblado de referencia (`Trinity.fasta.clean`) desde la Práctica 10.
2. Se indexa/formatea esa referencia para RSEM (`1.RSEMprepref.slurm`).
3. Se mapea cada biblioteca de RNA-seq de forma independiente contra la referencia y se cuantifica su expresión (`2.RSEMcalcexp.slurm`).
4. Se integra una matriz de abundancias relativas a partir de las cuentas esperadas de cada biblioteca (`3.AbundanceMatrix.slurm`).
5. Se identifican los genes expresados diferencialmente entre pares de condiciones (`4.DifferentialExpression.slurm`).
6. Se generan agrupamientos (clustering) y mapas de calor de los genes diferencialmente expresados (`5.Clustering.slurm`).
7. Se filtran los resultados significativos (padj ≤ 0.05) y se extraen las secuencias (nucleótido y proteína) y anotaciones correspondientes a los DEGs de cada tratamiento.

---

## Paso 0 — Enlace al transcriptoma de referencia

Como un primer paso, y con la intención de tener múltiples copias del mismo archivo en diferentes directorios, se genera un enlace al archivo a utilizar como referencia.

```bash
ln -s ../../Practica10/Trinity.fasta.clean .
```

---

## Paso 1 — Preparación de la referencia (RSEM)

Como en muchos de los procesos en los que se utiliza una referencia, ésta debe indexarse/formatearse. Para dicho fin, ejecute el script `1.RSEMprepref.slurm`. Visualice el contenido primero y, antes de su ejecución, analice las opciones que se utilizan en el archivo de ayuda. Discuta.

```bash
sbatch 1.RSEMprepref.slurm
```

### `1.RSEMprepref.slurm`

```bash
#!/bin/sh
#SBATCH -J RSEMprepref 
#SBATCH -n 1
#SBATCH -N 1
#SBATCH --mem 16G
#SBATCH -p q1
#SBATCH -e RSEMprepref.e%j
#SBATCH -o RSEMprepref.o%j

module load rsem/1.3.1/gcc/8.3.1-ehc7

rsem-prepare-reference --bowtie2 Trinity.fasta.clean ReferenceTrinityAssembly
```

---

## Paso 2 — Mapeo y cuantificación por biblioteca (RSEM)

Posteriormente, se debe realizar el mapeo de forma independiente de cada una de las diferentes bibliotecas del experimento de RNAseq. Para tal efecto ejecute el script `2.RSEMcalcexp.slurm`. Visualice también su contenido.

```bash
sbatch 2.RSEMcalcexp.slurm
```

### `2.RSEMcalcexp.slurm`

```bash
#!/bin/sh
#SBATCH -J RSEMcalcexp 
#SBATCH -n 1
#SBATCH -N 1
#SBAtCH -p q1
#SBATCH --mem 16G
#SBATCH -e RSEMcalcexp.e%j
#SBATCH -o RSEMcalcexp.o%j

module load rsem/1.3.1/gcc/8.3.1-ehc7

rsem-calculate-expression --bowtie2 --paired-end ../../Practica08/1.HQReads/HQ_Control01_R1.fastq ../../Practica08/1.HQReads/HQ_Control01_R2.fastq ReferenceTrinityAssembly Control01

rsem-calculate-expression --bowtie2 --paired-end ../../Practica08/1.HQReads/HQ_Control02_R1.fastq ../../Practica08/1.HQReads/HQ_Control02_R2.fastq ReferenceTrinityAssembly Control02

rsem-calculate-expression --bowtie2 --paired-end ../../Practica08/1.HQReads/HQ_Control03_R1.fastq ../../Practica08/1.HQReads/HQ_Control03_R2.fastq ReferenceTrinityAssembly Control03

rsem-calculate-expression --bowtie2 --paired-end ../../Practica08/1.HQReads/HQ_TreatmentX01_R1.fastq ../../Practica08/1.HQReads/HQ_TreatmentX01_R2.fastq ReferenceTrinityAssembly TreatmentX01

rsem-calculate-expression --bowtie2 --paired-end ../../Practica08/1.HQReads/HQ_TreatmentX02_R1.fastq ../../Practica08/1.HQReads/HQ_TreatmentX02_R2.fastq ReferenceTrinityAssembly TreatmentX02

rsem-calculate-expression --bowtie2 --paired-end ../../Practica08/1.HQReads/HQ_TreatmentX03_R1.fastq ../../Practica08/1.HQReads/HQ_TreatmentX03_R2.fastq ReferenceTrinityAssembly TreatmentX03

rsem-calculate-expression --bowtie2 --paired-end ../../Practica08/1.HQReads/HQ_TreatmentY01_R1.fastq ../../Practica08/1.HQReads/HQ_TreatmentY01_R2.fastq ReferenceTrinityAssembly TreatmentY01

rsem-calculate-expression --bowtie2 --paired-end ../../Practica08/1.HQReads/HQ_TreatmentY02_R1.fastq ../../Practica08/1.HQReads/HQ_TreatmentY02_R2.fastq ReferenceTrinityAssembly TreatmentY02

rsem-calculate-expression --bowtie2 --paired-end ../../Practica08/1.HQReads/HQ_TreatmentY03_R1.fastq ../../Practica08/1.HQReads/HQ_TreatmentY03_R2.fastq ReferenceTrinityAssembly TreatmentY03
```

> Nota: el diseño experimental contempla 3 condiciones (Control, TreatmentX, TreatmentY) con 3 réplicas cada una (01–03), lo que da un total de 9 bibliotecas mapeadas de forma independiente contra `ReferenceTrinityAssembly`.

---

## Paso 3 — Matriz de abundancias relativas

Los análisis de expresión diferencial asumen que la cantidad de secuencias mapeadas a cada transcrito de la referencia es relativa a sus niveles de expresión. Por tal motivo, es necesario generar una matriz de abundancias relativas, es decir, conocer cuál es el nivel de expresión de cada transcrito en cada réplica o condición. El script `3.AbundanceMatrix.slurm` genera una matriz de abundancias relativas con base en las cuentas esperadas identificadas en cada biblioteca (columnas) para cada uno de los transcritos o unigenes (renglones). Téngase en cuenta que si se busca realizar alguna normalización entre muestras, ésta deberá realizarse preferentemente con datos que no hayan sido ajustados/escalados (es decir, mejor usar cuentas esperadas que TPM o FPKM).

```bash
sbatch 3.AbundanceMatrix.slurm
```

### `3.AbundanceMatrix.slurm`

```bash
#!/bin/sh
#SBATCH -J AbundanceMatrix
#SBATCH -n 1
#SBATCH -N 1
#SBATCH --mem 25G
#SBATCH -p q1
#SBATCH -e AbundanceMatrix.e%j
#SBATCH -o AbundanceMatrix.o%j

module load rsem/1.3.1/gcc/8.3.1-ehc7
module load trinity/2.6.6/gcc/8.3.1-vykc


abundance_estimates_to_matrix.pl --est_method RSEM --gene_trans_map 'none'  --cross_sample_norm TMM \
 --out_prefix AbundanceMatrix Control01.genes.results Control02.genes.results Control03.genes.results TreatmentX01.genes.results TreatmentX02.genes.results TreatmentX03.genes.results TreatmentY01.genes.results TreatmentY02.genes.results TreatmentY03.genes.results
```

---

## Paso 4 — Análisis de expresión diferencial

Recuerde que, para llevar a cabo la identificación de genes expresados diferencialmente, los tratamientos deben siempre ser comparados por pares (p.ej., Control vs TreatmentX). Cuán significativas son estas diferencias es algo que se resuelve tras la normalización y la estimación/corrección de los valores de p (probabilidad). Son al menos dos las diferentes estrategias de normalización más utilizadas (sin embargo, no son las únicas). Analice cuidadosamente el script `4.DifferentialExpression.slurm`; note que se requieren diferentes archivos para su ejecución (`SamplesDescribed.txt` y `Contrasts.txt`). Analice cada uno de estos para su comprensión.

```bash
sbatch 4.DifferentialExpression.slurm
```

### `4.DifferentialExpression.slurm`

```bash
#!/bin/sh
#SBATCH -J DifferentialExpression
#SBATCH -n 1
#SBATCH -N 1
#SBATCH -p q1
#SBATCH --mem 16G
#SBATCH -e DifferentialExpression.e%j
#SBATCH -o DifferentialExpression.o%j

module load r/3.6.2/gcc/9.3.0-2qky
module load trinity/2.6.6/gcc/8.3.1-vykc

#run_DE_analysis.pl --matrix AbundanceMatrix.isoform.counts.matrix --method edgeR --output DEG --samples_file SamplesDescribed.txt --contrasts Contrasts.txt
run_DE_analysis.pl --matrix AbundanceMatrix.isoform.counts.matrix --method DESeq2 --output DEG --samples_file SamplesDescribed.txt --contrasts Contrasts.txt
```

> Nota: el script incluye, comentada, la alternativa de correr el análisis con `edgeR` en lugar de `DESeq2`; ambas son estrategias de normalización/estimación estadística válidas, pero en esta práctica se ejecuta con `DESeq2`.

Tras haber corrido el script, notará que los resultados se generan en un directorio (`DEG`); los archivos PDF puede importarlos a su máquina local para visualizarlos. Analice las tablas que contienen los resultados (p.ej., `AbundanceMatrix.isoform.counts.matrix.cond_B_vs_cond_A.DESeq2.DE_results`) y, a partir de éstas, seleccione los unigenes expresados diferencialmente cuyas diferencias sean significativas (padj ≤ 0.05).

```bash
awk -F"\t" '$11<=0.05 {print $1"\t"$7"\t"$11}' AbundanceMatrix.isoform.counts.matrix.cond_B_vs_cond_A.DESeq2.DE_results > TreatmentX_DEG
awk -F"\t" '$11<=0.05 {print $1"\t"$7"\t"$11}' AbundanceMatrix.isoform.counts.matrix.cond_C_vs_cond_A.DESeq2.DE_results > TreatmentY_DEG
```

---

## Paso 5 — Clustering y mapas de calor de los DEGs

Complementando el análisis de expresión diferencial, el script `5.Clustering.slurm` agrupa (clusteriza) los genes/transcritos con expresión diferencial significativa y genera un mapa de calor (`HeatMap`) a partir de la matriz de expresión normalizada (TMM), usando el mismo umbral de significancia (P ≤ 0.05) y un cambio mínimo de 2^C veces (fold-change, `-C 2`).

```bash
sbatch 5.Clustering.slurm
```

### `5.Clustering.slurm`

```bash
#!/bin/sh
#SBATCH -J ClusteringDE
#SBATCH -n 1
#SBATCH -N 1
#SBATCH -p q1
#SBATCH --mem 16G
#SBATCH -e ClusteringDE.e%j
#SBATCH -o ClusteringDE.o%j

module load r/3.6.2/gcc/9.3.0-2qky
module load trinity/2.6.6/gcc/8.3.1-vykc

cd DEG

analyze_diff_expr.pl --matrix ../AbundanceMatrix.isoform.TMM.EXPR.matrix -P 0.05 -C 2 --output HeatMap --samples ../SamplesDescribed.txt
```

---

## Paso 6 — Extracción de secuencias y anotaciones de los DEGs

Puede generar ahora una lista que contenga únicamente los identificadores de los unigenes diferencialmente expresados y, con base en ella, generar un archivo fasta que contenga únicamente estas secuencias, partiendo del archivo resultante del ensamblado que fuera utilizado como referencia para el análisis de RNAseq. También puede generar una lista de los descriptores de cada una de las proteínas codificadas en dichos unigenes.

```bash
awk -F"\t" '{print $1}' TreatmentX_DEG > TreatmentX_DEG.IDs
awk -F"\t" '{print $1}' TreatmentY_DEG > TreatmentY_DEG.IDs

module load cdbfasta/2017-03-16/gcc/9.3.0-afj3

cdbfasta ../Trinity.fasta.clean
cat TreatmentX_DEG.IDs | cdbyank ../Trinity.fasta.clean.cidx > TreatmentX_DEG.fasta
cat TreatmentY_DEG.IDs | cdbyank ../Trinity.fasta.clean.cidx > TreatmentY_DEG.fasta

grep -c ">" TreatmentX_DEG.fasta TreatmentY_DEG.fasta
```

¿Podemos también obtener las secuencias de las proteínas correspondientes a cada uno de los DEG?

```bash
cdbfasta ../../../Practica10/Trinity_Awise_prot.fas

cat TreatmentX_DEG.IDs | cdbyank ../../../Practica10/Trinity_Awise_prot.fas.cidx > TreatmentX_DEG_PRT.fasta
cat TreatmentY_DEG.IDs | cdbyank ../../../Practica10/Trinity_Awise_prot.fas.cidx > TreatmentY_DEG_PRT.fasta

grep -c ">" TreatmentX_DEG_PRT.fasta TreatmentX_DEG.fasta
grep -c ">" TreatmentY_DEG_PRT.fasta TreatmentY_DEG.fasta
```

¿Podríamos también generar una lista de los identificadores de cada una de las proteínas de Arabidopsis (o, en general, de la base de referencia utilizada) que resultaron homólogas a estos unigenes?

```bash
grep -Ff TreatmentX_DEG.IDs ../../../Practica10/BlastResult > DEGTreatmentXAnnotation.txt
grep -Ff TreatmentY_DEG.IDs ../../../Practica10/BlastResult > DEGTreatmentYAnnotation.txt
```

> Nota: este paso reutiliza el archivo de resultados de BLAST generado en la Práctica 10 (`BlastResult`), donde cada unigén de Trinity tiene asociado su mejor hit homólogo. Filtrando por los identificadores de los DEGs se obtiene la anotación funcional de únicamente aquellos unigenes con expresión diferencial significativa.

---

## Resumen de archivos generados

| Etapa | Archivos / directorios generados |
|---|---|
| Preparación de referencia | `ReferenceTrinityAssembly.*` (índices RSEM/bowtie2) |
| Cuantificación por biblioteca | `Control01.genes.results` ... `TreatmentY03.genes.results` (9 bibliotecas) |
| Matriz de abundancias | `AbundanceMatrix.isoform.counts.matrix`, `AbundanceMatrix.isoform.TMM.EXPR.matrix` |
| Expresión diferencial | Directorio `DEG/` con tablas `*.DESeq2.DE_results` y gráficos PDF |
| Clustering / mapas de calor | Directorio `HeatMap` (dentro de `DEgenes/`) |
| Filtrado de DEGs significativos | `TreatmentX_DEG`, `TreatmentY_DEG`, `TreatmentX_DEG.IDs`, `TreatmentY_DEG.IDs` |
| Secuencias de los DEGs | `TreatmentX_DEG.fasta`, `TreatmentY_DEG.fasta`, `TreatmentX_DEG_PRT.fasta`, `TreatmentY_DEG_PRT.fasta` |
| Anotación de los DEGs | `DEGTreatmentXAnnotation.txt`, `DEGTreatmentYAnnotation.txt` |

---

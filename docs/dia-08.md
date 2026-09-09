---
layout: default
title: "Día 08 · Ensamblaje y evaluación de transcriptomas"
---

<span class="eyebrow">Sábado · 26 septiembre</span>

# 📊 Día 8: Aplicabilidad de Transcriptomas y Criterios de Calidad en el Ensamblado

Bienvenid@s a la página de recursos del **Día 8** del curso **"Herramientas Bioinformáticas para el Análisis de Genomas y Transcriptomas"**. En esta jornada exploraremos las diversas aplicaciones biológicas de la secuenciación de ARN (RNA-seq), los sesgos y errores estructurales inherentes al ensamblado de secuencias expresadas, y los criterios e indicadores estadísticos necesarios para evaluar la calidad y completitud de un transcriptoma.

---

## 🔬 Teoría: Aplicaciones del Transcriptoma y RNA-seq

### 1. Evolución de las Tecnologías Transcriptómicas
El estudio global de la expresión génica ha evolucionado a través de tres grandes eras tecnológicas, siendo el RNA-seq la metodología dominante en la actualidad:

*   **Microarreglos (Microarrays):** Basados en la hibridación de cDNAs fluorescentes sobre sondas prediseñadas. Presentan alto rendimiento pero sufren de ruido de fondo, saturación de señal y limitación estricta a secuencias previamente conocidas (dependientes del genoma).
*   **Secuenciación de Bibliotecas EST / Sanger:** Basados en la lectura directa de clones de cDNA. Ofrecen resolución de base única pero sufren de muy bajo rendimiento y costos prohibitivos para cobertura profunda.
*   **RNA-seq (Secuenciación Masiva de ARN):** Utiliza tecnologías NGS para generar millones de lecturas cortas o largas de ARN/cDNA. Ofrece resolución de base única, rango dinámico amplio, bajo ruido de fondo y total independencia de un genoma de referencia previo.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                       APLICACIONES CLAVE DE RNA-SEQ                         │
├─────────────────────────────────────────────────────────────────────────────┤
│ 1. Identificación y descubrimiento de nuevos transcritos, exones y genes.   │
│ 2. Cuantificación simultánea de la expresión génica diferencial (DEGs).     │
│ 3. Caracterización de eventos de empalme alternativo (splicing) e isoformas.│
│ 4. Análisis de perfiles de expresión órgano/tejido-específicos.            │
│ 5. Detección de variabilidad genética (SNPs, indels y expresión alelica).   │
└─────────────────────────────────────────────────────────────────────────────┘
```

### 2. Etapas del Análisis Bioinformático en RNA-seq
Un flujo completo de análisis de transcriptomas mediante RNA-seq comprende tres fases secuenciales:

1.  **Pre-análisis:** Diseño experimental, selección de réplicas biológicas, longitud de lectura (Single-End vs. Paired-End) y control de calidad inicial del material crudo.
2.  **Análisis Central (*Core Analysis*):** Alineamiento/ensamblado de lecturas, reconstrucción de transcritos, cuantificación de abundancia a nivel de gen o isoforma (conteos, TPM, FPKM/RPKM) y análisis estadístico de expresión diferencial.
3.  **Análisis Avanzado e Interpretación:** Integración funcional (enriquecimiento GO, vías KEGG), identificación de ARNs no codificantes pequeños o largos, descubrimiento de fusiones génicas y visualización en navegadores genómicos.

---

## ⚠️ Errores Comunes y Sesgos en el Ensamblado de Transcriptomas

A diferencia de los genomas, el ensamblado de ARN enfrenta el reto de la abundancia heterogénea de lecturas (desde transcritos altamente expresados hasta secuencias raras). Esto genera artefactos bioinformáticos característicos:

| Tipo de Error / Sesgo | Descripción Biológica e Informática | Impacto en el Análisis |
| :--- | :--- | :--- |
| **Colapso de Familias (*Family Collapse*)** | Transcritos de genes paralogos o isoformas altamente similares son colapsados erróneamente en un único transcrito quimérico. | Pérdida de la diversidad de isoformas y estimación sesgada de la expresión. |
| **Quimerismo (*Chimerism*)** | Fusión artificial de dos transcritos independientes que comparten un pequeño motivo homólogo durante la extensión del grafo. | Generación de genes falsos con anotaciones funcionales duales no biológicas. |
| **Inserciones No Soportadas** | Retención de fragmentos intrónicos o secuencias aleatorias sin soporte real de lecturas en medio de un transcrito. | Interrupción artificial del marco de lectura abierto (ORF). |
| **Incompletitud (*Incompleteness*)** | Transcritos ensamblados que carecen de sus extremos $5'$ o $3'$ debido a caídas en la cobertura de secuenciación. | Detección de proteínas truncadas y pérdida de regiones UTR reguladoras. |
| **Fragmentación (*Fragmentation*)** | Un único transcrito biológico largo queda dividido en múltiples *contigs* cortos e independientes. | Sobrestimación del número total de genes/unigenes en el ensamblaje. |
| **Redundancia (*Redundancy*)** | Producción de múltiples *contigs* ligeramente variados para el mismo transcrito debido a errores de lectura o heterocigosidad. | Inflación del tamaño del transcriptoma y sesgos en la asignación de lecturas. |

---

## 🎯 Criterios de Calidad para Evaluar Transcriptomas

Para verificar si un ensamblado de transcriptoma es confiable, se debe realizar una evaluación multidimensional combinando criterios de continuidad, integridad biológica y anotación funcional.

```
                  ┌────────────────────────────────────────┐
                  │ CRITERIOS DE EVALUACIÓN DE CALIDAD     │
                  └───────────────────┬────────────────────┘
                                      │
         ┌────────────────────────────┼────────────────────────────┐
         ▼                            ▼                            ▼
┌──────────────────┐        ┌──────────────────┐        ┌──────────────────┐
│  CONTINUIDAD Y   │        │   INTEGRIDAD     │        │   ANOTACIÓN Y    │
│    COBERTURA     │        │    BIOLÓGICA     │        │   CONTENIDO      │
├──────────────────┤        ├──────────────────┤        ├──────────────────┤
│ • N50 vs ExN50   │        │ • Identificación │        │ • % Unigenes     │
│ • Re-mapeo de    │        │   de ORFs        │        │   anotados       │
│   lecturas (%)   │        │ • BUSCO %        │        │ • Cobertura      │
│ • TransRate Score│        │   completitud    │        │   Full-Length    │
└──────────────────┘        └──────────────────┘        └──────────────────┘
```

### 1. Métricas de Continuidad: N50 tradicional vs. ExN50
*   **N50 Tradicional:** Longitud para la cual el 50% de las bases del ensamblaje se encuentran en *contigs* de esa longitud o mayor. En transcriptomas, el N50 tradicional puede ser engañoso, ya que la presencia de miles de transcritos cortos ruidosos puede deprimir artificialmente el valor sin que ello signifique un mal ensamblaje.
*   **Métrica ExN50 (N50 Expresado):** Calcula el valor de N50 considerando únicamente el subconjunto de transcritos más altamente expresados que representan el $x\%$ del volumen total de expresión (por ejemplo, $E90N50$, el N50 del 90% de la expresión). A medida que se limita el cálculo a los transcritos con cobertura adecuada, el ExN50 alcanza un pico que refleja la verdadera continuidad del transcriptoma.

### 2. Porcentaje de Mapeo de Retorno (*Read Re-mapping Rate*)
Una prueba fundamental de validez consiste en alinear las lecturas crudas filtradas de regreso al transcriptoma ensamblado usando alineadores rápidos como Bowtie2, Salmon o Kallisto.
*   **Interpretación:** Un ensamblaje de alta calidad debe recuperar entre el **$80\%$ y el $90\%$** de las lecturas crudas representadas en los *contigs*. Un porcentaje bajo ($< 70\%$) indica que una fracción considerable de los datos se perdió durante la construcción del grafo.

### 3. Presencia y Longitud de Marcos de Lectura Abiertos (ORFs)
Los transcritos codificantes de proteínas deben albergar un **ORF (Open Reading Frame)** de longitud adecuada.
*   Se utilizan herramientas como **TransDecoder** para predecir regiones codificantes (codones de inicio ATG, codón de paro y composición de aminoácidos).
*   **Criterio de Calidad:** Un transcriptoma de alta calidad presenta una alta proporción de transcritos con ORFs completos (con sitio de inicio y paro identificados) y una distribución de longitudes de proteína coherente con la especie o grupo taxonómico de estudio.

### 4. Cobertura de Transcritos de Longitud Completa (*Full-length Transcripts*)
Mediante búsquedas de homología (`blastx`) contra bases de datos de proteínas curadas de referencia (como UniProtKB/Swiss-Prot):
*   Se evalúa qué porcentaje de las proteínas de referencia son cubiertas en más del **$80\%$ o $90\%$** de su longitud total por un único *contig* del ensamblaje.
*   Esta métrica permite cuantificar directamente el grado de fragmentación del transcriptoma.

### 5. Evaluación de Ortólogos Conservados (BUSCO)
Al igual que en genomas, la herramienta **BUSCO** analiza la presencia de genes ortólogos de copia única altamente conservados en la línea evolutiva correspondiente (p. ej., *eukaryota*, *viridiplantae*, *metazoa*).
*   **Categorías:** Se clasifican en Genes Completos y de Copia Única (*Single-copy*), Completos Duplicados (*Duplicated*), Fragmentados (*Fragmented*) o Ausentes (*Missing*).
*   Un porcentaje elevado de genes duplicados en un transcriptoma *de novo* sugiere la presencia de isoformas no agrupadas o redundancia en el ensamblaje.

### 6. Porcentaje de Unigenes Anotados Funcionalmente
El proceso de agrupación de transcritos similares genera conjuntos de **Unigenes** (representantes únicos por locus).
*   El éxito global del transcriptoma se mide calculando el porcentaje de Unigenes que logran ser asignados a una función conocida mediante alineamientos contra bases de datos de referencia (Swiss-Prot, Pfam, EggNOG, GO, KEGG).
*   Un transcriptoma bien ensamblado y libre de quimeras o errores de fase suele alcanzar entre un **$50\%$ y $70\%$** de anotación funcional exitosa en organismos no modelo.

---

# Práctica 09

Este documento reúne el instructivo de la práctica junto con los tres scripts de SLURM utilizados durante el flujo de trabajo (`SeqClean.slurm`, `getORF.slurm` y `Translate.slurm`), de modo que se pueda seguir toda la secuencia de ejercicios sin tener que saltar entre archivos.

**Flujo general de la práctica:**

1. Se parte de los transcriptomas ensamblados en la Práctica 08 (Mira y Trinity).
2. Se calculan métricas iniciales de longitud de secuencias.
3. Se limpian las secuencias con SeqClean (elimina secuencias cortas, colas poly A/T, baja complejidad y regiones ricas en Ns).
4. Se vuelven a calcular métricas para comparar antes/después de la limpieza.
5. Se identifican marcos de lectura abiertos (ORFs) con `getorf` (EMBOSS).
6. Se traduce el ORF más largo de cada transcrito/unigén a proteína con `translate2aa.pl`.
7. Se generan métricas finales sobre las proteínas resultantes.

---

## Ejercicio 01 — Preparación y limpieza de secuencias

Copie o genere un link simbólico en su directorio actual hacia los archivos resultantes de la Practica08, es decir, los transcriptomas ensamblados generados con Mira y Trinity.

```bash
ln -s ../Practica08/2.MiraAssembly/Mira_assembly/Mira_d_results/Mira_out.unpadded.fasta Mira.fasta
ln -s ../Practica08/3.TrinityAssembly/trinity_out_dir.Trinity.fasta Trinity.fasta
```

Utilice el script de perl `fastx-length.pl` ([fuente en GitHub](https://github.com/gringer/bioinfscripts/blob/master/fastx-length.pl)) para calcular algunas métricas/estadísticas simples.

```bash
./fastx-length.pl Mira.fasta >Temp 2>MiraStat01.txt
./fastx-length.pl Trinity.fasta >Temp 2>TrinityStat01.txt
```

Analice los resultados. Note que el umbral del tamaño en las secuencias resultantes tras el proceso de ensamblado es distinto en ambos ensambladores. Utilice la herramienta `seqclean` para eliminar secuencias <200, y recortar además aquellas secuencias que contengan elementos como: colas poly A/T, secuencias de baja complejidad y secuencias terminales ricas en bases indeterminadas (Ns). Revise el archivo de ayuda del programa `seqclean` para tal propósito. Al término, genere nuevas métricas y compare ambos resultados.

```bash
sbatch SeqClean.slurm
```

### `SeqClean.slurm`

```bash
#!/bin/sh
#SBATCH -J SeqClean
#SBATCH -n 1
#SBATCH -N 1
#SBATCH --mem 16G
#SBATCH -t 0
#SBATCH -e SeqClean.e%j
#SBATCH -o SeqClean.o%j
#SBATCH -p q1

module load seqclean/1.0/gcc/9.3.0-2hn4

seqclean Mira.fasta -l 201 -N -L -A
seqclean Trinity.fasta -l 201 -N -L -A
```

Tras la ejecución, genere las métricas post-limpieza:

```bash
./fastx-length.pl Mira.fasta.clean >Temp 2>MiraStat02.txt
./fastx-length.pl Trinity.fasta.clean >Temp 2>TrinityStat02.txt
```

---

## Ejercicio 02 — Identificación de marcos de lectura abiertos (ORFs)

Identifique marcos de lectura abiertos al interior de las contigs (unigenes) resultantes de los procesos de ensamblado. Utilice la herramienta `getorf`, disponible en el kit de herramientas de EMBOSS ([emboss.sourceforge.net](http://emboss.sourceforge.net/)). Para dicho propósito ejecute `getORF.slurm`. Antes de ejecutar la tarea, visualice el contenido de dicho archivo (`getORF.slurm`), cargue el módulo correspondiente y lea el archivo de ayuda para interpretar las variables utilizadas.

**EMBOSS**

```bash
module purge
module load emboss/6.6.0/gcc/8.3.1-7aag
getorf --help
sbatch getORF.slurm
```

### `getORF.slurm`

```bash
#!/bin/sh
#SBATCH -J getORF
#SBATCH -n 1
#SBATCH --mem 20G
#SBATCH -t 0
#SBATCH -p q1
#SBATCH -e getORF.e%j
#SBATCH -o getORF.o%j

module load emboss/6.6.0/gcc/9.3.0-4geh

getorf -sequence Mira.fasta.clean -outseq MiraORF.fna -minsize 201 -find 2 
getorf -sequence Mira.fasta.clean -outseq MiraPRT.faa -minsize 201 -find 0 
#-------------------------------------------------------------------------------------------
getorf -sequence Trinity.fasta.clean -outseq TrinityORF.fna -minsize 201 -find 2
getorf -sequence Trinity.fasta.clean -outseq TrinityPRT.faa -minsize 201 -find 0 
#-------------------------------------------------------------------------------------------
mkdir EmbossResults
mv *ORF.fna EmbossResults
mv *PRT.faa EmbossResults
mv fastx-length.pl EmbossResults
cd EmbossResults
./fastx-length.pl MiraORF.fna >Temp 2>MiraORFStat.txt
./fastx-length.pl TrinityORF.fna >Temp 2>TrinityORFStat.txt
rm Temp
cd ..
```
Analice los archivos resultantes y compare.

---

## Ejercicio 03 — Traducción del ORF más largo a proteína

Para generar un archivo que contenga la secuencia proteica que corresponde al ORF más largo identificado en cada transcrito o unigén, ejecute el script de perl `translate2aa.pl` (descargado de GitHub). Este script requiere EMBOSS (utiliza `getorf`) y algunas bibliotecas de BioPerl, por lo que debe asegurarse de cargar los módulos correspondientes al ejecutar el script en la línea de comandos. Puede realizar esta tarea utilizando el archivo generado para el gestor de tareas (`Translate.slurm`).

Ejecute preferentemente la tarea de la siguiente manera (tiempo aproximado 25 min):

```bash
sbatch Translate.slurm
```

### `Translate.slurm`

```bash
#!/bin/sh
#SBATCH -J Translante
#SBATCH -n 1
#SBATCH --mem 20G
#SBATCH -t 0
#SBATCH -p q1
#SBATCH -e Translate.e%j
#SBATCH -o Translate.o%j

module load emboss/6.6.0/gcc/9.3.0-4geh
module load perl/5.30.1/gcc/9.3.0-ib6o
module load perl-bioperl/1.7.6/gcc/9.3.0-fh2w

./translate2aa.pl -m 67 ../Mira.fasta.clean > MiraORFsTranslated.fasta
./translate2aa.pl -m 67 ../Trinity.fasta.clean > TrinityORFsTranslated.fasta
```
Estime las métricas para los archivos recientemente generados y compare las salidas:

```bash
./fastx-length.pl TrinityORFsTranslated.fasta > MetricasTrinityPRT.txt
./fastx-length.pl MiraORFsTranslated.fasta > MetricasMiraPRT.txt
```

---

## Resumen de archivos generados

| Etapa | Archivos generados |
|---|---|
| Métricas iniciales | `MiraStat01.txt`, `TrinityStat01.txt` |
| Limpieza (SeqClean) | `Mira.fasta.clean`, `Trinity.fasta.clean` |
| Métricas post-limpieza | `MiraStat02.txt`, `TrinityStat02.txt` |
| ORFs (nucleótidos y proteína cruda) | `MiraORF.fna`, `MiraPRT.faa`, `TrinityORF.fna`, `TrinityPRT.faa` (en `EmbossResults/`) |
| Métricas de ORFs | `MiraORFStat.txt`, `TrinityORFStat.txt` |
| ORF más largo traducido | `MiraORFsTranslated.fasta`, `TrinityORFsTranslated.fasta` |
| Métricas finales de proteínas | `MetricasMiraPRT.txt`, `MetricasTrinityPRT.txt` |

---
[← Volver a la portada](./)

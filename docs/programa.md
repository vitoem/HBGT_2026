---
layout: default
title: Programa
---

# Programa Detallado del Curso
## Herramientas Bioinformáticas para el Análisis de Genomas y Transcriptomas (HBGT 2026)

---

## Información general

| Campo | Detalle |
|---|---|
| **Fechas** | Del 17 de septiembre al 01 de octubre de 2026 |
| **Duración** | 11 días, 8 horas diarias de trabajo intensivo |
| **Idioma oficial** | Español |
| **Cupo máximo** | 20 participantes |
| **Sede** | Instituto de Ecología A.C. (INECOL), Salón BioMimic, Segundo Piso, Edificio B, Campus 3 |
| **Coordinación** | Dr. Enrique Ibarra Laclette y M. en C. Emanuel Villafán de la Torre |
| **Equipo de instructores** | Dr. Enrique Ibarra Laclette · M. en C. Emanuel Villafán de la Torre · Dra. Diana Hernández Oaxaca · Dr. Michel Pale Rivas |
| **Ayudante del curso** | Andrea Iridiana Barraza Ochoa |

**Mecanismo de evaluación:**
1. Asistencia y participación activa — 20%
2. Ejercicios prácticos desarrollados en cada sesión — 40%
3. Evaluaciones parciales — 40%

---

## Programa detallado por día

| Día | Fecha | Tema del día | Contenidos abordados | Práctica(s) asociada(s) | Responsable |
|---|---|---|---|---|---|
| **1** | Jueves 17 sept | Introducción y Fundamentos del Curso | • Información general y logística del curso<br>• Genómica y Transcriptómica en la Era Ómica: ¿qué es el genoma?, Paradoja del Valor C<br>• Organización genómica: procariotas vs. eucariotas<br>• El Transcriptoma: de las ómicas a la función<br>• Cómputo de Alto Rendimiento (HPC): biología computacional, bioinformática, pipelines, procesos serializados/paralelizados, clústers, scheduler | Práctica de Linux I (introducción a la línea de comandos) | Emanuel Villafán |
| **2** | Viernes 18 sept | Nociones generales de los genes y genomas | • Evolución de genomas complejos: poliploidía (auto- y alopoliploidía)<br>• Diploidización y fraccionamiento genómico<br>• Sintenia genómica (intra- e inter-genómica) | Práctica de Linux II (organización y seguridad) | Enrique Ibarra |
| **3** | Lunes 21 sept | Control y Procesamiento de Lecturas | • Dogma central y ciencias ómicas (genómica, transcriptómica, proteómica, metabolómica)<br>• Flujo metodológico NGS: preparación de librerías, amplificación clonal, secuenciación cíclica<br>• Anatomía del archivo FASTQ y escala de calidad Phred | **Práctica 01** — Preprocesamiento de secuencias:<br>Ej.1 Exploración/inspección de datos Single-End (compresión, conversión de calidad, formato de encabezados, conversión FASTQ↔FASTA/QUAL)<br>Ej.2 Diagnóstico y filtrado SE/PE (FastQC, FASTX-Toolkit, Trimmomatic, `qualityControl.py`, SeqPrep)<br>Ej.3 Extracción de secuencias 454 (archivos SFF)<br>Ej.4 Extracción/manipulación de archivos BAM (lecturas PacBio) | Enrique Ibarra |
| **4** | Martes 22 sept | Algoritmos y Herramientas para el Ensamblado de Genomas de Novo | • Jerarquía del ensamblado genómico (reads → contigs → scaffolds → cromosomas)<br>• Algoritmos codiciosos (Greedy)<br>• Overlap-Layout-Consensus (OLC)<br>• Grafos de de Bruijn (DBG) y k-meros<br>• Mecánica de un ensamblador moderno (remoción de ramales, colapso de burbujas) | **Práctica 02** — Ensamblado de genomas (Newbler y MIRA):<br>Ej.1 Newbler: ensamblado con coberturas 10X y 20X<br>Ej.2 Newbler: ensamblado híbrido con distintos formatos y coberturas<br>Ej.3 MIRA: ensamblado con el mismo set de datos | Emanuel Villafán |
| **5** | Miércoles 23 sept | Anotación de Genomas, Métodos y Bases de Datos | • Anotación estructural vs. funcional<br>• Prerrequisitos de la anotación<br>• Enmascaramiento de repetidos, homología, métodos ab initio (HMM: AUGUSTUS, GeneMark, GlimmerHMM, tRNAscan-SE, SNAP)<br>• Bases de datos estructurales (SRA, NONCODE, miRBase, Pseudogene.org, Dfam)<br>• Anotación funcional: transferencia de función por homología<br>• Bases de datos funcionales: Gene Ontology (GO), KEGG, InterPro/InterProScan (CDD, Pfam, PROSITE, etc.) | **Práctica 03** — Métricas de ensamblado (`assemblathon_stats.pl`) y evaluación de completitud con BUSCO<br>**Práctica 04** — Anotación de genomas procariontes con DFAST y Prokka/Proksee<br>**Práctica 05** — Predicción de modelos génicos con Augustus (ab initio y con evidencia transcripcional vía BLAT) | Emanuel Villafán |
| **6** | Jueves 24 sept | Identificación de RNAs No Codificantes (ncRNAs) y Elementos Repetitivos | • Elementos Transponibles (TEs): Clase I (retrotransposones) y Clase II (transposones de ADN)<br>• Estructura molecular de retrotransposones LTR<br>• Transcriptoma no codificante y lncRNAs (definición, comparación con mRNA, origen evolutivo, clasificación genómica: lincRNA, intrónico, antisentido/lncNAT)<br>• Herramientas de predicción de lncRNAs (FEELnc, PLncPRO, PLEK, Evolinc) | **Práctica 06** — Identificación de lncRNAs con Evolinc-I y relación con genes vecinos (gffread, bedtools)<br>**Práctica 07** — Identificación de otros ncRNAs con Rfam/Infernal (tRNAs) y elementos transponibles: estructura con LTR_Finder y enmascaramiento con RepeatMasker | Michel Pale |
| **7** | Viernes 25 sept | Reconstrucción y Ensamblado de Transcriptomas | • Desafíos del ensamblado de transcriptomas (abundancia desproporcionada, splicing alternativo, familias génicas)<br>• Ensamblado de novo: algoritmo Trinity (Inchworm, Chrysalis, Butterfly)<br>• Reconstrucción basada en genoma de referencia (mapeo empalmado, BWT/FM-index: HISAT2, STAR)<br>• Enfoques híbridos y tabla comparativa de estrategias | **Práctica 08** — Ensamblado de novo de transcriptomas (RNAseq):<br>Ej.1 Preparación de lecturas de alta calidad (concatenado R1/R2)<br>Ej.2 Ensamblado de novo con MIRA<br>Ej.3 Ensamblado de novo con Trinity | Emanuel Villafán |
| **8** | Lunes 28 sept | Aplicabilidad de Transcriptomas y Criterios de Calidad en el Ensamblado | • Evolución de tecnologías transcriptómicas (microarreglos, EST/Sanger, RNA-seq) y aplicaciones de RNA-seq<br>• Errores y sesgos comunes en el ensamblado (colapso de familias, quimerismo, fragmentación, redundancia)<br>• Criterios de calidad: N50 vs. ExN50, % de re-mapeo de lecturas, ORFs (TransDecoder), cobertura full-length, BUSCO, % de unigenes anotados | **Práctica 09** — Limpieza (SeqClean), identificación de ORFs (`getorf`, EMBOSS) y traducción del ORF más largo (`translate2aa.pl`) de los transcriptomas Mira y Trinity<br>**Práctica 10** — Construcción de base de datos de referencia (`FormatDB.slurm`/`makeblastdb`), identificación de CDS con AlignWise y contraste por BLASTp contra la base de datos de referencia | Enrique Ibarra |
| **9** | Martes 29 sept | Análisis de Expresión Diferencial (RNA-seq) | • Transición de microarreglos a RNA-seq<br>• Diseño experimental: réplicas biológicas vs. técnicas<br>• Normalización (RPKM, FPKM, TPM, Median of Ratios/DESeq2, TMM/edgeR)<br>• Distribución binomial negativa y sobredispersión<br>• Log2FC, valor p, FDR (Benjamini-Hochberg)<br>• Visualización e interpretación: MA-plot, Volcano plot, Heatmap, enriquecimiento GO/KEGG | **Práctica 11** — Cuantificación de expresión con RSEM, matriz de abundancias (TMM), análisis de expresión diferencial con DESeq2, clustering/mapas de calor, y extracción de secuencias y anotaciones de los DEGs | Enrique Ibarra |
| **10** | Martes 30 sept | Metagenómica I | Introducción al análisis de datos metagenómicos y flujo de trabajo. *(Materiales pendientes de publicación por parte de la coordinación del curso)* | Pendiente de publicar | Diana Hernández |
| **11** | Jueves 1 oct | Metagenómica II y cierre del curso | Continuación del análisis metagenómico, evaluación final y cierre del curso. *(Materiales pendientes de publicación por parte de la coordinación del curso)* | Pendiente de publicar / Evaluación final | Diana Hernaández |

---

## Resumen de prácticas numeradas

| Práctica | Día | Título | Herramientas principales |
|---|---|---|---|
| 01 | Día 3 | Preprocesamiento de secuencias | FastQC, FASTX-Toolkit, Trimmomatic, SeqPrep, samtools, bedtools, bioawk |
| 02 | Día 4 | Ensamblado de genomas (bacterianos) | Newbler, MIRA |
| 03 | Día 5 | Métricas de ensamblado y evaluación con BUSCO | assemblathon_stats.pl, BUSCO |
| 04 | Día 5 | Anotación de genomas procariontes | DFAST, Prokka/Proksee |
| 05 | Día 5 | Predicción de modelos génicos | Augustus, BLAT, JBrowse |
| 06 | Día 6 | Identificación de lncRNAs | Evolinc-I, gffread, bedtools |
| 07 | Día 6 | Otros ncRNAs y elementos transponibles | Infernal/Rfam, LTR_Finder, RepeatMasker |
| 08 | Día 7 | Ensamblado de novo de transcriptomas | MIRA, Trinity |
| 09 | Día 8 | Limpieza, ORFs y traducción | SeqClean, EMBOSS (getorf), translate2aa.pl |
| 10 | Día 8 | Anotación funcional de unigenes | makeblastdb, AlignWise, BLASTp |
| 11 | Día 9 | Expresión diferencial | RSEM, Trinity (abundance_estimates_to_matrix.pl, run_DE_analysis.pl, analyze_diff_expr.pl), DESeq2, cdbfasta |

---
*Fuentes utilizadas para construir este programa:*
- `docs/programa.md`
- `docs/dia-01.md` a `docs/dia-11.md`

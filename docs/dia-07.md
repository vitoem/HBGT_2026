---
layout: default
title: "Día 07 · lncRNA, ortólogos y familias génicas"
---

<span class="eyebrow">Viernes · 25 septiembre</span>

# Día 7: Reconstrucción y Ensamblado de Transcriptomas

Bienvenid@s a la página de recursos del **Día 7** del curso **"Herramientas Bioinformáticas para el Análisis de Genomas y Transcriptomas"**. En esta jornada exploraremos las estrategias algorítmicas y consideraciones particulares para la reconstrucción de transcriptomas a partir de datos de RNA-Seq, evaluando el ensamblado *de novo* frente a la reconstrucción guiada por un genoma de referencia y los enfoques híbridos.

---

## 🧪 Teoría: Consideraciones en la Reconstrucción del Transcriptoma

El transcriptoma representa el conjunto completo de transcritos de ARN (mRNAs y ncRNAs) expresados en una célula o tejido en un momento y condición específicos. A diferencia del genoma (que es estático y de número de copias equimolar), el transcriptoma es **altamente dinámico, multifactorial y muestra un rango dinámico de abundancia que abarca varios órdenes de magnitud**.

### Desafíos Particulares del Ensamblado de Transcriptomas
1. **Abundancia Desproporcionada:** Los transcritos altamente expresados generan millones de lecturas, mientras que los transcritos de baja abundancia cuentan con muy poca cobertura.
2. **Splicing Alternativo:** Un solo gen puede producir múltiples isoformas mediante combinaciones variables de exones, generando eventos de ramificación en los grafos de ensamblado.
3. **Familias Génicas y Duplicaciones:** Secuencias homólogas o duplicadas pueden confundir los algoritmos de resolución de grafos.

---

## 🌀 Estrategia 1: Ensamblado *De Novo* del Transcriptoma

El ensamblado *de novo* reconstruye secuencias de ARN directamente a partir de las lecturas cortas de RNA-Seq sin requerir un genoma de referencia previo.

### El Algoritmo Trinity
El ensamblador de referencia para transcriptomas *de novo* es **Trinity**, el cual divide la reconstrucción en tres módulos secuenciales:

```text
Lecturas FASTQ (RNA-Seq)
         │
         ▼
 ┌───────────────┐
 │   INCHWORM    │  --> Construye contigs iniciales utilizando una extensión codiciosa (greedy)
 └───────┬───────┘      basada en k-meros frecuentes (identifica isoformas dominantes).
         │
         ▼
 ┌───────────────┐
 │   CHRYSALIS   │  --> Agrupa contigs con solapamientos y construye Grafos de de Bruijn
 └───────┬───────┘      separados para cada gen o familia génica.
         │
         ▼
 ┌───────────────┐
 │   BUTTERFLY   │  --> Procesa de forma paralelizada los grafos de de Bruijn individuales,
 └───────────────┘      rastreando caminos de lecturas para reconstruir transcritos completos
                        y todas sus isoformas alternativas.
```

### Ventajas del Ensamblado *De Novo*
* **Independencia Total de Referencia:** No depende de la existencia o calidad de un genoma de referencia, siendo idóneo para organismos no modelo.
* **Descubrimiento de Regiones Ausentes:** Permite identificar transcritos provenientes de regiones intergénicas, brechas (*gaps*) o loci no ensamblados en el genoma.

### Desventajas del Ensamblado *De Novo*
* **Alto Consumo de Recursos Computacionales:** Requiere servidores con gran memoria RAM (centenas de GB) para almacenar y simplificar los grafos de de Bruijn.
* **Alta Sensibilidad a Errores:** Errores de secuenciación pueden generar ramificaciones falsas en los grafos.
* **Requerimiento de Cobertura Elevada:** Se requieren profundidades de secuenciación de al menos **30X** por transcrito para garantizar la reconstrucción de transcripts completos.

---

## 🎯 Estrategia 2: Reconstrucción Basada en Genoma de Referencia

Cuando se dispone de un genoma de referencia de alta calidad, la reconstrucción del transcriptoma se realiza alineando primero las lecturas de RNA-Seq contra el genoma y posteriormente agrupando los alineamientos en modelos de transcritos.

### Algoritmos de Mapeo Empalmado (*Spliced Alignment*) y BWT
Debido a que las lecturas de mRNA maduro carecen de intrones, al mapearse contra el genoma de ADN genómico deben poder dividirse a través de los sitios de empalme (*splice junctions*). Herramientas modernas como HISAT2 o STAR utilizan índices optimizados basados en la **Transformada de Burrows-Wheeler (BWT)** y semillas de búsqueda (*FM-index*) para mapear miles de millones de lecturas de forma ultrarrápida.

### Ventajas de la Reconstrucción con Referencia
* **Eficiencia Computacional:** Es un proceso altamente paralelizable que requiere significativamente menos memoria RAM y tiempo de cómputo que el ensamblado *de novo*.
* **Tolerancia a Errores de Secuenciación:** El genoma de referencia actúa como ancla, reduciendo el impacto de errores de lectura aislados.
* **Sensibilidad para Transcritos de Baja Abundancia:** Permite identificar e inferir transcritos raros con coberturas bajas (desde **10X**).

### Desventajas de la Reconstrucción con Referencia
* **Dependencia Crítica de la Calidad del Genoma:** Errores, fragmentación o ausencias en el genoma de referencia limitan directamente la reconstrucción del transcriptoma.
* **Nivel de Variación Estructural:** Variantes genómicas grandes o genomas highly polimórficos pueden dificultar el alineamiento correcto de las lecturas.

---

## 🔀 Estrategia 3: Enfoques Híbridos y Comparación Técnica

Las estrategias híbridas combinan lo mejor de ambos mundos:
1. **Alinear y luego ensamblar lo no alineado:** Mapear las lecturas contra el genoma de referencia, recuperar las lecturas que no lograron alinearse (*unmapped reads*) y realizar un ensamblado *de novo* sobre este subconjunto para descubrir secuencias de transcritos novedosas o ausentes en la referencia.
2. **Ensamblar *de novo* y mapear los contigs:** Realizar un ensamblado *de novo* inicial y posteriormente alinear los contigs resultantes contra el genoma para validar su estructura exón/intrón.

### Tabla Comparativa de Estrategias

| Parámetro / Criterio | Ensamblado *De Novo* | Reconstrucción con Referencia | Enfoque Híbrido |
| :--- | :--- | :--- | :--- |
| **Dependencia de Genoma** | Ninguna (Organismos no modelo) | Alta (Requiere referencia de calidad) | Media / Complementaria |
| **Cobertura Requerida** | Alta (mínimo 30X) | Baja / Moderada (desde 10X) | Variable |
| **Recursos de Memoria RAM** | Muy Altos (Cómputo en Clúster/HPC) | Bajos / Moderados | Moderados |
| **Sensibilidad a Errores** | Alta | Baja | Moderada |
| **Detección de Isoformas** | Compleja (depende de de Bruijn) | Precisa (basada en empalmes) | Muy Alta |
| **Transcritos Novedosos** | Detecta todo el transcriptoma expresado | Limitado a loci genómicos presentes | Máxima detección global |

---

# <span id="practica-08"> Práctica 08 — Ensamblado de novo de transcriptomas (RNAseq) </span>

Esta práctica trabaja con un experimento de RNAseq compuesto por tres condiciones (Control, TreatmentX y TreatmentY), cada una secuenciada por triplicado (réplicas biológicas 01–03), en lecturas pareadas (R1/R2). Como no se cuenta con un genoma de referencia para esta especie, el flujo de trabajo consiste en: (1) preparar y concatenar las lecturas de alta calidad de todas las condiciones y réplicas en un único par de archivos R1/R2; (2) generar un ensamblado de novo del transcriptoma con **MIRA**; y (3) generar un segundo ensamblado de novo, con el mismo conjunto de datos, utilizando **Trinity**, para posteriormente poder comparar ambos resultados (unigenes) entre sí.

---

## Ejercicio 1 — Preparación de lecturas de alta calidad (1.HQReads)

Analice el tipo de archivos a utilizar (fastq) y asegúrese de tener el mismo número de secuencias en los archivos correspondientes de secuencias pareadas (R1 y R2). Recuerde que el experimento de RNAseq consta de tres condiciones (Control, TreatmentX y TreatmentY), cada una secuenciada por triplicado (réplicas biológicas 01–03).

Como ocurre en muchos experimentos de RNAseq correspondientes a especies que carecen de un genoma de referencia, los contigs (unigenes) resultantes del proceso de ensamblado de novo podrán ser considerados como tal. Teniendo en cuenta que este es el caso en nuestro ejercicio, para realizar el ensamblado se deben concatenar todas las secuencias/lecturas R1 en un único archivo, y hacer lo mismo para el caso de las lecturas R2. Asegúrese de que, tras realizar esta tarea, el orden de las secuencias R1 y R2 sea el mismo en ambos archivos.

```bash
cat ../1.HQReads/HQ_Control*_R1.fastq ../1.HQReads/HQ_TreatmentX*_R1.fastq ../1.HQReads/HQ_TreatmentY*_R1.fastq > HQ_AllReads_R1.fastq
```

```bash
cat ../1.HQReads/HQ_Control*_R2.fastq ../1.HQReads/HQ_TreatmentX*_R2.fastq ../1.HQReads/HQ_TreatmentY*_R2.fastq > HQ_AllReads_R2.fastq
```

Verifique que ambos archivos concatenados contienen el mismo número de secuencias:

```bash
grep -c "@NB501110" HQ_AllReads_R*.fastq
```

---

## Ejercicio 2 — Ensamblado de novo con MIRA (2.MiraAssembly)

Recordemos que algunos ensambladores, como es el caso de MIRA, permiten el uso de secuencias SE y PE. Se asume que las secuencias SE, en algunas ocasiones, pueden ser secuencias más largas, y es posible generarlas a partir de secuencias pareadas uniendo ambos extremos (R1 y R2). Esta tarea mejora el ensamblado y reduce los tiempos de cálculo; para hacer dicho ejercicio utilizaremos el programa **SeqPrep** (`SeqPrep.slurm`). Antes de ejecutar el trabajo (aproximadamente 5 min), analicemos las opciones a considerar en el mismo.

Como resultado se obtendrán secuencias SE (provenientes de la fusión de R1 y R2) y secuencias PE (todas aquellas que no encontraron una región de sobrelapamiento acorde con el umbral especificado). Analice los archivos de salida y los correspondientes mensajes en los archivos `*.e*` y `*.o*`.

Ya que a estas alturas usted está familiarizado con el uso del ensamblador MIRA (Prácticas anteriores), analice el archivo `manifest.conf` y la tarea correspondiente antes de ejecutar el archivo `.slurm`. Es posible que requiera descomprimir los archivos a utilizar.

Ejecutar esta tarea tomará aproximadamente 2.5 hrs; en caso de haber recursos disponibles, incremente el número de procesadores y la memoria para reducir los tiempos.

**Script `MiraAssembly.slurm`:**

```bash
#!/bin/sh
#SBATCH -J MiraAssembly
#SBATCH -n 8
#SBATCH -N 1
#SBATCH --mem 14G
#SBATCH -t 365-00
#SBATCH -e MiraAssembly.e%j
#SBATCH -o MiraAssembly.o%j
#SBATCH -p q1

module load q1/mira/4.0.2

time mira manifest.conf > log_assembly.txt
```

Una vez concluida la ejecución, analicemos los resultados.

---

## Ejercicio 3 — Ensamblado de novo con Trinity (3.TrinityAssembly)

Los archivos fastq a utilizar serán aquellos que se generaron tras el concatenado de todas las secuencias R1 y R2 (Ejercicio 1), y que también fueron utilizados para generar el ensamblado con MIRA (Ejercicio 2).

A diferencia del ensamblador MIRA y de algunos otros disponibles, Trinity utiliza siempre un único archivo de entrada R1 y/o R2, así que, en caso de múltiples bibliotecas, estas deben concatenarse siempre, como se hizo anteriormente. Tenga en cuenta que, para el caso del ensamblador MIRA, esta condicionante puede no ser necesaria.

Analice el contenido del script con la tarea a ejecutar (`TrinityAssembly.slurm`); puede también cargar el módulo de manera independiente en su línea de comando y solicitar el archivo de ayuda para ver más información sobre las opciones disponibles.

> **NOTA:** ejecute la tarea sin hacer uso de la opción `--normalize_reads`; esta opción hace que la tarea sea en ocasiones más lenta, pero, al simplificar el proceso de ensamblado, lo optimiza y muchas veces mejora el resultado (no siempre "más" es "mejor"). Compare el efecto de usar y no usar dicha opción: si bien podría significar un aumento en el tiempo de ejecución del proceso (debido a la normalización), simplifica el proceso de ensamblado. Ejecutar este ensamblado tomará aproximadamente 2.9 hrs.

**Script `TrinityAssembly.slurm`:**

```bash
#!/bin/sh
#SBATCH -J TrinityAssembly
#SBATCH -n 8
#SBATCH -N 1
#SBATCH --mem 200G
#SBATCH -t 365-00
#SBATCH -e TrinityAssembly.e%j
#SBATCH -o TrinityAssembly.o%j
#SBATCH -p q1

#TRINITY
#para q1:
module trinity/2.6.6/gcc/8.3.1-vykc

#para q2:
#module q2-trinity/2.6.6/gcc/9.1.0-e3an

time Trinity --seqType fq --max_memory 200G --left ../2.MiraAssembly/HQ_AllReads_R1.fastq --right ../2.MiraAssembly/HQ_AllReads_R2.fastq --CPU 8 --full_cleanup --normalize_reads
```

Al finalizar ambos ensamblados (MIRA y Trinity), compare el número de unigenes/contigs generados por cada aproximación, así como sus métricas de contigüidad, para discutir las ventajas y desventajas de cada ensamblador frente a este conjunto de datos de RNAseq.

---

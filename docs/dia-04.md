---
layout: default
title: "Día 04 · Ensamblaje de genomas"
---

<span class="eyebrow">Martes · 22 septiembre</span>

# Día 4: Algoritmos y Herramientas para el Ensamblado de Genomas de Novo

Bienvenid@s a la página de recursos del **Día 4** del curso **"Herramientas Bioinformáticas para el Análisis de Genomas y Transcriptomas"**. En esta jornada nos adentraremos en el núcleo del análisis genómico computacional: el ensamblado *de novo*. Exploraremos cómo reconstruir un genoma completo a partir de millones de lecturas cortas generadas por plataformas NGS, estudiando los fundamentos teóricos de los principales algoritmos y poniéndolos en práctica en el clúster de HPC con ensambladores de referencia como **Newbler** y **MIRA**.

---

## 🔬 Teoría: Conceptos Fundamentales de Ensamblado y Paradigmas Algorítmicos

### 1. La Jerarquía del Ensamblado Genómico
El proceso de ensamblado consiste en ordenar y orientar de manera lógica millones de fragmentos de secuenciación (*reads*) para reconstruir la estructura genómica original. Este flujo se organiza en una jerarquía de complejidad creciente:
*   **Lecturas (*Reads*):** Las secuencias individuales directas obtenidas del secuenciador.
*   **Contigs (Bloques Contiguos):** Secuencias continuas de ADN obtenidas al traslapar lecturas solapadas. No contienen huecos (*gaps*) de secuencia.
*   **Scaffolds (Andamios):** Estructuras creadas al ordenar y orientar diferentes contigs empleando información de distancias estimadas (como el tamaño del inserto en lecturas pareadas). Contienen huecos internos representados por caracteres `N`.
*   **Cromosomas:** La reconstrucción final y mapeada a escala cromosómica (pseudomoléculas).

```
Lecturas:     ───►   ───►   ───►   ───►
                      ▼ (Traslape continuo)
Contigs:      [==== Contig 1 ====]    [==== Contig 2 ====]
                      ▼ (Orientación con pares / distancias)
Scaffolds:    [==== Contig 1 ====]───N─N───[==== Contig 2 ====]
                      ▼ (Mapeo completo)
Cromosomas:   [==================== CROMOSOMA 1 ====================]
```

### 2. Paradigma 1: Algoritmos Codiciosos (*Greedy Algorithms*)
Constituyeron las primeras aproximaciones lógicas en la historia de la bioinformática para ensamblar secuencias.
*   **Lógica básica:** El algoritmo toma decisiones locales rápidas basadas en el "mejor de los escenarios evaluados en cada paso", lo que se traduce en seleccionar siempre el alineamiento por parejas (*pairwise alignment*) con el mayor puntaje de traslape.
*   **Limitaciones:** Aunque son sumamente rápidos y eficientes para genomas pequeños (como virus o plásmidos), se quedan atrapados con facilidad en óptimos locales causados por secuencias repetitivas. Finalizan su ejecución de forma abrupta cuando ya no es posible encontrar más traslapes y no garantizan la obtención de una secuencia consenso globalmente óptima.

### 3. Paradigma 2: Overlap-Layout-Consensus (OLC) y Grafos de Sobrelapado
Este paradigma fue diseñado originalmente para procesar lecturas largas generadas por tecnologías como Sanger. Su funcionamiento se basa en la teoría de grafos (donde los vértices o nodos representan las lecturas y las aristas o *edges* representan los traslapes detectados entre ellas). Se compone de tres fases:
1.  **Overlap (Sobrelapado):** Realiza un alineamiento cruzado masivo de todos contra todos (*all-vs-all pairwise alignment*) para identificar traslapes significativos entre lecturas.
2.  **Layout (Distribución):** Construye un grafo de sobrelapado y busca un **Camino Hamiltoniano**, el cual consiste en una secuencia lógica que recorre **cada nodo o lectura exactamente una y solo una vez**.
3.  **Consensus (Consenso):** Alinea las lecturas ordenadas del camino para deducir la secuencia nucleotídica consenso con mayor soporte estadístico.

*   **Ventajas y Desventajas:** Es computacionalmente muy pesado y difícil de escalar para millones de lecturas NGS cortas debido al costo del alineamiento *all-vs-all*. No obstante, es un método altamente paralelizable por contigs y ha resurgido con gran fuerza para procesar lecturas largas de tercera generación (como PacBio HiFi u Oxford Nanopore).

### 4. Paradigma 3: Grafos de de Bruijn (DBG) y k-meros
Desarrollados específicamente para lidiar de forma eficiente con el volumen masivo de lecturas cortas generadas por tecnologías NGS (como Illumina). En lugar de alinear lecturas completas, el algoritmo descompone cada lectura en sub-secuencias solapadas de tamaño fijo llamadas **k-meros**.
*   **Definición de k-mero:** Secuencias de nucleótidos de longitud fija $k$. Por ejemplo, para la secuencia `TAGATA` y un valor de $k = 4$, los k-meros generados serán: `TAGA`, `AGAT` y `GATA`.
*   **Estructura del Grafo:**
    *   Las **aristas** (*edges*) representan los k-meros únicos identificados en el set de datos.
    *   Los **nodos** flanqueantes representan los sub-k-meros de longitud $k-1$ (prefijos y sufijos), confiriendo direccionalidad al grafo.
    *   La reconstrucción del genoma se resuelve encontrando un **Camino Euleriano**, es decir, una secuencia que recorre **cada arista (k-mero) exactamente una y solo una vez**.

*   **Ventajas y Desventajas:** Elimina por completo el costoso paso de alineamiento masivo entre lecturas (*all-vs-all*) y evita redundancias en regiones de alta cobertura. Sin embargo, su robustez es sumamente sensible a los errores de secuenciación: una sola base errónea en una lectura puede crear hasta $k$ nodos y aristas falsas que ramifican y ensucian el grafo. De ahí surge la vital importancia de realizar un filtrado inicial riguroso de calidad en las lecturas.

### 5. Mecánica General de un Ensamblador moderno
Casi todos los ensambladores bioinformáticos incorporan algoritmos de postprocesamiento para limpiar los grafos construidos:
*   **Remoción de ramales ("dead-ends" o "tips"):** Eliminación de caminos cortos sin salida que se generan por errores en los extremos de las lecturas.
*   **Colapso de burbujas ("bubbles"):** Fusión de caminos paralelos redundantes generados por errores de secuenciación internos o variaciones alélicas (polimorfismos).
*   **Simplificación por lecturas pareadas:** Uso del tamaño promedio de inserto conocido de las librerías pareadas para desenredar caminos ambiguos y resolver regiones repetitivas del genoma.

---

# <span id="practica-01"> Práctica 02 — Ensamblado de Genomas (Newbler y MIRA) </span>

---

## Ejercicio 1 — Newbler: Ensamblado con coberturas 10X y 20X

La intención con este ejercicio es ensamblar un genoma bacteriano de aproximadamente 0.4 Mpb, utilizando para dicho fin coberturas (profundidad) de 10X y 20X, respectivamente.

El programa (ensamblador) a utilizar será Newbler v3.0, el cual fue inicialmente generado para ensamblar preferentemente datos generados con el pirosecuenciador 454 provenientes de bibliotecas tanto SE como mate-paired. Posteriormente dicho ensamblador fue optimizado para realizar ensamblados híbridos, utilizando también secuencias PE generadas con la plataforma Illumina y/o secuencias SE generadas con la plataforma PacBio, siempre y cuando estas no excedan una longitud de 30 Kpb.

Como input, los archivos pueden estar en formato .fasta, .fasta y .qual, y fastq.

Revise las características de las secuencias a utilizar para generar el ensamblado antes de realizar el mismo. Para tal propósito puede utilizar el script de perl provisto en su directorio de trabajo (`fastx-length.pl`). Dicho script fue descargado del repositorio GitHub: [https://github.com/gringer/bioinfscripts/blob/master/fastx-length.pl](https://github.com/gringer/bioinfscripts/blob/master/fastx-length.pl)

Genere un script que permita que el gestor de tareas (Slurm) envíe a la cola de trabajo dicho proceso, cargue el módulo y consulte el manual y/o la ayuda para realizar dicha tarea.

Una vez realizado el ensamblado se deberán discutir las diferencias de los resultados obtenidos. Si lo considera necesario, utilice de nueva cuenta el script `fastx-length.pl`.

**Script `runAssembly.slurm`:**

```bash
#!/bin/sh
#SBATCH -J runAssembly
#SBATCH -n 4
#SBATCH -N 1
#SBATCH --mem 32G
#SBATCH -t 0
#SBATCH -p q1
#SBATCH -e runAssembly.e%j
#SBATCH -o runAssembly.o%j

module load newbler/3.0/gcc/9.3.0-bypq

runAssembly -cpu 4 -o Assembly_v1.0 454ReadsCln10xA.fna

runAssembly -cpu 4 -o Assembly_v2.0 454ReadsCln10xA.fna 454ReadsCln10xB.fna
```

---

## Ejercicio 2 — Newbler: Ensamblado híbrido con distintos formatos y coberturas

En ocasiones, para generar (y mejorar) los ensamblados de genomas completos, se aprovechan las ventajas que ofrecen las diferentes plataformas de secuenciación. En su mayoría (aunque no en todos los casos) los ensambladores pueden combinar datos generados a partir de diferentes plataformas (ensamblados híbridos).

El siguiente ejercicio tiene como objeto demostrar que el formato de los archivos no tiene ninguna influencia en el resultado generado, no así la cobertura, la longitud y la calidad de las secuencias. Utilice los archivos empleados en el ejercicio anterior. Convierta únicamente uno de los sets de datos (454ReadsCln10xA o 454ReadsCln10xB) en un único archivo fastq. En la medida de lo posible, trate de evitar generar archivos redundantes en su directorio actual de trabajo.

```bash
conda activate qiime1-1.9.1
```

```bash
srun --mem 16G -n1 -p q1 convert_fastaqual_fastq.py -c fastaqual_to_fastq -f ../Ejercicio01/454ReadsCln10xA.fna -q ../Ejercicio01/454ReadsCln10xA.qual
```

```bash
ln -s ../Ejercicio01/454ReadsCln10xB.fna
ln -s ../Ejercicio01/454ReadsCln10xB.qual
```

Una vez realizado lo anterior, ejecute la tarea "runAssembly.slurm" utilizando una cobertura 20x (archivos A y B) y una cobertura 30x (archivos A, B y C). Compare los resultados con aquellos generados en el Ejercicio01.

**Script `runAssembly.slurm`:**

```bash
#!/bin/sh
#SBATCH -J runAssembly
#SBATCH -n 4
#SBATCH -N 1
#SBATCH --mem 32G
#SBATCH -t 0
#SBATCH -p q1
#SBATCH -e runAssembly.e%j
#SBATCH -o runAssembly.o%j

#q1 module
module load newbler/3.0/gcc/9.3.0-bypq

runAssembly -cpu 4 -o Assembly_v3.0 454ReadsCln10xA.fastq 454ReadsCln10xB.fna

runAssembly -cpu 4 -o Assembly_v4.0 454ReadsCln10xC.fna 454ReadsCln10xB.fna 454ReadsCln10xA.fastq
```

---

## Ejercicio 3 — MIRA: Ensamblado con el mismo set de datos

Utilizando el mismo set de datos del Ejercicio01 (optimizados como si provinieran de diferentes plataformas), genere un ensamblado, pero ahora utilizando el ensamblador MIRA. Tenga en cuenta que dicho ensamblador únicamente emplea archivos fastq como entrada.

Revise el script de Slurm y el archivo manifesto. Discuta lo necesario.

**Script `MiraAssembly.slurm`:**

```bash
#!/bin/sh
#SBATCH -J MiraAssembly
#SBATCH -n 4
#SBATCH -N 1
#SBATCH --mem 40G
#SBATCH -t 0
#SBATCH -e MiraAssembly.e%j
#SBATCH -o MiraAssembly.o%j
#SBATCH -p q1

module load q1/mira/4.0.2

mira manifest.conf > log_assembly.txt
```
---

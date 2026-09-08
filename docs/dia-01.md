---
layout: default
title: "Día 01 · Introducción y fundamentos"
---

<span class="eyebrow">Jueves · 17 septiembre</span>

---

# 🖥️ Día 1: Introducción y Fundamentos del Curso

Bienvenid@ al espacio de recursos del **Día 1** del curso **"Herramientas Bioinformáticas para el Análisis de Genomas y Transcriptomas"**. Este espacio ha sido diseñado para centralizar la información logística, los fundamentos teóricos de las ciencias ómicas, los conceptos de infraestructura de cómputo y la guía de inicio rápido en la terminal de UNIX/Linux.

---

### 📅 1. Información General y Logística

El curso de Herramientas Bioinformáticas para el Análisis de Genomas y Transcriptomas está coordinado por el **Dr. Enrique Ibarra Laclette** y el **M. en C. Emanuel Villafán de la Torre**, y está dirigido a estudiantes y académicos que busquen incorporar el análisis informático masivo en sus proyectos de investigación.

*   **Fechas de la Jornada:** Del 17 de septiembre al 01 de octubre de 2026.
*   **Horas de Dedicación:** 8 horas diarias de trabajo intensivo.
*   **Idioma Oficial:** Español.
*   **Cupo Máximo:** 20 participantes.
*   **Sede de Impartición:** Instituto de Ecología A.C. (INECOL), Salón BioMimic, Segundo Piso, Edificio B, Campus 3.
*   **Equipo de Instructores:**
    *   Dr. Enrique Ibarra Laclette
    *   M. en C. Emanuel Villafán de la Torre
    *   Dra. Diana Hernández Oaxaca
    *   Dr. Michel Pale Rivas
    *   *Ayudante del Curso:* Andrea Iridiana Barraza Ochoa

### 📊 Mecanismo de Evaluación
Para acreditar de manera satisfactoria este curso, se empleará un esquema continuo basado en el desempeño diario y la entrega de prácticas:
1.  **Asistencia y participación activa:** 20%
2.  **Ejercicios prácticos desarrollados en cada sesión:** 40%
3.  **Evaluaciones parciales:** 40%

---

### 🌎 2. Genómica y Transcriptómica en la Era Ómica

La biología clásica se ha visto profundamente transformada por los **desarrollos tecnológicos de secuenciación de siguiente generación (NGS)**. Esta revolución tecnológica nos ha forzado a transitar de una visión local (análisis de genes individuales) a una **visión global** de los fenómenos biológicos, caracterizada por un **gran volumen de datos** y una **mayor complejidad** en su análisis e interpretación. Así nacen las **Ciencias Ómicas**.

### A. ¿Qué es el Genoma?
En el contexto de la genómica, definimos al **Genoma** como la secuencia nucleotídica completa contenida en un juego de cromosomas de un organismo. Este plano de información genética está integrado estructuralmente por:
*   **Genes:** Regiones codificantes de proteínas y ARN funcionales.
*   **Elementos Reguladores:** Secuencias responsables de coordinar la expresión de los genes.
*   **Secuencias Repetitivas:** Elementos repetitivos acumulados a lo largo de la evolución de la especie.

### B. El Enigma del Tamaño y la Paradoja del Valor C
El tamaño de los genomas es extraordinariamente variable en el mundo vivo. Por ejemplo, mientras que el genoma de *Homo sapiens* posee aproximadamente **3,200 Mb** [8], plantas como *Pinus lambertiana* (pino de azúcar) cuentan con genomas gigantescos de **27,602 Mb** y *Picea glauca* (abeto blanco) con **24,633 Mb**.

A pesar de esta abismal diferencia en tamaño físico, un genoma gigante no equivale a un mayor número de genes o a una mayor complejidad biológica. Esta discordancia se conoce como la **Paradoja del Valor C**. Los estudios a gran escala revelan que:
*   Los genomas más grandes contienen **proporcionalmente menos genes codificantes** de proteínas.
*   El tamaño del genoma eucariota escala de manera directa con el porcentaje de **elementos transponibles** (secuencias repetitivas) que posee, y no con su contenido génico.

```
Genoma Humano (3.2 Gb):      🧬 [== GENES ==][====== TRANSPOSONES ======]
Genoma de Pinus (27.6 Gb):   🧬 [== GENES ==][======================== TRANSPOSONES ========================]
```

### C. Organización Genómica: Procariotas vs. Eucariotas
*   **Genomas Procariotas:** Bacterias y arqueas poseen genomas compactos caracterizados por una alta densidad de genes. Sus características clave son:
    *   **Operones Policistrónicos:** Agrupaciones de regiones codificantes coordinadas bajo el control de un único promotor común.
    *   **Plásmidos:** Moléculas de ADN extracromosómico circular que codifican para funciones accesorias adaptativas de gran importancia evolutiva, como la resistencia a antibióticos, la patogenicidad o el metabolismo de sustratos específicos.
    *   **Transferencia Horizontal de Genes (HGT):** Intercambio directo de material genético entre organismos independientes, acelerando la evolución y adaptación procariota.
*   **Genomas Eucariotas:** Su organización es mucho más compleja, fraccionando la secuencia de los genes en regiones codificantes (**exones**) e intermedias no codificantes (**intrones**), y estando los cromosomas lineales altamente empaquetados por histonas.

### D. El Transcriptoma: De las Ómicas a la Función
Mientras que el genoma representa la biblioteca estática de posibilidades de un organismo, el **Transcriptoma** representa el estudio global de los patrones de expresión de ARN en un tejido, momento o condición ambiental específica. El transcriptoma actúa como el puente metodológico clave para conectar la secuencia de ADN con la función celular y fisiológica activa ("de las ómicas a la función").

---

### 💻 3. Cómputo de Alto Rendimiento (HPC) y Bioinformática

Para abordar el procesamiento de gigabytes de datos provenientes de plataformas NGS, la biología clásica recurre a la bioinformática y al cómputo científico.

### Glosario de Conceptos de Cómputo
*   **Biología Computacional:** Área dedicada al uso y desarrollo de herramientas, modelos matemáticos, simulación y algoritmos con el objetivo de entender los sistemas biológicos.
*   **Bioinformática:** Subdisciplina enfocada en la curación, análisis, procesamiento y manipulación de los datos biológicos masivos generados por las ciencias ómicas.
*   **Flujo de Trabajo (Pipeline):** Cadena de programas informáticos conectados secuencialmente. Se divide en tres fases críticas: **Preprocesamiento** (filtrado y control de calidad), **Procesamiento** (alineamiento o ensamble) y **Postprocesamiento** (anotación, análisis estadístico e interpretación). La salida de un programa se convierte directamente en la entrada del siguiente.
*   **Proceso Serializado vs. Paralelizado (Multithreading):**
    *   *Serializado:* Ejecuta las tareas de una en una, de forma secuencial, utilizando un único núcleo (*core*) de procesamiento.
    *   *Paralelizado / Multithreading:* Divide el problema complejo en subproblemas y los ejecuta de manera simultánea distribuyéndolos en múltiples *cores*.
*   **Cómputo de Alto Rendimiento (HPC):** Infraestructura computacional robusta (clúster de servidores) equipada con gran capacidad de memoria RAM, almacenamiento y procesadores optimizados para realizar cómputo paralelo masivo.
*   **Nodo de Procesamiento:** Un servidor de cómputo individual que forma parte del clúster de HPC, el cual cuenta con sus propios recursos físicos de CPU, memoria RAM y almacenamiento.
*   **Administrador de Trabajos (Scheduler):** Software encargado de coordinar la cola de solicitudes de los usuarios en el HPC, distribuyendo de manera óptima los recursos solicitados (cores, RAM, tiempo) y asignando los trabajos a nodos específicos de procesamiento.

---

### 🐚 4. Fundamentos de la Shell de UNIX

La gran mayoría de los paquetes de software especializados en bioinformática carecen de una interfaz gráfica de usuario (GUI). Para utilizarlos, es indispensable interactuar directamente con la **Shell de UNIX/Linux** mediante una **Línea de Comandos**. 

### El Sistema Operativo GNU/Linux
*   **GNU/Linux:** Es un sistema operativo de libre distribución (Open Source), basado en UNIX, que integra el Kernel desarrollado por Linus Torvalds con las herramientas y compiladores provistos por el proyecto GNU.
*   **Kernel (Núcleo):** La porción más interna del sistema operativo que sirve de puente de comunicación directa entre el software de aplicación y los componentes físicos (hardware) de la máquina.
*   **Shell (Intérprete de Comandos):** El programa que actúa como interfaz interactiva entre el usuario y el sistema operativo. La shell lee los comandos escritos por el usuario en la terminal y ordena su ejecución al kernel. La shell más extendida y la que usaremos en el curso es **BASH** (Bourne-Again Shell).

```
           ┌───────────────────────────────────────────────┐
           │                  USUARIO                      │
           └───────────────────────┬───────────────────────┘
                                   ▼
           ┌───────────────────────────────────────────────┐
           │      SHELL: Interfaz Intérprete (BASH)        │
           └───────────────────────┬───────────────────────┘
                                   ▼
           ┌───────────────────────────────────────────────┐
           │      KERNEL: Administrador de Hardware        │
           └───────────────────────┬───────────────────────┘
                                   ▼
                [ CPU ]  [ Memoria RAM ]  [ Almacenamiento ]
```

### 📂 5. Guía de Referencia y Sintaxis de Comandos Básicos

Para interactuar de manera eficiente con el **Sistema de Archivos** (el cual organiza nuestros datos de forma jerárquica en archivos y directorios), debemos dominar la sintaxis de la línea de comandos.

### Sintaxis Estándar de la Terminal
```bash
comando [-opciones] [argumentos]
```
*   **Comando:** La instrucción específica que le solicita al intérprete (BASH) realizar una tarea en el host.
*   **Opciones:** Modificadores que alteran o amplían el comportamiento por defecto de un comando. Inician de manera obligatoria con un guion corto (`-` para opciones de una letra) o doble guion (`--` para opciones de palabras completas).
*   **Argumentos:** Indican al comando sobre qué elemento específico (un archivo, una ruta, un texto) debe recaer la acción.

### Comandos de Navegación Esenciales
*   `pwd` (Print Working Directory): Imprime en pantalla la ruta completa del directorio de trabajo actual donde nos encontramos posicionados dentro de la terminal.
*   `ls` (List): Enlista de forma alfabética los archivos y subcarpetas contenidos en el directorio actual.
    *   `ls -F`: Añade un carácter indicador al final del nombre para diferenciar el tipo de archivo (p. ej., una diagonal `/` para indicar carpetas).
    *   `ls -l`: Muestra el contenido detallado en formato de lista larga, incluyendo permisos, propietario, tamaño y fecha de modificación.
    *   `ls --help` o `ls -h`: Despliega el manual de ayuda rápida y las opciones disponibles para el comando.
*   `cd [ruta]` (Change Directory): Permite cambiar el directorio de trabajo actual a la ruta especificada.

### Atajos de Navegación en UNIX
La Shell cuenta con atajos predefinidos que facilitan el movimiento rápido a través del árbol jerárquico de directorios:
*   `.` : Representa al **directorio actual** en el que estás posicionado.
*   `..` : Representa al **directorio padre** (sube un nivel en la estructura).
*   `~` : Apunta directamente al **directorio personal** (*home directory*) del usuario activo.
*   `-` : Te regresa instantáneamente al **directorio de trabajo anterior** en el que te encontrabas posicionado antes de tu último `cd`.

```
                     ┌───────────────────┐
                     │   Raíz: '/'       │
                     └─────────┬─────────┘
                              ▼
                     ┌───────────────────┐
                     │   '/Users'        │
                     └────────┬──────────┘
                              ▼
                     ┌───────────────────┐
                     │ '/Users/bio'      │  <─── Directorio Home ('~')
                     └────────┬──────────┘
                              ▼
                     ┌───────────────────┐
                     │ '/Users/bio/data' │  <─── Posición actual (pwd)
                     │                   │       Si haces 'cd ..' vas a '/Users/bio'
                     └───────────────────┘
```

### Rutas Absolutas vs. Rutas Relativas
Para indicarle al sistema la ubicación de un elemento en el disco, podemos emplear dos tipos de rutas:
1.  **Rutas Absolutas:** Describen la ubicación inequívoca de un archivo o carpeta partiendo obligatoriamente desde el directorio raíz (`/`) del sistema de archivos. No importa dónde estés parado, una ruta absoluta siempre funciona igual.
    *   *Ejemplo:* `/Users/bio/data/proteina.txt`
2.  **Rutas Relativas:** Describen la ubicación de un elemento tomando como punto de partida de referencia tu posición (*working directory*) actual. Nunca inician con una diagonal raíz `/`.
    *   *Ejemplo:* `data/proteina.txt` o `../backup/archivo.zip`

---

[← Volver a la portada](./)

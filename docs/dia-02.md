---
layout: default
title: "Día 02 · Nociones generales de los genes y genomas"
---

<span class="eyebrow">Viernes · 18 septiembre</span>

# Día 2: Nociones generales de los genes y genomas; Linux Avanzado.

Bienvenidos a la página de recursos del **Día 2** del curso **"Herramientas Bioinformáticas para el Análisis de Genomas y Transcriptomas"**. En esta jornada profundizaremos en cómo los eventos evolutivos moldean la arquitectura de los genomas complejos y avanzaremos en el dominio de la terminal de Linux para la organización segura de proyectos bioinformáticos.

---

### Unidad 1: Evolución de Genomas Complejos y Poliploidía

Para interpretar correctamente los ensamblajes bioinformáticos, debemos comprender las fuerzas evolutivas que estructuran los genomas eucariotas, particularmente en plantas, donde los genomas sufren cambios drásticos en tamaño y contenido génico.

### 1. Poliploidía (Duplicación del Genoma Completo - WGD)
La poliploidía es un evento evolutivo recurrente caracterizado por la duplicación del set completo de cromosomas de un organismo. Existen dos mecanismos principales:
*   **Autopoliploidía:** Ocurre por la duplicación del genoma dentro de una sola especie, frecuentemente debido a la fusión de gametos no reducidos (que contienen el doble de la carga cromosómica normal). Un autotetraploide resultante posee cuatro copias homólogas de cada cromosoma de su especie parental.
*   **Alopoliploidía:** Se origina mediante la hibridación entre dos especies distintas, seguida de una duplicación cromosómica. El alotetraploide resultante combina dos juegos de cromosomas homólogos diferentes (provenientes de cada parental).

### 2. Diploidización y Fraccionamiento Genómico
Posterior a un evento de duplicación del genoma completo, los organismos atraviesan un proceso evolutivo conocido como **diploidización**, durante el cual el genoma duplicado tiende a regresar funcional y estructuralmente a un estado diploide estable. Las consecuencias moleculares clave son:
*   **Fraccionamiento:** Pérdida masiva y paulatina de genes homólogos duplicados a lo largo del tiempo.
*   **Reorganización Cromosómica:** Reordenamientos que pueden fragmentar y fusionar cromosomas redundantes.

### 3. Sintenia Genómica
La **sintenia** es la conservación del orden de los genes (co-linealidad) entre diferentes cromosomas dentro del mismo genoma (sintenia intra-genómica, reflejo de duplicaciones antiguas) o entre genomas de especies distintas (sintenia inter-genómica). La comparación de sintenia utilizando grupos externos filogenéticos que carecen de duplicaciones recientes permite reconstruir la historia evolutiva y los eventos de poliploidía de un linaje.

---

### 💻 Unidad 2: Práctica de Linux II (Organización y Seguridad)

En esta práctica avanzamos más allá de la navegación básica para aprender a organizar directorios jerárquicos complejos y manipular datos con seguridad.

### 1. Creación Jerárquica de Carpetas
Para proyectos grandes, es fundamental crear estructuras organizadas de directorios. El comando `mkdir` cuenta con una opción potente:
*   `mkdir -p [ruta/de/directorios]`: Crea una ruta completa de subdirectorios, generando las carpetas padre automáticamente si no existen previamente.

> **Ejemplo práctico de Live Coding:**
> ```bash
> mkdir -p ~/analisis_genoma/resultados/anotacion
> ```
> *Resultado:* Se crea la carpeta `analisis_genoma`, dentro de ella `resultados`, y en su interior `anotacion` con un solo comando.

### 2. Edición y Creación de Archivos Vacíos
*   `touch [archivo]`: Crea un archivo de texto vacío o actualiza la fecha de modificación de uno existente.
*   Para escribir o editar scripts en la terminal, utilizaremos editores interactivos integrados en la consola como `nano` o `vim`.

### 3. Copiado y Movimiento Seguro
*   `cp [origen] [destino]`: Copia un archivo. Si deseas copiar un directorio completo con todo su contenido, debes usar la opción recursiva `cp -r`.
*   `mv [origen] [destino]`: Mueve o renombra un archivo o directorio en el sistema.

### 4. Borrado Definitivo y Preventivo
En Linux, la eliminación de archivos mediante la terminal es **permanente e irreversible**. No existe una papelera de reciclaje.
*   `rm [archivo]`: Elimina un archivo permanentemente.
*   `rm -r [directorio]`: Elimina un directorio y todo su contenido de forma recursiva.
*   ⚠️ **Práctica de Seguridad Obligatoria:** Utiliza siempre la opción interactiva `rm -i` o `rm -ri`. El sistema te preguntará y requerirá confirmación explícita (`y`/`n`) antes de borrar cada elemento, previniendo la pérdida accidental de datos crudos valiosos.

---

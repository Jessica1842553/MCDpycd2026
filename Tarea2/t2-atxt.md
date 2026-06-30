## **Análisis de Texto** 
### Guiones de los episodios piloto ($1 \times 01$) de Malcolm in the Middle vs. Modern Family.

### - Objetivo:
Analizar y comparar la estructura lingüística y los rasgos estilísticos de dos producciones televisivas icónicas: **Malcolm in the Middle** y **Modern Family**. Se busca contrastar el ritmo, intensidad y riqueza de la diferente comedia familiar de cada una.

---

## 1. Segmentación Temporal y Evolución de Bloques
Se dividió el episodio correspondiente en cuatro bloques equivalentes de diálogos para simular la estructura cronológica clásica de la narrativa televisiva (Acto 1, Acto 2, Acto 3 y Clímax).  
Mediante el uso de agrupaciones `.groupby()` y conteos únicos `.nunique()`, se observó la fluctuación de la diversidad léxica a lo largo de los episodios.

La gráfica de barras horizontales nos mostró que Modern Family mantiene de manera consistente una mayor cantidad de palabras únicas en cada una de las cuatro etapas del episodio en comparación con Malcolm in the Middle.  
Malcolm se estabiliza en un rango de entre 210 y 230 palabras distintas por bloque, Modern Family muestra un pico de variedad en los actos intermedios (Bloques 2 y 3 con más de 260 palabras únicas). 

Esto estadísticamente comprueba que la estructura multi-trama de Modern Family exige un flujo constante y renovado de vocabulario conforme se salta de una familia a otra, a diferencia del desarrollo lineal de Malcolm.

---

## 2. Similitud Coseno Vectorial
Utilizando las funciones de distancia espacial distribuidas en la librería `scipy.spatial.distance`, se vectorizaron las distribuciones totales de frecuencia de las series en una matriz cruzada para medir su Similitud Coseno, obteniendo los siguientes indicadores:

- **Distancia de Coseno:** 0.3586
- **Similitud Coseno (Léxica):** 0.6414 (**64.14%** de coincidencia)

Un nivel de similitud del 64.14% refleja una coincidencia léxica notable entre ambos textos moderadamente alto. A pesar de las diferencias temporales (década de los 2000 vs. 2010) y de formato, ambas producciones comparten una base semántica común muy sólida.  
Esto se justifica porque ambas subvierten el mismo subgénero (*sitcom* familiar), lo que las obliga a recurrir a un núcleo idéntico de términos vinculados a las relaciones parentales, la cotidianidad del hogar y los conflictos domésticos.

---

## 3. Análisis de Sentimiento vía Léxico Supervisado (AFINN)
Se implementó un análisis de sentimiento basado en el léxico lexicográfico AFINN-165 a partir de cruces relacionales del tipo `inner join` para evaluar la carga emocional de los diálogos de los pilotos.

| Métrica Emocional | Malcolm in the Middle | Modern Family |
| :--- | :---: | :---: |
| **Carga Positiva** | **67.57%** | 59.84% |
| **Carga Negativa** | 32.43% | **40.16%** |
| **Puntuación Promedio** | **0.605** | 0.389 |

Los resultados contradicen la hipótesis intuitiva de que el guion de *Malcolm* reflejaría una mayor negatividad por el tono disfuncional de la serie. *Malcolm in the Middle* presenta un promedio de sentimiento significativamente más alto (0.605) y una mayor concentración de palabras positivas (67.57%). 
  
Se descubre que el piloto de *Modern Family* basa su comedia en la incomodidad, la frustración parental y el conflicto sutil (reflejado en el 40.16% de carga negativa). En contrapolo, el guion de *Malcolm* utiliza términos de alta energía, asombro y descripciones entusiastas para introducir su universo al espectador, lo que sesga positivamente la métrica del diccionario de sentimientos.

---
Puntos 7, 8 y 9 del código: [Tarea2_PCD](Tarea2/Tarea2_PCD.ipynb)
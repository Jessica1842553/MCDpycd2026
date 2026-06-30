## **Análisis de Texto**
### Diseño de experimentos para comparar modelos y sus hiperparámetros con relación a la clasificación de textos.

---

### 1. Descripción y Origen de los Datos

Se extrajo una muestra controlada de una fuente académica **20 Newsgroups**, distribuido oficialmente a través de la librería `sklearn.datasets` mediante la función `fetch_20newsgroups`.

### 1.1. Características de los Datos
Este conjunto de datos está compuesto por una colección de aproximadamente 20,000 documentos de foros de discusión (Newsletters/Usenet) divididos en 20 temáticas distintas.  
Para este diseño de experimentos binario, se aislaron exclusivamente dos categorías con identidades semánticas y vocabularios técnicos altamente competitivos:

1. **`rec.autos` (Clasificada como 'autos'):** Mensajes y discusiones enfocados en especificaciones automotrices, mecánica, compra/venta de vehículos y rendimiento de motores.
2. **`sci.space` (Clasificada como 'space'):** Mensajes enfocados en ciencias del espacio, misiones de la NASA, órbitas, ingeniería aeroespacial y astronomía.

---

### 2. Distribución Estadística de los Datos
Para asegurar un análisis transparente y mitigar el ruido estadístico ajeno al lenguaje, se activaron los parámetros `remove=('headers', 'footers', 'quotes')`.  
Esto eliminó de forma automática los metadatos de los correos (remitentes, líneas de asunto), las firmas de pie de página y las respuestas citadas, dejando estrictamente el cuerpo de texto crudo redactado por los usuarios.

Tras realizar una limpieza inicial de registros que quedaron completamente vacíos debido a dicha eliminación, la distribución final de los datos quedó perfectamente balanceada de la siguiente manera:

* **Clase `space` (Ciencias del Espacio):** 955 documentos (50.48%)
* **Clase `autos` (Automovilismo):** 937 documentos (49.52%)
* **Volumen Total:** 1,892 observaciones textuales.

---

### 3. Resultados del Diseño de Experimentos
Detalles acerca del comportamiento de las 12 configuraciones experimentales evaluadas mediante la interacción de las cuatro metodologías de vectorización y los tres niveles del hiperparámetro de regularización $C$:

### 3.1. Análisis por Estrategia de Vectorización

#### A. Estrategia: Conteo Simple
- **Hiperparámetro C = 0.1 y 1.0:** Alcanzan una exactitud idéntica de **94.20%**. La matriz de confusión demuestra una alta simetría, clasificando correctamente 185 textos de automovilismo y 172 de ciencias del espacio.
- **Hiperparámetro C = 10.0:** La exactitud disminuye a **91.03%**. Al reducirse la regularización, el modelo comenzó a sobreajustarse a términos ruidos o muy específicos de los datos de entrenamiento, lo que elevó las falsas alarmas (19 textos de autos clasificados erróneamente como espacio).

#### B. Estrategia: TF-IDF a Nivel Palabra
- **Hiperparámetro C = 1.0:** Representa el *punto de equilibrio óptimo del experimento*, alcanzando la máxima exactitud global de **94.72%**. El modelo minimiza de forma crítica el error de omisión (Falsos Negativos = 5), demostrando una sensibilidad superior para aislar los patrones léxicos de la temática espacial.
- **Hiperparámetro C = 10.0:** Mantiene un rendimiento competitivo del **94.46%**, aunque con una ligera penalización en la clasificación de la categoría espacial.

#### C. Estrategia: TF-IDF a Nivel N-Gramas
- **Hiperparámetro C = 0.1:** Se identificó un fenómeno severo de *subajuste* con una exactitud de apenas **53.30%**. La matriz de confusión revela que la fuerte penalización del modelo, sumada a la dispersión de los rangos de n-gramas (2,3), provocó que el algoritmo asignara casi la totalidad de las observaciones (177) a la predicción de la clase espacial.
- **Hiperparámetro C = 1.0 y 10.0:** El rendimiento se recupera escalando a un **87.34%** y **88.39%** respectivamente, lo que comprueba que los n-gramas requieren un margen de flexibilidad ($C$ más alto).

#### D. Estrategia: TF-IDF a Nivel Caracteres
- Esta estrategia obtuvo los rendimientos más estables pero bajos del experimento, oscilando entre **67.28% y 70.71%**. El análisis evidencia que la frecuencia e interconexión de caracteres individuales es insuficiente para discriminar discusiones temáticas de texto largo.

---

### 4. Conclusión

El diseño de experimentos demuestra de forma estadística que el éxito en el procesamiento de lenguaje natural no depende únicamente de la complejidad del vectorizador. Mientras que los n-gramas y los caracteres fallan en capturar de forma eficiente la semántica de las discusiones de los foros, la vectorización clásica por **TF-IDF Palabras** tiene una superioridad al ponderar correctamente la relevancia de los tecnicismos de cada categoría. 

---
[Código](Tarea3_PCD.ipynb)
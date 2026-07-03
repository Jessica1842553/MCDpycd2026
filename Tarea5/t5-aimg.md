## **Análisis de imágenes** 
### Procesamiento de imágenes

---

## 1. Conjunto de Datos

El conjunto de datos seleccionado para este experimento es el dataset oficial **Malaria**, disponible de manera nativa a través del repositorio de la API de `tensorflow_datasets` (TFDS).

### 1.1. Distribución y Balanceo de Clases
El dataset total está compuesto por **27,558 imágenes individuales de células**, divididas equitativamente en dos clases biológicas:

1. **Clase 0: Parasitized (Infectada):** Células que contienen el parásito *Plasmodium falciparum* en alguna de sus etapas de desarrollo. Visualmente se caracterizan por presentar pequeñas manchas o anillos densos de color morado/azul brillante en su citoplasma debido a la tinción de Giemsa.
2. **Clase 1: Uninfected (Sana / Normal):** Eritrocitos completamente limpios, con una textura y coloración rosada/rojiza homogénea, sin cuerpos extraños internos.

Se extrajo un subconjunto estricto y controlado del dataset original:
- **Subset de Entrenamiento:** 400 micrografías digitales.
- **Subset de Validación:** 100 micrografías digitales.

## 2. Análisis y Discusión de Resultados

El modelo secuencial implementado bajo la metodología de Transfer Learning utilizando VGG16 arrojó un comportamiento eficiente y estable, corrigiendo los errores matemáticos y la volatilidad de los gradientes de fases previas.

### A. Eficiencia Paramétrica
Al establecer conceptualmente la propiedad `base_model.trainable = False`, se congelaron 14,714,688 parámetros correspondientes a los extractores de características primitivas de VGG16. Esto permitió restringir el entrenamiento estocástico a únicamente 2,097,665 parámetros acoplados en el clasificador densamente conectado. 

### B. Diagnóstico de la Convergencia y Curvas de Aprendizaje
Al analizar las representaciones gráficas resultantes, se identifican fenómenos analíticos de gran valor teórico:

1. **Efecto del Conocimiento Transferido (Época 0 a 1):** Durante la primera transición de épocas, se aprecia la métrica `accuracy` en entrenamiento se eleva exponencialmente de 52.75% a 77.50%, mientras que la función de pérdida decrece de 1.08 a 0.47. Este comportamiento valida la efectividad de los pesos iniciales de *ImageNet*, los cuales proveen al sistema filtros pre-configurados que aceleran la identificación de estructuras celulares.
2. **Estabilización de la Función de Pérdida (`Loss`):** La pérdida de validación (`val_loss`, curva naranja) tiende a estabilizarse de forma óptima en un umbral de [0.41 - 0.45] a partir de la tercera época. El hecho de que la curva no suba confirma que se eliminó el sobreajuste grave.
3. **Brecha de Varianza Controlada:** La diferencia observada entre el `accuracy` de entrenamiento (~94%) y el de validación (~77%) es un comportamiento esperado debido a la restricción en el volumen del subset de datos empleado (400 muestras de entrada). A pesar de esta ligera varianza, el modelo manifiesta una capacidad de generalización aceptable para entornos de diagnóstico médico simulados.

### 4. Conclusión
La estrategia de Transfer Learning con VGG16 representa una solución óptima y balanceada para diferentes tareas, como en este caso de clasificación biomédica donde los recursos computacionales y el volumen de muestras son limitados.
---

- [Código](Tarea5_PCD.ipynb)
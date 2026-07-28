## Procesamiento de Audio

### 1. Transformada Wavelet Discreta (DWT)
A diferencia de la Transformada de Fourier, la **DWT con la familia Daubechies (`db1` / Haar)** nos permite descomponer la señal de audio en diferentes niveles de resolución temporal y frecuencial:
- **Coeficientes de Aproximación ($c_A$):** Capturan las bajas frecuencias y la **envolvente fonética** principal de la voz (el contorno del sonido al decir *"zero"* o *"one"*).
- **Coeficientes de Detalle ($c_D$):** Capturan altas frecuencias y variaciones rápidas (ruido o consonantes sibilantes).

Para esta prueba, seleccionamos los coeficientes de aproximación del nivel 4 ($c_{A4}$), reduciendo la dimensión del audio sin perder la estructura morfofonética.

### 2. Clasificación mediante Dynamic Time Warping (DTW)
El algoritmo **DTW** calcula la distancia mínima y la alineación óptima no lineal entre dos secuencias temporales que pueden variar en velocidad o duración.

---

## Justificación Técnica: La Importancia de la Normalización

Se aplicó una **normalización L-infinito** a las señales en el dominio del tiempo antes de la descomposición Wavelet:

$$\hat{x}[n] = \frac{x[n]}{\max(|x[n]|)}$$

**Efectos en la clasificación:**
1. *Invariancia al volumen:* Se eliminó la dependencia de la potencia del micrófono o la cercanía del locutor.
2. *Comparación morfológica pura:* El algoritmo DTW pasó a evaluar exclusivamente el contorno fonético y la duración de la sílaba.
3. *Resultado:* La distancia hacia la Muestra A (`'0'`) se redujo significativamente respecto a la Muestra B (`'1'`), logrando una predicción correcta y robusta.

---

## Conclusiones
* La combinación de **Wavelet (Aproximación Level 4) + Normalización + DTW** permite construir un reconocedor de voz aislado eficiente sin necesidad de entrenar redes neuronales complejas.
* Se demostró experimentalmente que el procesamiento previo de la señal (pre-procesamiento de amplitud) es igual o más crítico que la elección del algoritmo de distancia.

---
- [Código](Tarea7_PCD.ipynb)
# Procesamiento de Audio: Intros de Series

## 1. Introducción
Se seleccionaron como casos de estudio dos series con estructuras de producción opuestas: el tema principal de *Game of Thrones* (representativo del género dramático/orquestal) y un intro típico de *The Big Bang Theory* (representativo del género de comedia/pop). 

---

## 2. Visualización en el Dominio del Tiempo

### 2.1. Análisis de Envolvente Dinámica (Waveshow)
A través de la función `librosa.display.waveshow`, se analizaron las formas de onda de ambas señales. Los resultados demuestraron una clara divergencia en sus envolventes de amplitud:
- **The Big Bang Theory:** Presenta una onda homogéneamente saturada desde los primeros vectores temporales, una estrategia de producción diseñada para capturar la atención inmediata del espectador mediante transitorios de alta energía.
- **Game of Thrones:** Exhibe una envolvente dinámica creciente, reflejando una acumulación dramática y una dosificación de la tensión instrumental a lo largo del tiempo.

---

## 3. Análisis Espectral y Distribución de Masa Frecuencial

### 3.1. Transformada de Fourier de Corto Tiempo (STFT)
Mediante el cálculo de la STFT y su posterior conversión a la escala logarítmica de decibelios, se obtuvieron los espectrogramas logarítmicos de frecuencia. 
- El espectrograma de *Game of Thrones* reveló una densidad armónica masiva concentrada en las bandas inferiores (por debajo de los $512\text{ Hz}$).
- Por el contrario, el espectrograma de *The Big Bang Theory* exhibió una clara dispersión hacia las bandas superiores, con componentes activos por encima de los $4096\text{ Hz}$ producto de guitarras acústicas/eléctricas y sintetizadores agudos.

---

## 4. Interpretación Computacional del Centroide Espectral

- **Game of Thrones ($\mu = 1325.89\text{ Hz}$):** Este valor matemático confirma analíticamente una concentración de energía en el espectro de frecuencias bajas y medias-bajas, validando la predominancia de arreglos orquestales densos.
- **The Big Bang Theory ($\mu = 2622.35\text{ Hz}$):** El centroide se desplaza de manera contundente hacia el espectro de frecuencias medias-altas, duplicando la frecuencia de la muestra dramática debido a los instrumentos y la mezcla comercial pop.
- **Brecha de Frecuencia Absoluta ($\Delta = 1296.46\text{ Hz}$):** Esta distancia paramétrica representa la separación estadística real entre ambos constructos sonoros.

---

## 5. Conclusión
A través de la combinación de descriptores en el dominio del tiempo, coeficientes y métricas de masa espectral como el Centroide, se logró establecer una frontera matemática clara de $\approx 1296.46\text{ Hz}$ de diferencia, demostrando que las herramientas usadas proporcionan un marco riguroso y reproducible para el análisis de fenómenos acústicos.

---
- [Código](Tarea6_PCD.ipynb)
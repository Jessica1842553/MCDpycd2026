## **Análisis de imágenes** 
### Procesamiento de imágenes con `opencv`

---

### 1. Análisis de Imagen

El procesamiento de la muestra industrial de balines de acero (*Essential Cycles*) arrojó un escenario analítico de alta complejidad, a diferencia de las geometrías ideales, esta imagen de control presentó dos retos fundamentales: el embalado denso de los componentes y la alta reflectancia del material metálico pulido.

#### A. Mitigación de Ruido
La presencia de brillos intensos debido a la iluminación y las sombras proyectadas entre los balines adyacentes generaban gradientes de intensidad sumamente abruptos dentro de un mismo objeto. En una primera aproximación el detector de bordes de Canny interpretaba estos brillos como discontinuidades o "bordes fantasmas" internos, fragmentando la estructura circular. 

Para resolverlo, se usó la aplicación de un filtro de Suavizado Gaussiano con un Kernel bidimensional de $13 \times 13$. Este operador funcionó para difuminar las variaciones de luminancia internas y homogeneizando la textura del metal sin destruir la información del perímetro exterior.

#### B. Optimización Paramétrica de la Transformada de Hough
La disposición compacta de los balines provocó inicialmente un fenómeno de sobreajuste y falsos positivos (macrocírculos que agrupaban múltiples balines). Para corregir este comportamiento y lograr la convergencia del modelo, se ejecutó una calibración sobre el espacio paramétrico del acumulador de Hough:

1. **Resolución del Acumulador (`dp=1.2`):** Se estableció en este factor para balancear la velocidad de cómputo y la escala del plano de votación, permitiendo una acumulación de votos óptima en regiones con alta densidad de bordes.
2. **Distancia Mínima entre Centros (`minDist=35`):** Se fijó en 35 píxeles como el umbral seguro para evitar que el algoritmo duplicara centros en un mismo balín, forzando al sistema a reconocer solo un centroide dominante por pieza a pesar de estar en contacto físico directo con las demás.
3. **Umbral de Validación (`param2=25`):** Esta fue la variable crítica del experimento. Al definir un mínimo de 25 votos en el acumulador, se logró filtrar con éxito el ruido superficial y eliminar los macrocírculos erróneos.
4. **Delimitación de Escala (`minRadius=10` y `maxRadius=25`):** Restringir el radio máximo de manera estricta a 25 píxeles fue fundamental para impedir que las curvas combinadas de varios balines adyacentes fueran interpretadas erróneamente como una sola estructura circular de gran tamaño.

#### C. Conclusión
Como se constata en la representación gráfica final, el algoritmo logró discriminar y delimitar individualmente cada componente mediante contornos vectoriales perfectos (marcados en verde), posicionando el centroide geométrico (punto rojo) de manera exacta. Esta aproximación metodológica comprueba que la correcta calibración permite resolver problemas complejos de conteo automatizado en líneas de producción industrial.

---

- [Imagen](https://www.essentialcycles.com/cdn/shop/files/090705-01_1.jpg?v=1737387525)
- [Código](T4_PCD.ipynb)
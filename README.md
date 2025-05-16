# Variabilidad-FC-Wavelet
## Introducción

Este laboratorio busca entender cómo varía la frecuencia cardíaca usando la transformada wavelet. Básicamente, esta herramienta ayuda a ver cómo cambian las frecuencias importantes en la señal del corazón a lo largo del tiempo. Es por ello, que es necesario conocer el funcionamiento del sistema cardiaco  y cómo se procesan las señales que se obtienen del corazón, tal como se muetsra a continuación:

### Electrocardiograma

Un electrocardiograma (ECG) registra la actividad eléctrica del corazón, en este se pueden observar las fluctuaciones de voltaje, en otras palabras, se muestran los cambios de voltaje a lo largo de cada latido, por lo que permite analizar la variación del potencial eléctrico durante un ciclo cardíaco completo, pero también captura los datos valiosos sobre el funcionamiento del corazón y su condición, con el fin de reconocer arritmias, valorar enfermedades cardiacas y vigilar la salud cardiovascular. En un ECG, un complejo QRS simboliza la despolarización de los ventrículos, un evento fisiológico que sucede en el ciclo cardiaco.

### Complejo QRS

En la señal del ECG, el complejo QRS representa la despolarización de los ventrículos, un evento fisiológico que sucede en el ciclo cardiaco. Las características de este complejo QRS, describen su duración y amplitud, identificando si hay conducción de transmisión eléctrica. El intervalo RR mide el tiempo entre dos complejos QRS sucesivos, este es fundamental para determinar la frecuencia cardiaca. Al analizar cómo varía este intervalo (HRV) se puede examinar cómo el sistema nervioso autónomo afecta en la actividad cardiaca y detectar ritmos anormales. Entonces al observar con detalle la señal del ECG, prestando atención al complejo QRS y al intervalo RR este es primordial para entender la dinámica cardiaca y diagnosticar diversas enfermedades cardiovasculares 

<p align="center">
  <img src="https://github.com/user-attachments/assets/86e71e60-f4a7-47d0-899f-e168f568ce10" alt="q" />
</p>

> Complejo QRS.


### El Sistema Nervioso 

El sistema nervioso autónomo (SNA) es el encargado de la regulación homeostática de las funciones viscerales e involuntarias del cuerpo, para entenderlo mejor se puede tomar de ejemplo el ritmo cardíaco,  la actividad gastrointestinal y respiratoria. El sistema se conforma de de dos componentes fundamentales: el sistema nervioso simpático y el sistema nervioso parasimpático, estos funcionan de manera que el uno se complementa con el otro y viceversa, aunque tienen efectos contrarios.

• **Sistema nervioso simpático:** Este sistema es crucial para preparar al cuerpo de afrontar situaciones de tensión o urgencia, de manera que se encienden respuestas de “lucha o huida”. Durante el proceso, los efectos se ven reflejados en las pupilas dilatadas (midriasis), la velocidad de los latidos que se incrementan y la liberación de glucosa en el torrente sanguíneo para suministrar una fuente adicional de energía.

• **Sistema Nervioso Parasimpático:** Su función es fundamental para estados de relajación y conservación de la energía, de modo que facilita actividades de procesos anabólicos como la digestión y descanso. Disminuye la frecuencia cardiaca y estimula los procesos asociados a la acumulación de las reservas energéticas del cuerpo.

### Transformada Wavelet

Es una técnica que analiza una señal para descomponerla en elementos con diferentes escalas y ubicaciones. Se diferencia con la transformada de fourier,  en que utiliza ondas sinusoidales (senos y cosenos) uniformes para describir señales, la transformada wavelet emplea funciones ondulatorias breves y de forma irregular, conocidas como wavelets. Esta propiedad le permite capturar los cambios de frecuencia dentro de una señal como el momento en que ocurren, lo que permite conservar la información esencial al mismo tiempo que se reduce el tamaño del archivo 

• **Uso de la transformada Wavelet**

En el campo de señales biológicas la transformada wavelet tiene una gran variedad de aplicaciones, en algunas de estas  se destaca en el análisis de electrocardiogramas (ECG) para la identificación de enfermedades como son las  arritmias y otras irregularidades cardiacas. Se ha logrado desarrollar diferentes algoritmos que destacan las capacidades de las wavelets para identificar patrones específicos en los registros de ECG, logrando con exactitud en el diagnósticos Además en el procesamiento de señales de electroencefalografía (EEG),  estas facilitan mucho en la eliminación de ruidos e interferencias dando como resultado la claridad de las ondas cerebrales para su análisis. La transformada wavelet también se integra con métodos como en las máquinas de soporte vectorial para categorizar distintos tipos de arritmias cardiacas basándose en los patrones de la señal. Es de mucha utilidad para la compresión de imágenes médicas y señales biológicas, permitiendo conservar información esencial al mismo tiempo que reduce el tamaño del archivo 

• **Tipos de Wavelets utilizadas en señales biológicas**

Existen diferentes familias wavelets cada una con propiedades únicas. Una de las más destacadas son las ondículas Haar las cuales se basan en funciones escalonadas y por lo tanto son las más sencillas y las primeras en pensar a utilizarse, otra de estas familias son las ondículas Daubechies señaladas como dbN, estás proporciona una buena aproximación de datos y compleción eficientes. Las ondículas Symlets  se puede decir que es una variación de las Daubechies, ya que ofrecen una mejor simetría en la representación de las señales, por último los coiflets contiene características con las Daubechies pero se distinguen por tener un mayor número de momentos nulos y la wavelet sombrero mexicano (Mexican Hat Wavelet) es útil para detectar bordes y transiciones en las señales.

A continuación se muestra un diagrama de flujo donde se evidencia el paso a paso a realizar en el presente laboratorio.

<div align="center">
  <img src="https://github.com/user-attachments/assets/4dd329a6-ccdd-4c97-88b8-20e0f08ca559" alt="Descripción" width="700"/>
</div>

> Diagrama de Flujo.

## Medición
### Adquisición de la señal 


Se inició la medición de la señal colocando electrodos en la superficie de la piel del paciente, para una buena conexión al capturar la actividad eléctrica . Los electrodos son previamente conectados al circuito integrado AD8232, el cual  ayudará a capturar la señal de una forma más sencilla, debido a que éste al ser un amplificador de señal de biopotenciales, capta y amplifica la señal eléctrica del corazón.

La salida analógica del módulo se conectó al sistema de adquisición de datos DAQ de National Instruments. A Partir de la librería nidaqmx se desarrollo una interfaz en Python para visualizar la señal en tiempo real, en total se recolectaron 30000 datos durante un lapso de 5 minutos, manteniendo el paciente en reposo para minimizar interferencias y realizar el procesamiento correspondiente.

<p align="center">
  <img src="https://github.com/user-attachments/assets/fdab44eb-f4a4-4f47-950f-fc074f56b772" alt="aqq" />
</p>

> **Ejes de la Gráfica:**
> > **-El eje horizontal (Tiempo [s]):** Representa el tiempo transcurrido durante el registro del ECG.

> > **-El eje vertical (Amplitud [mV]):** Representa la amplitud de las señales eléctricas del corazón.

Los electrodos se colocan estratégicamente en el pecho del usuario para captar la señal de manera óptima. De manera que en la clavícula derecha, debajo de la clavícula izquierda, y el electrodo verde, que actúa como tierra que se situó en la zona de las costillas.

<p align="center">
  <img src="https://github.com/user-attachments/assets/4c26b7de-662c-4968-b1ed-a6bc29adaa03" alt="Imagen centrada" width="500">
</p>

> Ubicación de los electrodos.

En electrocardiografía, la frecuencia de muestreo define la cantidad de mediciones de la actividad eléctrica que se realizan cada segundo. Se aconseja una frecuencia mínima de 500 muestras por segundo (MPS), la cual es vital para registrar las características del trazado incluyendo las ondas P,QRS y T. Una frecuencia de muestreo suficiente previene la aparición de frecuencias falsas en una señal digital (aliasing) y la pérdida de información relevante, como detalles críticos de la señal cardiaca, especialmente durante  activacion y reparacion electrica de los ventrículos en el complejo QRS

### Pre-procesamiento de la señal

Ésta etapa es clave en el análisis de señales fisiológicas (Como el ECG) y en general para cualquier sistema de adquisición de datos.  Su propósito es limpiar y preparar la señal, por lo cual una estrategia inicial de filtro pasa bajo a un filtro pasa banda  

• **Filtro pasa bajo:** Es un tipo de filtro diseñado para permitir el paso de frecuencias bajas y bloquear las altas, esto contribuye a la limpieza de la señal y generar un efecto suavizado a los datos, pero también evitar errores de muestreo.

• **Filtro pasa banda:** Este filtro permite el paso de cierto rango de frecuencias limitado y bloquea el paso de frecuencias por encima y debajo de este rango. Es decir, que para construir un filtro pasa banda se une un filtro pasa bajo y pasa alto, por eso se obtiene como resultado el paso de ese rango de frecuencias en específico y la atenuación de las demás.

<p align="center">
  <img src="https://github.com/user-attachments/assets/99141174-0674-43aa-bf5a-186f5faede7c" alt="AQQQQ" width="500"/>
</p>

> Filtro pasa bajo a pasa alto.

<p align="center">
  <img src="https://github.com/user-attachments/assets/5d9d741c-af52-4e70-a287-d2aa126127f0" alt="kl" />
</p>

> Ecuación para pasar de pasa bajo a pasa alto.

<p align="center">
  <img src="https://github.com/user-attachments/assets/757c7feb-9e26-4dd0-b5a4-659a4d28926d" alt="k" />
</p>

> Ecuación para hallar el orden del filtro.

### **Diseño del filtro:**

**•	Frecuencia de corte baja (fL):** 0.5 Hz

**•	Frecuencia de corte alta (fH):** 40 Hz

**•	Frecuencia de muestreo (fs):** 500 Hz

**•	Atenuación fuera de la banda:** 60 Hz

**•	Orden del filtro:** Butterworth orden 4


Se procedió a identificar el HRV recordando que este  representas las variaciones en el tiempo entre latido sucesivos en el corazón, localizar los picos brinda como se marca la despolarización ventricular en un ECG, dando información de la duración de un ciclo cardiaco valioso para evaluar la frecuencia y la regularidad del ritmo cardiaco. Se retiró una sección de la señal para la mejor visualización de estos picos y su análisis.

<p align="center">
  <img src="https://github.com/user-attachments/assets/e2e73bf1-7da4-49c7-9683-fc4e2adb70ae"/>
</p>

> Detección de Picos R.

<p align="center">
  <img src="https://github.com/user-attachments/assets/5afff3c2-62db-47ec-94dd-7b86d4124467" />
</p>

> Detección de Picos R, filtrada.

### Análisis de la HRV en el dominio del tiempo

**•	Media de los intervalos RR:**  Este parámetro es clave para el laboratorio ya que determina tanto la frecuencia cardiaca promedio como su variabilidad (HRV). Se calculó promediando todos los intervalos RR registrados 3 segundos, es decir sumando  sumando los intervalos y dividiendo el total por la cantidad de mediciones. En nuestra señal, la media de los intervalos RR fue de 0,6519 segundos (651,9 ms).

Este valor representa el tiempo promedio entre latidos cardíacos consecutivos, esencial para conocer la frecuencia cardiaca media utilizando la fórmula ()  es esencial para comprender que una media más baja sugiere una frecuencia cardíaca más alta, mientras que una media más alta indica una frecuencia cardíaca más baja.

<p align="center">
  <img src="https://github.com/user-attachments/assets/1b0b9669-756a-4071-85e0-eb807563dcdb" /><br><br>
  <img src="https://github.com/user-attachments/assets/529fa94a-c1b6-432b-b345-e9eb8d50146b" />
</p>

Este valor representa que la frecuencia cardíaca es elevada pero puede estar influenciado por el estrés, la actividad física o el estado emocional del individuo.

**•Desviación estándar de los intervalos RR:** este valor se toma de todos los intervalos RR medidos durante el mismo período, representa información valiosa sobre las fluctuaciones en los tiempos entre latidos sucesivos del corazón, lo que facilita una comprensión más profunda de la estabilidad y el funcionamiento del sistema cardiovascular recordando que este es independiente a la frecuencia cardiaca útil. En nuestra señal, la desviación estándar de los intervalos RR fue de 0,2689 segundos (268,9 ms). 

La desviación estándar tiene un valor de 0,2689 segundos, un valor relativamente alto lo que sugiere que hay una mayor variabilidad en los intervalos RR, esto refleja la respuesta activa del sistema nervioso autónomo y en específico el sistema parasimpático el cual regular la frecuencia cardiaca. Es decir, al tener una desviación estándar baja se asocia con un ritmo cardíaco más constante y menos influenciado por factores externos. Por el contrario, una alta variabilidad puede ser indicativa de un mejor estado de salud cardiovascular y de una mayor capacidad del organismo para adaptarse a cambios fisiológicos.

En total, se identifican 458 complejos R a lo largo de toda la señal, a continuación se representan los primeros valores RR en segundos   

<p align="center">
  <img src="https://github.com/user-attachments/assets/bb252e88-0cc2-4597-bcfd-83e414bdf124"/>
</p>

> **Intervalos R-R (en segundos):**
> > [0.540018  - 0.53001767 0.540018 -  0.53001767  - 0.540018 -  0.52001733  -  
 0.52001733 - 0.53001767  -  0.53001767  -  0.52001733 - 0.53001767  -  0.52001733  -  
 0.510017 -  0.52001733  -  0.510017  -  0.990033  -  0.960032  -  0.97003233  -  
 0.930031  -  0.95003167   -  0.50001667  -   0.55001833  -  0.540018  -  0.55001833  -  
 0.56001867  -  0.570019  -  0.570019 -  0.58001933 -  0.570019  -  1.110037  -  
 0.540018  -  0.50001667  -  1.00003333   -  0.98003267  -  1.45004833 - 0.97003233  -  
 0.55001833  -  1.21004033  -  0.64002133   -  0.68002267   -  0.70002333  -   0.67002233  -  
 0.61002033   -  0.58001933  -  0.56001867   -  0.570019   -   0.56001867   -   0.56001867  -  
 0.56001867   -   0.55001833   -   0.56001867   -   0.56001867   -   0.56001867   -   0.540018  -  
 0.53001767   -   0.52001733   -   0.510017    -   1.03003433   -   0.53001767   -   0.540018  -  
 0.540018   -  0.540018   -   0.56001867   -   0.55001833  -    0.56001867   -   0.56001867  -  
 1.07003567   -   0.52001733 0.510017   -   0.50001667   -   0.510017   -   1.00003333  -  
 0.510017   -  0.50001667   -   0.50001667   -   1.42004733   -   0.92003067 1.410047  -  
 0.50001667   -   0.50001667   -   0.50001667   -   0.510017    -   0.510017   -   0.510017  -  
 0.510017   -  1.04003467   -   0.50001667   -   0.50001667   -   0.510017   -   0.52001733  -  
 0.52001733 0.510017   -   0.540018    -    0.510017   -   0.52001733   -  0.510017 ]

### Aplicación de transformada Wavelet

<p align="center">
  <img src="https://github.com/user-attachments/assets/879fe11b-162c-43e6-9731-703aa0de93ca" />
</p>

> **Ejes de la Gráfica:**
> > **-El eje horizontal:** Representa el tiempo transcurrido durante el registro de los intervalos RR. Esto permite observar cómo varían los patrones de frecuencia a lo largo del tiempo.
> > **-El eje vertical:** Muestra las diferentes escalas o frecuencias. Las frecuencias más bajas corresponden a variaciones más lentas en el ritmo cardíaco, mientras que las frecuencias más altas reflejan cambios más rápidos.

Para analizar cómo cambia la fuerza de las diferentes frecuencias de la señal a lo largo del tiempo, se decidió utilizar la transformada wavelet continua (CWT) con la wavelet de Morlet. En la imagen que vimos antes se puede observar cómo se aplicó esta técnica a datos de variabilidad de la frecuencia cardíaca (HRV) buscando así identificar diferentes alteraciones en las frecuencias bajas y altas a medida que transcurría el tiempo. La wavelet de Morlet combina una onda sinusoidal con una forma de campana gaussiana, permitiendo registrar cuándo ocurren los eventos como qué frecuencias componen la señal, ofreciendo un buen equilibrio entre la precisión en el tiempo y en la frecuencia. Por esta razón resulta muy útil para analizar señales como la HRV, donde las frecuencias y su intensidad no se mantienen constantes

En el espectrograma se puede observar como la intensidad del color o luminosidad refleja la energía o potencia de las distintas frecuencias en cada instante de tiempo, indicando como en las áreas más brillantes con colores más intensos indican una mayor energía en una frecuencia específica. Estos colores tambien indican la magnitud o potencia de la señal, es decir, tonos cálidos (rojo, amarillo) corresponden a una alta potencia, mientras que los tonos fríos (azul) indican una baja potencia.

**•Banda de Baja Frecuencia (0,04 - 0,15 Hz):** Esta banda de frecuencia está vinculada con la actividad simpática y parasimpática del sistema nervioso por lo que es muy sensible a tener cambios en el que aparezcan áreas con colores más cálidos en la banda de baja frecuencia (LF), en el que pudo haber  aumentado en la actividad y  podría asociarse con una respuesta de estrés o con la activación del sistema nervioso simpático.

**•Banda de Alta Frecuencia (0,15- 0,4):** Esta banda generalmente refleja la actividad parasimpática encargada de modular la respiración, por lo tanto es muy susceptible a cualquier cambio notable en la potencia en esta banda debido variaciones en la respuesta parasimpática, en el que están involucrados  procesos de relajación.

**•Análisis Crítico de Cambios en la Potencia Espectral:** La CWT facilitó la observación de cómo varían estas frecuencias en potencia a lo largo del tiempo. Por ejemplo, si en un segmento específico se observa un aumento en la potencia de la banda de baja frecuencia y podría interpretarse como un incremento en la actividad simpática, lo que podría estar asociado a situaciones de estrés o esfuerzo físico. En cambio en una disminución en la potencia de estas frecuencias podría indicar un estado de relajación o recuperación.



## Instrucciones

### Archivos principales

- **archivo.ui**  
  Archivo generado con Qt Designer que contiene la definición de la interfaz gráfica del programa. Este archivo debe ser cargado en el código Python para mostrar la ventana con los botones y opciones para el usuario.

- **archivo.txt**  
  Archivo de texto que contiene los datos o parámetros necesarios para la ejecución del programa, o puede ser un archivo de salida donde se guardan los resultados del análisis.

- **script_principal.py**  
  Código Python que carga la interfaz `.ui`, lee el archivo `.txt` y ejecuta todo el procesamiento y análisis de señales.

### Requisitos y librerías necesarias

Para correr el proyecto, necesitás tener instaladas las siguientes librerías en tu entorno Python (Spyder, Google Colab, etc.):

pip install PyWavelets
pip install numpy
pip install matplotlib
pip install pyqt5
pip install wfdb

• Tener Python 3.9 instalado y utilizar Spyder o IDLE, como en ésta práctica.

• Tener acceso a los archivos .ui y .txt para cargar.

• Contar con las librerías necesarias instaladas para ejecutar el código correctamente (especificadas en el inicio del artículo).

## Usar

Por favor, cite este artículo:

Huertas, V.; Ramírez, A.; Gómez, P. Variabilidad-FC-Wavelet. 15 de mayo de 2025.

## Información de contacto

• est.laurav.huertas@unimilitar.edu.co
• est.deisy.aramirez@unimilitar.edu.co
• est.paulav.gomez@unimilitar.edu.co


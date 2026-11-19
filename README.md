[![Open in MATLAB Online](https://www.mathworks.com/images/responsive/global/open-in-matlab-online.svg)](https://matlab.mathworks.com/open/github/v1?repo=YasditContreras/MSFP4)

# Práctica 4: Modelado y control del sistema endócrino

## Información del estudiante
Contreras Jiménez Kenia Yasdit \[23212188]; L23212188@tijuana.tecnm.mx

Modelado de Sistemas Fisiológicos

Ingeniería Biomédica

## Docente
Dr. Paul Antonio Valle Trujillo; paul.valle@tectijuana.edu.mx

Departamento de Ingeniería Eléctrica y Electrónica, Tecnológico Nacional de México/IT Tijuana, Blvd. Alberto Limón Padilla s/n, Tijuana, C.P. 22454, B.C., México.

## Descripción de la asignatura

El modelizado de sistemas fisiológicos es una herramienta importante en Ingeniería Biomédica, permite comprender el funcionamiento del cuerpo humano, así como diseñar y evaluar terapias y dispositivos médicos; se define como el proceso de formular modelos matemáticos o computacionales que representan el comportamiento y la interacción de los sistemas biológicos y fisiológicos. Esta asignatura pretende aportar al perfil del Ingeniero Biomédico la capacidad de realizar investigación científica en el área de Biología de Sistemas con la finalidad de dirigir y participar en equipos de trabajo interdisciplinarios en contextos nacionales e internacionales, así como de proporcionar soluciones informáticas para resolver problemas en el campo de la Ingeniería Biomédica con ética profesional; lo anterior al proporcionar al estudiante bases sólidas para modelizar sistemas y diseñar controladores para la solución de problemas en las áreas de atención médica y del sector industrial médico. La construcción de analogías entre circuitos eléctricos y sistemas fisiológicos para la formulación de modelos matemáticos y el diseño de controladores mediante la experimentación *in silico* brindan herramientas de gran aplicación en el quehacer profesional del Ingeniero Biomédico.

La asignatura de Modelado de Sistemas Fisiológicos forma parte del plan de estudios de la carrera en Ingeniería Biomédica con la siguiente competencia general del curso: Utiliza las propiedades de los circuitos RLC para describir la dinámica de sistemas fisiológicos, obtener modelos matemáticos y aplicar el control clásico, esto con el objetivo de integrar los principios de la Ingeniería de Control, la Electrónica Analógica y las Ciencias de la Computación con la Anatomía y Fisiología del cuerpo humano para proporcionar descripciones cuantitativas y cualitativas de sistemas fisiológicos complejos con el objetivo de modelizar, analizar, controlar, ilustrar y predecir su dinámica tanto en el corto como en el largo plazo.

## Competencia y objetivos

### Competencia a desarrollar
Modeliza sistemas fisiológicos mediante analogías eléctricas, ecuaciones diferenciales y funciones de transferencia para analizar su comportamiento dinámico y diseña estrategias de control mediante técnicas de control clásico. En particular, durante la práctica se interpreta una descripción simplificada de los procesos de secreción, transporte, almacenamiento y respuesta hormonal para proponer un circuito eléctrico equivalente de segundo orden, comparar una condición de referencia (*control*) con una condición alterada (*caso*), diseñar un controlador PID y contrastar los resultados obtenidos mediante modelado analítico, simulación computacional y experimentación en el Laboratorio de Electrónica.

### Objetivos específicos
1. Interpretar la descripción funcional del eje endócrino y proponer el circuito eléctrico equivalente de segundo orden identificando entradas, salidas, flujos y nodos.
2. Formular las ecuaciones del circuito mediante análisis de mallas y obtener la función de transferencia $G(s) = V_s(s)/V_e(s)$ aplicando la transformada de Laplace.
3. Sustituir los valores comerciales de los componentes para obtener las funciones de transferencia independientes de la condición de referencia (*control*) y la condición alterada (*caso*, hipertiroidismo).
4. Analizar el error en estado estacionario ante una entrada escalón unitario y determinar la estabilidad de ambos sistemas mediante la ubicación de sus polos.
5. Formular el modelo mediante ecuaciones integro-diferenciales e implementarlo junto con la función de transferencia y el circuito físico en MATLAB/Simulink y Simscape Electrical.
6. Comparar las respuestas en lazo abierto ante un escalón unitario durante el intervalo $t \in [0, 10]\,\mathrm{s}$.
7. Diseñar y sintonizar un controlador PID para reducir la diferencia entre la respuesta del caso y la respuesta de referencia del individuo sano.
8. Reproducir los modelos y el sistema controlado en Python (Visual Studio Code) y contrastar los resultados con MATLAB/Simulink.
9. Relacionar los elementos eléctricos del modelo con las estructuras y procesos fisiológicos mediante un diagrama biológico elaborado en BioRender.

## Descripción detallada del sistema

El sistema endócrino participa en la regulación de numerosos procesos fisiológicos mediante la liberación de hormonas producidas por glándulas especializadas. Para estudiar su comportamiento dinámico mediante analogías eléctricas, se plantea un modelo fenomenológico simplificado de segundo orden construido bajo las siguientes hipótesis funcionales:

1. **Estímulo fisiológico $V_e(t)$:** Señal neural, metabólica o homeostática que inicia la secreción hormonal, representada mediante una fuente de voltaje.
2. **Transporte y pérdidas $R_1$:** Oposición efectiva y retrasos asociados al transporte de la hormona desde la glándula hasta el compartimento efector.
3. **Almacenamiento temporal $C$:** Capacidad del compartimento para acumular temporalmente la señal hormonal antes de su utilización o eliminación.
4. **Inercia y respuesta del tejido diana $L$ y $R_2$:** Rama en serie conformada por una inductancia $L$ (retardo o resistencia dinámica a cambios rápidos) y una resistencia $R_2$ (oposición efectiva asociada a la utilización, disipación o eliminación hormonal).
5. **Flujos hormonales $F_e(t)$ y $F_s(t)$ :** Corrientes asociadas a la secreción/transporte hormonal y a la utilización/respuesta del órgano diana, respectivamente.
6. **Nivel hormonal efectivo $V_s(t)$:** Variable de salida medida en el nodo de unión entre $R_1$, $C$ y $L$, que representa de manera normalizada la señal hormonal disponible para producir una respuesta metabólica.

### Analogía fisiológica–eléctrica

| Variable o proceso fisiológico | Representación eléctrica | Interpretación dentro del modelo |
| --- | --- | --- |
| Estímulo para la secreción hormonal | $V_e(t)$ | Señal de entrada que activa la respuesta del sistema endócrino. |
| Flujo de secreción y transporte hormonal | $F_e(t)$ / $i_1(t)$ | Corriente asociada con la transferencia de la señal hormonal hacia el compartimento de respuesta. |
| Pérdidas y oposición durante el transporte | $R_1$ | Representación fenomenológica de procesos que reducen o retardan la transmisión de la señal hormonal. |
| Acumulación temporal de hormona | $C$ | Capacidad del compartimento para almacenar temporalmente la señal hormonal antes de su utilización o eliminación. |
| Retardo o inercia de la respuesta del tejido diana | $L$ | Representación de la resistencia dinámica del sistema a cambios rápidos en la respuesta hormonal. |
| Utilización, disipación o eliminación de la señal | $R_2$ | Oposición efectiva asociada con la utilización o desaparición de la señal hormonal en el compartimento de respuesta. |
| Flujo asociado con la respuesta del tejido diana | $F_s(t)$ / $i_2(t)$ | Corriente correspondiente a la rama que representa la respuesta del órgano diana. |
| Nivel hormonal efectivo | $V_s(t)$ | Variable de salida que representa de manera normalizada la señal hormonal disponible en el compartimento de interés. |

### Parámetros del control y del caso

La modificación simultánea de la capacitancia $C$ y la resistencia $R_2$ permite simular la alteración fisiológica correspondiente a un cuadro de **hipertiroidismo** (mayor acumulación y liberación hormonal junto con menor tasa de eliminación efectiva en el modelo):

| Componente | Control (Individuo sano) | Caso (Hipertiroidismo simulado) |
| --- | --- | --- |
| $R_1$ | $1\mathrm{k}\Omega$ | $1\mathrm{k}\Omega$ |
| $L$ | $100\mathrm{mH}$ | $100\mathrm{mH}$ |
| $C$ | $1\mu\mathrm{F}$ | $1000\mu\mathrm{F}$ |
| $R_2$ | $100\mathrm{k}\Omega$ | $1\mathrm{k}\Omega$ |

La entrada aplicada al sistema es un escalón unitario $V_e(t) = u(t)$, y la señal de error utilizada para el diseño del controlador se define como:

$$
e(t) = V_{s,\mathrm{control}}(t) - V_{s,\mathrm{caso}}(t).
$$

Palabras clave: Sistema endócrino; Analogía eléctrica RLC; Función de transferencia; Hipertiroidismo; Controlador PID; Simulación *in silico*.

---

## Diagrama biológico del sistema endócrino (BioRender)

<p align="center">
<img width="562" height="397" alt="image" src="https://github.com/user-attachments/assets/7f173e70-b6e0-48f0-a6bb-513ba5e31def" />
</p>

*Figura 1. Representación biológica del modelo del sistema endócrino y correspondencia de sus componentes eléctricos elaborada en BioRender.com (Prado Acosta Briseida, Contreras Kenia Yasdit, Cerano Fuentes David Esau).*

| Elemento | Estructura / Proceso biológico | Interpretación en el diagrama |
| --- | --- | --- |
| $V_e(t)$ | Hipotálamo / Hipófisis | Estímulo inicial que desencadena la señalización endócrina. |
| $R_1$ | Sistema circulatorio | Resistencia al flujo sanguíneo durante el transporte hormonal. |
| $C$ | Glándula tiroides | Acumulación y liberación de hormonas tiroideas (en hipertiroidismo existe mayor acumulación y liberación). |
| $L$ | Tejido / Órgano diana (Corazón) | Tiempo que tarda el tejido en responder ante variaciones de la señal hormonal. |
| $R_2$ | Hígado / Metabolismo hepático | Eliminación y degradación de la hormona (en hipertiroidismo se presenta menor eliminación). |
| $V_s(t)$ | Metabolismo sistémico | Nivel hormonal efectivo disponible que regula la actividad metabólica. |

---

## Desarrollo matemático de la práctica

### 1. Topología del circuito y análisis de mallas

El circuito equivalente consta de una rama de entrada con la fuente $V_e(t)$ en serie con $R_1$, conectada a un nodo central donde se derivan en paralelo un capacitor $C$ hacia tierra y una rama en serie formada por el inductor $L$ y el resistor $R_2$. La tensión de salida $V_s(t)$ se mide sobre la carga $R_2$.

Aplicando las leyes de voltaje de Kirchhoff a las dos mallas con corrientes $i_1(t)$ e $i_2(t)$:

**Malla 1:**

$$
R_1 i_1(t) + \frac{1}{C} \int \left[i_1(t) - i_2(t)\right] dt = V_e(t)
$$

**Malla 2:**

$$
L \frac{d i_2(t)}{dt} + R_2 i_2(t) + \frac{1}{C} \int \left[i_2(t) - i_1(t)\right] dt = 0
$$

La tensión de salida en la carga $R_2$ está dada por:

$$
V_s(t) = R_2 i_2(t).
$$

### 2. Obtención de la función de transferencia

Aplicando la transformada de Laplace con condiciones iniciales nulas, de la Malla 2 se obtiene la relación entre las corrientes de malla:

$$
\frac{1}{Cs} \left[I_1(s) - I_2(s)\right] = (Ls + R_2) I_2(s)
$$

Despejando $I_1(s)$:

$$
I_1(s) - I_2(s) = Cs(Ls + R_2) I_2(s) \implies I_1(s) = \left[1 + Cs(Ls + R_2)\right] I_2(s).
$$

Sustituyendo $I_1(s)$ en la ecuación transformada de la Malla 1:

$$
V_e(s) = R_1 I_1(s) + (Ls + R_2) I_2(s)
$$

$$
V_e(s) = R_1 \left[1 + Cs(Ls + R_2)\right] I_2(s) + (Ls + R_2) I_2(s)
$$

$$
V_e(s) = \left[R_1 + R_1 L C s^2 + R_1 R_2 C s + Ls + R_2\right] I_2(s)
$$

$$
V_e(s) = \left[R_1 L C s^2 + (L + R_1 R_2 C) s + (R_1 + R_2)\right] I_2(s).
$$

Dado que $V_s(s) = R_2 I_2(s)$, se despeja la función de transferencia general del sistema:

$$
\boxed{G(s) = \frac{V_s(s)}{V_e(s)} = \frac{R_2}{R_1 L C s^2 + (L + R_1 R_2 C) s + (R_1 + R_2)}}
$$

### 3. Sustitución de parámetros: Control vs. Caso

#### Condición Control (Individuo sano)
Con $R_1 = 1\mathrm{k}\Omega$, $L = 100\mathrm{mH}$, $C = 1\mu\mathrm{F}$ y $R_2 = 100\mathrm{k}\Omega$:
- $R_1 L C = (10^3)(0.1)(10^{-6}) = 1 \times 10^{-4}$
- $L + R_1 R_2 C = 0.1 + (10^3)(10^5)(10^{-6}) = 0.1 + 100 = 100.1$
- $R_1 + R_2 = 1000 + 100\,000 = 101\,000$

$$
G_{\mathrm{control}}(s) = \frac{100\,000}{10^{-4} s^2 + 100.1 s + 101\,000} = \frac{1 \times 10^9}{s^2 + 1\,001\,000 s + 1.01 \times 10^9}.
$$

#### Condición Caso (Hipertiroidismo simulado)
Con $R_1 = 1\mathrm{k}\Omega$, $L = 100\mathrm{mH}$, $C = 1000\mu\mathrm{F}$ y $R_2 = 1\mathrm{k}\Omega$:
- $R_1 L C = (10^3)(0.1)(10^{-3}) = 0.1$
- $L + R_1 R_2 C = 0.1 + (10^3)(10^3)(10^{-3}) = 0.1 + 1000 = 1000.1$
- $R_1 + R_2 = 1000 + 1000 = 2000$

$$
G_{\mathrm{caso}}(s) = \frac{1000}{0.1 s^2 + 1000.1 s + 2000} = \frac{10\,000}{s^2 + 10\,001 s + 20\,000}.
$$

### 4. Error en estado estacionario

Aplicando el Teorema del Valor Final ante una entrada escalón unitario $V_e(s) = \frac{1}{s}$:

$$
V_s(\infty) = \lim_{s \to 0} s V_e(s) G(s) = \lim_{s \to 0} G(s) = \frac{R_2}{R_1 + R_2}.
$$

**Valor final en Control:**

$$
V_{s,\mathrm{control}}(\infty) = \frac{100\mathrm{k}\Omega}{1\mathrm{k}\Omega + 100\mathrm{k}\Omega} = \frac{100}{101} \approx 0.9901\mathrm{V} \quad \Rightarrow \quad e_{\mathrm{ss,control}} = 1 - 0.9901 = 0.0099\mathrm{V}.
$$

**Valor final en Caso:**

$$
V_{s,\mathrm{caso}}(\infty) = \frac{1\mathrm{k}\Omega}{1\mathrm{k}\Omega + 1\mathrm{k}\Omega} = \frac{1}{2} = 0.5000\mathrm{V} \quad \Rightarrow \quad e_{\mathrm{ss,caso}} = 1 - 0.5000 = 0.5000\mathrm{V}.
$$

El cambio de parámetros en el caso patológico provoca una caída del nivel hormonal estacionario de $0.99\mathrm{V}$ a $0.50\mathrm{V}$, generando un error en estado estacionario del $50$ % respecto al estímulo unitario y de $0.49\mathrm{V}$ respecto al individuo sano.

### 5. Análisis de estabilidad (Cálculo de polos)

Las raíces del polinomio característico determinan la estabilidad en lazo abierto:

$$
s^2 + \frac{L + R_1 R_2 C}{R_1 L C} s + \frac{R_1 + R_2}{R_1 L C} = 0
$$

**Polos para el Control:**

$$
s^2 + 1\,001\,000 s + 1.01 \times 10^9 = 0 \implies s_{1,2} = \frac{-1\,001\,000 \pm \sqrt{(1\,001\,000)^2 - 4(1)(1.01 \times 10^9)}}{2}
$$

$$
s_1 \approx -1010, \qquad s_2 \approx -999\,990.
$$

**Polos para el Caso:**

$$
s^2 + 10\,001 s + 20\,000 = 0 \implies s_{1,2} = \frac{-10\,001 \pm \sqrt{(10\,001)^2 - 4(1)(20\,000)}}{2}
$$

$$
s_1 \approx -2, \qquad s_2 \approx -9999.
$$

En ambos escenarios, los polos son reales y estrictamente negativos (ubicados en el semiplano izquierdo del plano complejo $s$), por lo que **ambos sistemas son estables y presentan respuesta sobreamortiguada**. Sin embargo, el polo dominante del caso ($s_1 = -2$) está mucho más cerca del origen que el del control ($s_1 = -1010$), lo que implica una dinámica transitoria significativamente más lenta.

### 6. Modelo mediante ecuaciones integro-diferenciales

Para su implementación en diagramas de bloques (Simulink), el sistema se expresa despejando las variables de estado asociadas a los elementos almacenadores de energía ($C$ e $L$):

$$
\begin{aligned}
i_1(t) &= \frac{1}{R_1} \left( V_e(t) - \frac{1}{C} \int \left[i_1(t) - i_2(t)\right] dt \right), \\
i_2(t) &= \frac{1}{L} \int \left( \frac{1}{C} \int \left[i_1(t) - i_2(t)\right] dt - R_2 i_2(t) \right) dt, \\
V_s(t) &= R_2 i_2(t).
\end{aligned}
$$

---

## Implementación y control en lazo cerrado

### Simulación en MATLAB/Simulink, Simscape Electrical y Python
1. **Lazo abierto ($t \in [0, 10]\,\mathrm{s}$):** Se aplica un escalón unitario $V_e(t) = u(t)$ comparando las tres representaciones (ecuaciones integro-diferenciales, función de transferencia y circuito eléctrico en Simscape) para verificar que la salida converge a $\approx 0.99\,\mathrm{V}$ en el control y a $0.50\,\mathrm{V}$ en el caso.
2. **Lazo cerrado con PID:** La salida $V_{s,\mathrm{control}}(t)$ se emplea como señal de referencia para el modelo del caso. El controlador PID recibe el error $e(t) = V_{s,\mathrm{control}}(t) - V_{s,\mathrm{caso}}(t)$:

$$
C(s) = k_P + \frac{k_I}{s} + k_D s.
$$

| Parámetro PID | Valor sintonizado |
| --- | --- |
| $k_P$ | Pendiente de registrar tras sintonización (*Tune*) |
| $k_I$ | Pendiente de registrar tras sintonización (*Tune*) |
| $k_D$ | Pendiente de registrar tras sintonización (*Tune*) |

### Verificación cruzada de resultados

| Evidencia | Descripción | Estado |
| --- | --- | --- |
| Diagrama biológico | Esquema del sistema endócrino elaborado en BioRender. | Incluido |
| Desarrollo matemático | Mallas, función de transferencia, polos y error estacionario. | Incluido |
| Simulaciones en MATLAB/Simulink | Modelos en lazo abierto y lazo cerrado con Simscape Electrical. | Pendiente de adjuntar gráficas PDF |
| Sintonización PID | Ganancias $k_P, k_I, k_D$ y evidencia de respuesta controlada. | Pendiente |
| Implementación en Python | Script `.py` en VS Code reproduciendo las curvas de MATLAB. | Pendiente |
| Experimentación en laboratorio | Montaje físico en protoboard y capturas del osciloscopio. | Pendiente |

---

## Lista de archivos incluidos en el repositorio

1. `README.md` — Documentación completa, desarrollo analítico y guía de reproducción de la práctica.
2. `imagenes/sistema_endocrino_biorender.png` — Diagrama biológico del sistema endócrino creado en BioRender.
3. `Calculo_Matematico_Pr4.pdf` — Desarrollo manuscrito de mallas, funciones de transferencia, polos y ecuaciones integro-diferenciales.
4. `Apellido_NoControl.mlx` / `.pdf` — Cuaderno computacional de MATLAB y exportación en PDF.
5. `modelo_endocrino.slx` — Modelos de Simulink (ecuaciones, función de transferencia, Simscape Electrical y lazo cerrado PID).
6. `modelo_endocrino.py` — Código fuente en Python para la verificación numérica de las respuestas.
7. `figuras/` — Gráficas exportadas en PDF comparando $V_{s,\mathrm{control}}(t)$, $V_{s,\mathrm{caso}}(t)$ y $V_{s,\mathrm{PID}}(t)$.
8. `CITATION.cff` — Archivo de metadatos y citación académica del repositorio.

## Referencias

\[1] P. A. Valle, *Syllabus para Modelado de Sistemas Fisiológicos*, Tecnológico Nacional de México / Instituto Tecnológico de Tijuana, Tijuana, B.C., México, 2026. https://biomath.xyz/course/

\[2] *Práctica 5.6: Modelado y control del sistema endócrino*, instructivo de la asignatura Modelado de Sistemas Fisiológicos, pp. 96–102.

\[3] M. C. Khoo, *Physiological Control Systems: Analysis, Simulation, and Estimation*, 2nd ed., IEEE Press, 2018.

\[4] K. Ogata, *Ingeniería de Control Moderna*, 5.ª ed., Pearson Educación, 2010.

\[5] J. E. Hall, *Guyton and Hall Textbook of Medical Physiology*, 14th ed., Elsevier, 2021.

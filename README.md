# Diseno incubador neonatal

## Introducción
La incubadora neonatal es un dispositivo médico diseñado para replicar, en la medida de lo posible, las condiciones del ambiente intrauterino, con el fin de garantizar la supervivencia y el desarrollo óptimo del recién nacido, especialmente en casos de prematuridad o bajo peso al nacer [1][2]. Su función principal consiste en regular de forma precisa variables fisiológicamente críticas como la temperatura, la humedad y el flujo de aire al interior de la cabina, creando un entorno térmico neutro que minimice el gasto energético del neonato y favorezca su homeostasis [3].

La importancia de este dispositivo radica en que el neonato, particularmente el prematuro, posee una capacidad limitada para la termorregulación autónoma debido a su piel delgada, escasa grasa subcutánea y un sistema nervioso inmaduro [4]. En este contexto, mantener la temperatura interna alrededor de los 37 °C resulta esencial para prevenir complicaciones como la hipotermia o, en climas tropicales, la hipertermia, esta última posible cuando la temperatura ambiental a la sombra puede superar los 40 °C [5]. Por estas razones, el diseño, construcción y validación de sistemas de monitoreo y control para incubadoras neonatales constituye un área de alta relevancia dentro de la ingeniería biomédica.

El objetivo de esta práctica es reconocer la importancia de las incubadoras neonatales en la salud del neonato, mediante el diseño, simulación y construcción a escala de un sistema capaz de emular su modo de operación, integrando circuitos de control de temperatura y medición de peso, y evaluando su desempeño en comparación con soluciones comerciales disponibles en el mercado.

## Funcionamiento y partes de una incubadora
Desde el punto de vista funcional, la incubadora neonatal opera como un sistema de control de lazo cerrado que regula las condiciones ambientales internas de la cabina. La mayoría de las incubadoras incorporan mecanismos para controlar los niveles de oxígeno y la humedad relativa del aire que respira el neonato, y los microprocesadores integrados en los modelos modernos permiten un control preciso de temperatura, humedad y concentración de oxígeno [6]. El principio de operación general se describe como un ventilador que impulsa el aire ambiente filtrado a través de un elemento calefactor y un contenedor de agua, en donde, el aire acondicionado (humidificado y calentado) fluye hacia la cabina superior donde se encuentra el neonato, mientras que parte del aire es recirculado y otra parte sale por las ranuras de ventilación [7].

En cuanto a sus partes principales, se pueden identificar los siguientes subsistemas:

**Subsistema de control térmico.** La salida de calor del dispositivo es regulada típicamente mediante servocontrol para mantener constante la temperatura cutánea del neonato en un punto del abdomen donde se fija una sonda termistor o también puede controlarse la temperatura del aire interior de la cabina [8]. Las incubadoras actuales proporcionan el ambiente térmico neutro mediante una resistencia eléctrica como elemento calefactor [9]. Adicionalmente, las incubadoras de doble pared, al incorporar una segunda capa interna de plexiglás, reducen la pérdida de calor por radiación, lo que representa una mejora frente a los diseños de pared simple [10].

**Subsistema de control de humedad.** En los primeros días de vida, la pérdida evaporativa diaria de neonatos prematuros puede alcanzar hasta el 20% de la masa corporal; dicha pérdida puede reducirse incrementando la humedad del aire al interior de la incubadora [11]. Por ello, los diseños modernos incorporan sistemas activos de humidificación en lazo cerrado que mantienen niveles controlados y estables de humedad relativa.

**Subsistema de monitoreo y alarmas.** Las variables críticas de monitoreo dentro de la incubadora son la temperatura, la humedad y el nivel de ruido, dado que hipotermia e hipertermia pueden incrementar la morbilidad y mortalidad en neonatos prematuros, mientras que la humedad relativa del aire tiene un papel crucial en la prevención de la deshidratación [12]. Para la seguridad del paciente, las incubadoras electrónicas cuentan con alarmas que se activan ante sobrecalentamiento, falla del ventilador y corte de energía; asimismo, incluyen un mecanismo de corte automático del calefactor cuando la temperatura de la cabina alcanza los 40 °C [7].

**Cubierta y estructura.** Las incubadoras de caja cerrada cuentan con un sistema de filtración natural del aire que minimiza el riesgo de contaminación y limita la pérdida de humedad; la cubierta cerrada envuelve completamente al neonato e incluye orificios de acceso lateral para el personal de salud [13].

**Subsistema de medición de peso.** Diseños de incubadoras de bajo costo más recientes han integrado la medición continua del peso del neonato como parte del sistema principal, junto con el control de temperatura y humedad, demostrando la viabilidad de consolidar múltiples funciones de monitoreo en un único dispositivo [14].

## Desarrollo de una incubadora a escala

### Circuito Eléctrico Temperatura
El subsistema de control de temperatura fue diseñado para mantener el interior de la incubadora dentro de un rango aproximado entre **36 °C y 37,5 °C**, tal como se exige en la práctica. Para ello, se utilizó un sensor **DHT22** conectado a una **ESP32**, encargada de adquirir la temperatura interna del prototipo y ejecutar la lógica de control.

El sistema implementado cuenta con dos actuadores principales: un **bombillo** empleado como elemento calefactor y un **ventilador** para la circulación de aire y disipación de calor cuando la temperatura supera el límite establecido. El bombillo se acciona mediante un **módulo relé**, mientras que el ventilador se alimenta desde la etapa de potencia implementada con **transformador, puente rectificador y regulación de tensión**. De esta manera, el prototipo reproduce el comportamiento básico de una incubadora neonatal a escala con control térmico de lazo cerrado.

También se implementó un panel de **tres LEDs** para indicar el estado térmico del sistema:
- **LED rojo**: temperatura baja.
- **LED verde**: temperatura dentro del rango ideal.
- **LED rojo / amarillo**: temperatura por encima del rango permitido.

#### Simulación del circuito de temperatura
![Simulación del circuito de temperatura en Wokwi](imagenes/simulacion_temperatura_wokwi.png)

#### Montaje real del circuito de temperatura
![Montaje real del sistema de temperatura](imagenes/montaje_temperatura_real.jpg)

---

### Circuito Eléctrico que Mide Peso
Para la medición de peso se empleó una **celda de carga** acoplada a un módulo **HX711**, el cual permite acondicionar y digitalizar la señal proveniente de la galga. Esta señal es procesada por la **ESP32**, la cual estima el peso aplicado y lo muestra en una **pantalla OLED**.

Este subsistema se diseñó con el propósito de estimar el peso del neonato a escala dentro del prototipo, cumpliendo así con el requisito de la práctica de contar con un sistema de medición de peso mostrado en pantalla. Aunque durante las pruebas experimentales la calibración no alcanzó la precisión esperada, se logró integrar satisfactoriamente la arquitectura general de adquisición, procesamiento y visualización de la variable.

#### Simulación del sistema de peso
![Simulación del sistema de peso con HX711](imagenes/simulacion_peso_wokwi.png)

#### Montaje real del sistema de peso
![Montaje real de la galga y HX711](imagenes/montaje_peso_real.jpg)

---

### Código para el funcionamiento y control
El funcionamiento del sistema fue implementado en la **ESP32**, integrando las rutinas de lectura de sensores, control de actuadores y visualización de variables en tiempo real. El código desarrollado permite:

- leer temperatura y humedad desde el **DHT22**,
- estimar el peso a partir de la lectura del **HX711**,
- mostrar temperatura y peso en la **pantalla OLED**,
- accionar el **bombillo** por medio del **relé** cuando la temperatura se encuentra por debajo del umbral definido,
- activar el **ventilador** cuando la temperatura supera el límite superior,
- encender el LED correspondiente según el estado térmico del sistema.

En términos de lógica de control, el sistema compara continuamente la temperatura medida con el rango objetivo de operación. Si la temperatura se encuentra por debajo del intervalo deseado, se activa el elemento calefactor; si supera el límite superior, se desactiva el calefactor y se habilita el ventilador. Cuando la temperatura se encuentra dentro del rango, el sistema indica condición normal mediante el LED verde.

#### Diagrama de flujo / fragmento de código
![Diagrama de flujo o captura del código principal](imagenes/diagrama_flujo_codigo.png)

---

### Simulación del sistema en Wokwi
Con el fin de documentar el diseño y validar de forma visual la lógica de control, se desarrolló una simulación funcional del sistema en **Wokwi**. En esta simulación se representaron los principales elementos del prototipo presentado en laboratorio:

- **ESP32** como unidad de adquisición y control,
- **pantalla OLED** para visualización de variables,
- **sensor DHT22** para la medición de temperatura y humedad,
- **módulo HX711** para la estimación del peso,
- **módulo relé** para el accionamiento del bombillo,
- **ventilador** representado de forma equivalente,
- **panel de LEDs** para señalización del estado térmico.

Debido a las limitaciones propias del entorno de simulación, la etapa de potencia real compuesta por **transformador, bombillo de 120 V y ventilador alimentado externamente** se representó de forma **conceptual o equivalente**, manteniendo la misma lógica funcional del prototipo físico. Esto permitió documentar de manera clara la relación entre sensores, microcontrolador, sistema de visualización y actuadores.

La simulación permitió:
- validar el comportamiento lógico del sistema,
- documentar el circuito para el repositorio de GitHub,
- evidenciar la integración de los módulos electrónicos utilizados,
- complementar las fotografías del montaje real con una representación clara del sistema completo.

#### Vista general de la simulación
![Vista general de la simulación en Wokwi](imagenes/simulacion_wokwi_general.png)

#### Detalle de actuadores
![Detalle del relé, bombillo y ventilador en simulación](imagenes/simulacion_wokwi_actuadores.png)

#### Detalle de sensores y visualización
![Detalle de OLED, DHT22 y HX711 en simulación](imagenes/simulacion_wokwi_sensores.png)

#### Enlaces
**Repositorio de GitHub:**  
[Pegar aquí enlace del repositorio](PEGAR_AQUI_ENLACE_DEL_REPOSITORIO)

**Simulación en Wokwi:**  
[Pegar aquí enlace de la simulación](PEGAR_AQUI_ENLACE_DE_WOKWI)

---

### Diseño de la Estructura
Para realizar la estrutura, se empleo una caja de plástico, la cual se le quitó la tapa y se diseñó una cúpula con cartón y acetato, se le reliazaron unos cortes a la caja para tener una entrada del neonato y así mismo entradas más pequeñas para manipularlo sin necesidad de abrir la caja. También se le hizo el acondicionamiiento para posicionar el bombillo, el ventilador, la galga para medir el peso y el sensor de temperatura.

#### Diseño estructural
![Diseño estructural de la incubadora](imagenes/diseno_estructura.jpg)

### Diseño final
Incorporando la estructura y todo el sistema electrónico en una cajita al ldao, donde por uno de los laterales se puede visualizar por mmedio de una Oled los valores de temperatura y peso; Por medio de LEDs indicar la situación en la que se ecnuentra el neonato dependiendo su temperatura, siendo así el azul un estado de baja temperatura <36°C, verde el estado ideal de la incubadora donde la temperatura oscila entre los 36 y 37.5°C y rojo ya una temperatura superior a esta que podría llegar a calentar de más al neonato.

#### Vista general del diseño final
[![incubadora1.jpg](https://i.postimg.cc/Pq6fqhJt/incubadora1.jpg)](https://postimg.cc/bGtf671M)

#### Vista lateral del prototipo
[![incubadora2.jpg](https://i.postimg.cc/MZfZzCSK/incubadora2.jpg)](https://postimg.cc/0rx1fHjL)

#### Vista complementaria del montaje
[![incubadora3.jpg](https://i.postimg.cc/pddx47Cb/incubadora3.jpg)](https://postimg.cc/qNW9C1Wj)

#### Circuito montado
[![circuitoincubadora.jpg](https://i.postimg.cc/ydgKYZ2M/circuitoincubadora.jpg)](https://postimg.cc/vgsk0cYh)

#### Evidencia de estado por baja temperatura
[![Hipotermia.jpg](https://i.postimg.cc/66ZKkCr7/Hipotermia.jpg)](https://postimg.cc/14yb6nYP)

#### Evidencia de estado en rango normal
[![Normal.jpg](https://i.postimg.cc/zXSrB5PV/Normal.jpg)](https://postimg.cc/6y3SbsKX)

#### Evidencia de estado por temperatura alta
[![Alta.jpg](https://i.postimg.cc/zfMmMf3F/Alta.jpg)](https://postimg.cc/B8xwP4Tj)

---

## Análisis
### Pregunta 1: ¿Qué otras variables son críticas en el monitoreo neonatal?
Además de temperatura y peso, existen otras variables fisiológicas y ambientales igualmente críticas. La frecuencia cardíaca y la saturación de oxígeno (SpO₂) son esenciales dado que los neonatos prematuros son propensos a episodios de apnea y bradicardia, y una caída en SpO₂ puede generar daño hipóxico en órganos en desarrollo. La frecuencia respiratoria permite detectar dificultad respiratoria, una de las principales causas de mortalidad neonatal. El nivel de ruido también importa, pues valores superiores a 45 dB al interior de la cabina se asocian con alteraciones del sueño y efectos negativos sobre el desarrollo auditivo. Por último, la concentración de oxígeno debe regularse activamente, ya que tanto la hipoxia como la hiperoxia son nocivas para el neonato prematuro.

### Pregunta 2: ¿Qué haría falta para convertir el prototipo en una incubadora real?
Técnicamente, se requeriría un controlador PID más robusto capaz de mantener el error de temperatura por debajo de ±0,5 °C, junto con sensores adicionales de SpO₂, frecuencia cardíaca y ruido, un sistema de humidificación activa en lazo cerrado, y materiales biocompatibles esterilizables. Desde el punto de vista regulatorio, el dispositivo debería cumplir la norma IEC 60601-2-19 y obtener registro sanitario ante el INVIMA como dispositivo médico, lo que implica pruebas de biocompatibilidad, validación de software y documentación técnica exhaustiva.

### Pregunta 3: ¿Qué semejanzas hay entre una incubadora neonatal y una servo-cuna?
Ambos dispositivos tienen el mismo propósito: proveer un ambiente térmico neutro al neonato. Los dos emplean servocontrol con sensor cutáneo abdominal, incorporan alarmas de temperatura fuera de rango y permiten integración con equipos de monitoreo de signos vitales. La diferencia fundamental es el mecanismo de transferencia de calor: la incubadora usa convección en un ambiente cerrado, mientras que la servo-cuna usa radiación infrarroja en un sistema abierto, lo que la hace preferible cuando se requiere acceso inmediato al paciente.

## Conclusiones
La práctica permitió comprender el funcionamiento de una incubadora neonatal desde la perspectiva de la ingeniería de control y los circuitos electrónicos, demostrando que es técnicamente factible controlar la temperatura de una cabina y estimar el peso del neonato con componentes de bajo costo. Sin embargo, el ejercicio también evidenció las brechas significativas entre un prototipo académico y un dispositivo médico certificado, tanto en precisión de control como en cumplimiento normativo. Más allá de las variables abordadas, el cuidado neonatal es intrínsecamente multivariable, lo que subraya la complejidad real de estos equipos y la importancia de una formación sólida en metrología, normativa y validación clínica para el ingeniero biomédico.

## Referencias
[1] C. G. K. Tran, A. Gibson, D. Wong, D. Tilahun, N. Selock, T. Good, ... G. Rao, “Designing a low-cost multifunctional infant incubator,” J. Lab. Autom., vol. 19, no. 3, pp. 332–337, Jun. 2014. https://doi.org/10.1177/2211068214530391.

[2] L. Restrepo-Pérez, N. Durango-Londoño, N. E. Gómez-Suárez, F. González-Ramírez, y N. Rivera-Bonilla, “Prototipo de incubadora neonatal,” Revista Ingeniería Biomédica, vol. 1, no. 1, pp. 55–59, 2007. Available at: http://www.scielo.org.co/pdf/rinbi/v1n1/v1n1a12.pdf.

[3] M. van Leeuwen, O. Frauenfelder, M. Oude-Reimer, F. Camba, M. Ceccatelli, I. Hankes-Drielsma, A. Kalbér, T. Kühn, y E. Silva, European Standards of Care for Newborn Health: Temperature management in newborn infants. European Foundation for the Care of Newborn Infants (EFCNI), Nov. 2018. Disponible en: https://newborn-health-standards.org/standards/standards-english/care-procedures/temperature-management-in-newborn-infants/.

[4] R. B. Knobel-Dail, “Role of effective thermoregulation in premature neonates,” Research and Reports in Neonatology, vol. 4, pp. 147–156, 2014. https://doi.org/10.2147/RRN.S52377.

[5] R. E. Black, S. Cousens, H. L. Johnson et al., “Global, regional, and national causes of child mortality in 2008: a systematic analysis,” Lancet, vol. 375, pp. 1969–1987, Jun. 2010. https://doi.org/10.1016/S0140-6736(10)60549-1.

[6] V. DeFrancesco, “Perinatology,” in Clinical Engineering Handbook, 2004, pp. 410–416. doi: 10.1016/b978-012226570-9/50102-2.

[7] “Frank’s infant incubators.” http://www.frankshospitalworkshop.com/equipment/infant_incubators_equipment.html

[8] E. F. Bell, “Infant incubators and radiant warmers,” Early Human Development, vol. 8, no. 3–4, pp. 351–375, Oct. 1983, doi: 10.1016/0378-3782(83)90018-x.

[9] O. Yeler and M. F. Koseoglu, “Energy efficiency and transient-steady state performance comparison of a resistance infant incubator and an improved thermoelectric infant incubator,” Engineering Science and Technology an International Journal, vol. 31, p. 101055, Sep. 2021, doi: 10.1016/j.jestch.2021.09.001.

[10] “Infant Incubators | Biomedical Instrumentation & Technology,” Biomedical Instrumentation & Technology. https://array.aami.org/doi/full/10.2345/i0899-8205-40-3-215.1

[11] M. Abdiche, G. Farges, S. Delanaud, V. Bach, P. Villon, and J.-P. Libert, “Humidity control tool for neonatal incubator,” Medical & Biological Engineering & Computing, vol. 36, no. 2, pp. 241–245, Mar. 1998, doi: 10.1007/bf02510752.

[12] P. A. Aya-Parra, A. J. Rodriguez-Orjuela, V. R. Torres, N. P. C. Hernandez, N. M. Castellanos, and J. Sarmiento-Rojas, “Monitoring System for Operating Variables in Incubators in the Neonatology Service of a Highly Complex Hospital through the Internet of Things (IoT),” Sensors, vol. 23, no. 12, p. 5719, Jun. 2023, doi: 10.3390/s23125719.

[13] A. R. Midgley et al., “Monitoring dynamic responses of perifused neuroendocrine tissues to stimuli in real time,” in Methods in neurosciences, 1995, pp. 188–219. doi: 10.1016/S1043-9471(06)80034-0.

[14] R. Cuervo, M. A. Rodríguez-Lázaro, R. Farré, D. Gozal, G. Solana, and J. Otero, “Low-cost and open-source neonatal incubator operated by an Arduino microcontroller,” HardwareX, vol. 15, p. e00457, Jul. 2023, doi: 10.1016/j.ohx.2023.e00457.

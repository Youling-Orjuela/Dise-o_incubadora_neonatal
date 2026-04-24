# Diseno incubadora neonatal

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

### Simulación del circuito de temperatura
Con el fin de validar el comportamiento del sistema térmico, se desarrolló una simulación específica del circuito de temperatura en **Wokwi**. En esta simulación se representaron los elementos principales asociados al control térmico del prototipo: **ESP32**, **sensor DHT22**, **pantalla OLED**, **módulo relé**, **bombillo calefactor**, **ventilador** y **panel de LEDs**.

La lógica implementada permite identificar tres estados térmicos:
- **Temperatura baja**: se activa el bombillo calefactor y se enciende el LED de baja temperatura.
- **Temperatura en rango**: se enciende el LED verde para indicar condición adecuada.
- **Temperatura alta**: se apaga el bombillo y se activa el ventilador para disipar calor.

Esta simulación permitió comprobar de forma visual la interacción entre el sensor de temperatura, la unidad de control y los actuadores del sistema.

<img width="776" height="526" alt="image" src="https://github.com/user-attachments/assets/c68bc2f1-49a8-4a8d-ad04-c687fc074c6c" />


**Enlace a la simulación de temperatura:**  
https://wokwi.com/projects/462155404758716417

---

### Simulación del sistema de peso
De manera complementaria, se desarrolló una simulación independiente del sistema de medición de peso, con el objetivo de representar la adquisición de datos desde una **celda de carga** por medio del módulo **HX711**, y su posterior visualización en la **pantalla OLED**.

En esta simulación se incluyeron la **ESP32**, la **pantalla OLED** y el **módulo HX711** como elementos principales. La finalidad de este montaje fue mostrar la arquitectura general de medición de peso implementada en el prototipo, así como la relación entre el sensor de fuerza y la etapa de procesamiento digital.

Aunque la calibración del sistema en el montaje real presentó limitaciones, la simulación permitió documentar claramente la estructura del sistema de pesaje y su integración con el microcontrolador.

<img width="810" height="496" alt="image" src="https://github.com/user-attachments/assets/01c12997-0cb2-4c5b-82f8-8835659884ef" />


**Enlace a la simulación de peso:**  
https://wokwi.com/projects/462156450476540929

---

### Simulación general del sistema
Finalmente, se elaboró una simulación general del prototipo en **Wokwi**, integrando en un mismo entorno los módulos principales del sistema presentado en laboratorio:
- **ESP32** como unidad de adquisición y control.
- **Pantalla OLED** para visualización de temperatura y peso.
- **Sensor DHT22** para medición de temperatura y humedad.
- **Módulo HX711** para el sistema de medición de peso.
- **Módulo relé** para el accionamiento del bombillo.
- **Ventilador** representado de forma equivalente.
- **Panel de LEDs** para señalización del estado térmico.

Debido a las limitaciones propias del entorno de simulación, la etapa de potencia real compuesta por **transformador, bombillo de 120 V y ventilador alimentado externamente** se representó de forma conceptual o equivalente, manteniendo la misma lógica funcional del montaje físico. Esta simulación fue útil para documentar el sistema completo, validar su comportamiento lógico y complementar las evidencias del prototipo real.

<img width="1477" height="595" alt="image" src="https://github.com/user-attachments/assets/9910ebc9-a02b-4bb3-b468-d32bce883ce1" />


**Enlace a la simulación general:**  
https://wokwi.com/projects/462153338274913281
---

## Explicación del código de la incubadora neonatal

## Librerías e instancias de hardware
```cpp
#include <Wire.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>
#include <DHT.h>
#include "HX711.h"

#define DHTPIN     4
#define DHTTYPE    DHT22

#define OLED_SDA   21
#define OLED_SCL   22

#define LED_OK     32
#define LED_LOW    19
#define LED_HIGH   25

#define FAN_PIN    33
#define RELAY_PIN  13

#define HX_DT      26
#define HX_SCK     27

#define SCREEN_WIDTH 128
#define SCREEN_HEIGHT 64
#define OLED_ADDR 0x3C

Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, -1);
DHT dht(DHTPIN, DHTTYPE);
HX711 scale;
```

Este bloque declara las librerías necesarias para el funcionamiento del sistema y crea las instancias de los principales periféricos del prototipo.

`Wire.h` es la librería estándar de Arduino para la comunicación I2C. Este protocolo utiliza dos líneas, `SDA` y `SCL`, y permite conectar dispositivos como la pantalla OLED con un número reducido de cables. En este proyecto se utiliza para establecer la comunicación entre la ESP32 y la pantalla.

`Adafruit_GFX.h` y `Adafruit_SSD1306.h` permiten controlar la pantalla OLED. La primera ofrece funciones gráficas básicas, como escribir texto o dibujar elementos, mientras que la segunda implementa el controlador específico del display SSD1306.

`DHT.h` se utiliza para la lectura del sensor DHT22, el cual proporciona información de temperatura y humedad relativa. Estas variables son críticas dentro de la incubadora, ya que permiten conocer el estado térmico del ambiente interno.

`HX711.h` permite manejar el módulo HX711, encargado de acondicionar y digitalizar la señal proveniente de la celda de carga. Dado que la galga genera señales eléctricas muy pequeñas, este módulo es necesario para que la ESP32 pueda interpretar la medición de peso.

En este mismo bloque se definen los pines físicos del sistema. Se asignan los pines del sensor DHT22, la pantalla OLED, los LEDs indicadores, el ventilador, el relé y el sistema de medición de peso.

---

## Umbrales y parámetros de control
```cpp
const float TEMP_LOW  = 36.0;
const float TEMP_HIGH = 37.5;

const float FAN_ON_TEMP  = 37.5;
const float FAN_OFF_TEMP = 37.2;

bool relayActiveLow = true;
float calibration_factor = -359834.0;
```

Este bloque define los parámetros de referencia para el funcionamiento del sistema.

`TEMP_LOW` y `TEMP_HIGH` delimitan el rango ideal de temperatura de la incubadora. Si la temperatura baja de 36 °C, se interpreta una condición de hipotermia. Si la temperatura supera 37.5 °C, el sistema considera una condición de sobrecalentamiento.

`FAN_ON_TEMP` y `FAN_OFF_TEMP` establecen la histéresis del ventilador. Esto significa que el ventilador no se activa y desactiva exactamente en el mismo valor, lo cual evita conmutaciones rápidas y mejora la estabilidad del sistema.

La variable `relayActiveLow` indica que el relé utilizado se activa con nivel lógico bajo. Finalmente, `calibration_factor` corresponde al factor de calibración experimental del módulo HX711, el cual se emplea para convertir la lectura de la celda de carga en una estimación de peso.

---

## Variables globales del sistema
```cpp
float temperature = NAN;
float humidity    = NAN;
float weight_kg   = 0.0;
long  weight_raw  = 0;

bool fanState    = false;
bool heaterState = false;
bool hxReady     = false;
```

En esta sección se declaran las variables globales que almacenan el estado actual del sistema.

`temperature` y `humidity` guardan las lecturas del sensor DHT22. Se inicializan como `NAN` para indicar que al comienzo del programa aún no existe una lectura válida.

`weight_kg` almacena el peso calculado en kilogramos, mientras que `weight_raw` conserva la lectura cruda del HX711 para fines de depuración.

`fanState` y `heaterState` representan el estado del ventilador y del bombillo calefactor, respectivamente. `hxReady` verifica si el módulo HX711 fue inicializado correctamente y está listo para trabajar.

---

## Función de control de LEDs
```cpp
void setLEDs(bool okLed, bool lowLed, bool highLed) {
  digitalWrite(LED_OK, okLed ? HIGH : LOW);
  digitalWrite(LED_LOW, lowLed ? HIGH : LOW);
  digitalWrite(LED_HIGH, highLed ? HIGH : LOW);
}
```

Esta función simplifica el control del panel de LEDs del sistema.

Recibe tres parámetros booleanos, uno para cada LED: temperatura normal, temperatura baja y temperatura alta. Dependiendo de estos valores, la función enciende o apaga cada indicador mediante `digitalWrite()`.

Desde el punto de vista funcional, esta sección corresponde a la capa de señalización visual del prototipo, permitiendo mostrar rápidamente el estado térmico de la incubadora.

---

## Función de control del relé
```cpp
void setRelay(bool on) {
  heaterState = on;
  if (relayActiveLow) {
    digitalWrite(RELAY_PIN, on ? LOW : HIGH);
  } else {
    digitalWrite(RELAY_PIN, on ? HIGH : LOW);
  }
}
```

Esta función controla el relé encargado de accionar el bombillo calefactor.

El parámetro `on` indica si el calefactor debe encenderse o apagarse. Como el módulo relé utilizado trabaja con lógica activa en bajo, cuando se desea encender el bombillo se escribe `LOW` en el pin de control. Si el relé trabajara con lógica activa en alto, la función usaría la condición contraria.

Además de cambiar el estado físico del relé, la función actualiza la variable `heaterState`, lo cual permite reflejar el estado del calefactor en la pantalla OLED y en el monitor serial.

---

## Función para clasificar el estado térmico
```cpp
const char* estadoTermico(float t) {
  if (isnan(t)) return "ERROR";
  if (t < TEMP_LOW) return "BAJA";
  if (t > TEMP_HIGH) return "ALTA";
  return "NORMAL";
}
```

Esta función clasifica la temperatura medida en una categoría fácilmente interpretable por el usuario.

Si la lectura no es válida, devuelve `ERROR`. Si la temperatura está por debajo del rango establecido, devuelve `BAJA`. Si la temperatura supera el límite superior, devuelve `ALTA`. En caso contrario, devuelve `NORMAL`.

Esta abstracción permite traducir un valor numérico en una descripción textual del estado térmico del sistema.

---

## Actualización automática de LEDs
```cpp
void actualizarLEDs(float t) {
  if (isnan(t)) {
    setLEDs(false, false, false);
  } else if (t < TEMP_LOW) {
    setLEDs(false, true, false);
  } else if (t > TEMP_HIGH) {
    setLEDs(false, false, true);
  } else {
    setLEDs(true, false, false);
  }
}
```

Esta función traduce la temperatura medida en una señal visual inmediata.

Si la temperatura está por debajo del rango, se activa el LED de baja temperatura. Si está por encima del rango, se activa el LED de alta temperatura. Si la temperatura se encuentra dentro del intervalo deseado, se enciende el LED verde de condición normal.

Con esto, el usuario puede identificar rápidamente el estado de la incubadora sin necesidad de leer la pantalla.

---

## Lectura del sensor DHT22
```cpp
void leerDHT() {
  float t = dht.readTemperature();
  float h = dht.readHumidity();

  if (!isnan(t)) temperature = t;
  if (!isnan(h)) humidity = h;
}
```

Esta rutina se encarga de adquirir la información del sensor DHT22.

La ESP32 consulta periódicamente la temperatura y la humedad del ambiente interno del prototipo. Si las lecturas son válidas, estas se almacenan en las variables globales `temperature` y `humidity`.

Esto permite que el sistema use estos datos tanto para control como para visualización.

---

## Control del ventilador
```cpp
void actualizarVentilador(float t) {
  if (isnan(t)) {
    fanState = false;
  } else {
    if (t >= FAN_ON_TEMP) {
      fanState = true;
    } else if (t <= FAN_OFF_TEMP) {
      fanState = false;
    }
  }

  digitalWrite(FAN_PIN, fanState ? HIGH : LOW);
}
```

Esta función implementa la lógica de enfriamiento del sistema.

Cuando la temperatura supera el umbral superior, el ventilador se activa para ayudar a disipar calor dentro de la incubadora. Cuando la temperatura vuelve a un valor seguro, el ventilador se apaga.

El uso de dos umbrales distintos introduce histéresis, lo cual evita oscilaciones rápidas del actuador y mejora la estabilidad del control.

---

## Control del bombillo calefactor
```cpp
void actualizarBombillo(float t) {
  if (isnan(t)) {
    setRelay(false);
    return;
  }

  if (t < TEMP_HIGH) setRelay(true);
  else               setRelay(false);
}
```

Esta función gestiona el calentamiento del sistema.

Si la temperatura es menor al umbral superior, el bombillo calefactor permanece encendido. Si la temperatura supera ese límite, el relé se desactiva y el bombillo se apaga.

Este bloque representa la acción del calefactor dentro del lazo de control térmico de la incubadora.

---

## Inicialización del HX711
```cpp
void iniciarHX711() {
  scale.begin(HX_DT, HX_SCK);
  delay(3000);

  if (scale.is_ready()) {
    scale.tare(20);
    scale.set_scale(calibration_factor);
    hxReady = true;
    Serial.println("HX711 listo");
  } else {
    hxReady = false;
    Serial.println("HX711 no responde");
  }
}
```

Este bloque inicia la comunicación con el módulo HX711 y verifica si el sistema de pesaje está disponible.

Si la inicialización es exitosa, se aplica el factor de calibración y se realiza una tara inicial. Esto permite que las mediciones posteriores representen únicamente la carga aplicada y no el peso propio de la estructura.

Si el módulo no responde, el sistema informa la falla y evita usar lecturas no confiables.

---

## Lectura del peso
```cpp
void leerPeso() {
  if (!hxReady) return;
  if (!scale.is_ready()) return;

  weight_raw = scale.read_average(10);

  float w = scale.get_units(5);

  if (w < 0) w = -w;
  if (w < 0.01) w = 0.0;

  weight_kg = w;
}
```

Esta función realiza la lectura del sistema de pesaje.

Primero verifica que el HX711 esté correctamente inicializado. Luego toma una lectura promedio y la convierte a kilogramos usando el factor de calibración. También almacena una lectura cruda para fines de depuración.

Finalmente, corrige pequeñas fluctuaciones cercanas a cero para evitar mostrar ruido como si fuera peso real.

---

## Visualización en pantalla OLED
```cpp
void mostrarOLED() {
  display.clearDisplay();
  display.setTextSize(1);
  display.setTextColor(SSD1306_WHITE);
  display.setCursor(0, 0);

  display.println("Incubadora neonatal");
  display.println("-------------------");

  display.print("Temp: ");
  if (isnan(temperature)) display.println("ERROR");
  else {
    display.print(temperature, 1);
    display.println(" C");
  }

  display.print("Hum : ");
  if (isnan(humidity)) display.println("ERROR");
  else {
    display.print(humidity, 1);
    display.println(" %");
  }

  display.print("Peso: ");
  display.print(weight_kg, 3);
  display.println(" kg");

  display.print("Estado: ");
  display.println(estadoTermico(temperature));

  display.print("Fan: ");
  display.println(fanState ? "ON" : "OFF");

  display.print("Bomb: ");
  display.println(heaterState ? "ON" : "OFF");

  display.display();
}
```

Esta función organiza toda la información relevante del sistema en la pantalla OLED.

En ella se muestran temperatura, humedad, peso, estado térmico y estado de los actuadores. Esto permite que el usuario observe en tiempo real el comportamiento de la incubadora sin recurrir al computador.

---

## Visualización por monitor serial
```cpp
void mostrarSerial() {
  Serial.println("---------------");

  Serial.print("Temp: ");
  if (isnan(temperature)) Serial.println("ERROR");
  else {
    Serial.print(temperature, 2);
    Serial.println(" C");
  }

  Serial.print("Hum : ");
  if (isnan(humidity)) Serial.println("ERROR");
  else {
    Serial.print(humidity, 2);
    Serial.println(" %");
  }

  Serial.print("RAW: ");
  Serial.print(weight_raw);
  Serial.print(" | Peso: ");
  Serial.print(weight_kg, 3);
  Serial.println(" kg");

  Serial.print("Estado: ");
  Serial.println(estadoTermico(temperature));

  Serial.print("Ventilador: ");
  Serial.println(fanState ? "ON" : "OFF");

  Serial.print("Bombillo: ");
  Serial.println(heaterState ? "ON" : "OFF");
}
```

Además de la OLED, el sistema también envía información al monitor serial. Esto facilita la depuración del prototipo y permite observar con mayor detalle las variables internas, como la lectura cruda del HX711.

---

## Configuración inicial del sistema (`setup`)
```cpp
void setup() {
  Serial.begin(115200);
  delay(500);

  pinMode(LED_OK, OUTPUT);
  pinMode(LED_LOW, OUTPUT);
  pinMode(LED_HIGH, OUTPUT);
  setLEDs(false, false, false);

  pinMode(FAN_PIN, OUTPUT);
  digitalWrite(FAN_PIN, LOW);

  pinMode(RELAY_PIN, OUTPUT);
  setRelay(false);

  Wire.begin(OLED_SDA, OLED_SCL);
  if (!display.begin(SSD1306_SWITCHCAPVCC, OLED_ADDR)) {
    Serial.println("OLED no encontrada");
    while (true) delay(1000);
  }

  display.clearDisplay();
  display.setCursor(0, 0);
  display.println("INCUBADORA UMNG");
  display.println("Inicializando...");
  display.display();

  dht.begin();
  delay(500);

  iniciarHX711();

  display.clearDisplay();
  display.setCursor(0, 0);
  display.println("INCUBADORA UMNG");
  display.println("Lista!");
  display.display();
  delay(1000);
}
```

La función `setup()` se ejecuta una sola vez al iniciar el sistema. En ella se configuran los pines de entrada y salida, se inicializa la comunicación con la OLED, el DHT22 y el HX711, y se define el estado seguro inicial de los actuadores.

Esta etapa es fundamental porque garantiza que el sistema arranque en condiciones controladas y que todos los periféricos estén correctamente listos antes de iniciar el lazo principal.

---

## Bucle principal de funcionamiento (`loop`)
```cpp
void loop() {
  leerDHT();
  leerPeso();

  actualizarLEDs(temperature);
  actualizarVentilador(temperature);
  actualizarBombillo(temperature);

  mostrarOLED();
  mostrarSerial();

  delay(800);
}
```

La función `loop()` constituye el ciclo principal de ejecución del sistema. En cada iteración se leen los sensores, se actualiza la lógica de control y se muestran los resultados tanto en la OLED como en el monitor serial.

Este ciclo repetitivo convierte a la incubadora en un sistema dinámico de monitoreo y control en tiempo real.

### Diseño de la Estructura
Para realizar la estrutura, se empleo una caja de plástico, la cual se le quitó la tapa y se diseñó una cúpula con cartón y acetato, se le reliazaron unos cortes a la caja para tener una entrada del neonato y así mismo entradas más pequeñas para manipularlo sin necesidad de abrir la caja. También se le hizo el acondicionamiiento para posicionar el bombillo, el ventilador, la galga para medir el peso y el sensor de temperatura.

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

## Análisis de Costos de Implementación
El sistema de incubadora neonatal a escala desarrollado presenta un costo total aproximado de $200.000 COP. Este valor se puede discriminar en dos grandes componentes: electrónicos y de diseño. Para esto, se tiene que en los componentes electrónicos (estos incluyen todos los sensores, resistencias, transformador, capacitores, ventilador y demás) el gasto fue de aproximadamente $150.000 COP, mientras que a nivel de diseño (caja plástica, cinta, cartón piedra, entre otros) se gastó $50.000 COP. 

Las incubadoras neonatales comerciales presentan características mucho más avanzadas, lo cual impacta directamente su costo. La empresa Dräger fabrica incubadoras de alta gama como la serie Isolette, llegando a costar mas de 100 millones COP. Por su parte, Instrumentalia S.A.S, tiene incubadoras para Colombia a partir de los 50 millones COP. LEEX Medical es la empresa mas accesible, ofreciendo incubadoras neonatales a partir de los 20 millones COP.

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

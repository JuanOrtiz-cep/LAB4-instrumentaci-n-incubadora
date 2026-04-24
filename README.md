# LAB4-instrumentación-incubadora


# README.md

# Diseño y Construcción de una Incubadora Neonatal a Escala

Catalina Martínez Franco
Joseph Rodríguez 
Juan Esteban Ortiz

Universidad Militar Nueva Granada
Ingeniería Biomédica

---

## 1. Introducción

En este laboratorio se diseñó y construyó un prototipo funcional de incubadora neonatal a escala, orientado al control de variables críticas para la supervivencia del recién nacido, principalmente temperatura y peso. El sistema fue desarrollado mediante principios de electrónica analógica, sensores biomédicos y sistemas de control en lazo cerrado. Para este se hace la siguiente revisión bibliográfica.

### 2. Marco Teórico

Una incubadora neonatal es un dispositivo médico diseñado para proporcionar al neonato un ambiente controlado similar al vientre materno, garantizando condiciones térmicas adecuadas, protección frente al entorno externo y monitoreo constante de variables fisiológicas [1], [2].

Uno de los parámetros más importantes es la temperatura corporal, la cual debe mantenerse cercana a **37 °C**, especialmente en neonatos prematuros, quienes presentan menor capacidad de termorregulación debido a inmadurez fisiológica y baja cantidad de tejido adiposo [3], [4].

Para lograrlo, las incubadoras emplean sistemas de calefacción por convección forzada, sensores térmicos y controladores automáticos que ajustan el calentamiento según la temperatura interna.

Además del control térmico, también es importante el monitoreo del peso neonatal, ya que permite evaluar crecimiento, hidratación y evolución clínica.

La presente práctica consistió en diseñar una incubadora neonatal a escala capaz de regular temperatura entre **36 °C y 37.5 °C**, medir peso simulado y visualizar el estado operativo mediante indicadores luminosos.


## 2.1 Importancia de la Termorregulació y Peso Neonatal.

Los recién nacidos prematuros presentan alta susceptibilidad a padecer hipotermia, hipertermia, deshidratación, estrés metabólico e inestabilidad cardiorrespiratoria. Cuando se habla de una incubadora se habla de un dispositivo que crea un ambiente controlado en temperatura, humedad y ventilación, además de otras posibles variables que ayudan a la vigilancia de un neonato prematuro, por ejemplo el peso. 
Este ambiente controlado pretende simular un vientre materno y por esto mismo controlar la temperatura es vital, ya que la temperatura de un vientre materno sano es de aproximadamente 36-36,5°C a 37-37,5°C según la fuente. Para ello la incubadora debe mantener temperatura estable dentro de rangos clínicamente seguros.
Por esto mismo, el peso neonatal es igual de importante y es otro referente que permite detectar alteraciones nutricionales, retención de líquidos o pérdida excesiva de masa corporal, ya que es posible comparar el desarrollo de un neonato en condiciones normales con uno prematuro en incubadora. El peso puede medirse mediante sensores resistivos o galgas extensiométricas.

## 2.2 Sistema de Control en Lazo Cerrado

Un sistema de lazo cerrado compara la temperatura medida con una referencia deseada y corrige automáticamente el error.
e(t)=T_{ref}-T(t)
Donde:
* (T_{ref}): temperatura deseada
* (T(t)): temperatura real interna

---

## 3. Objetivos

### 3.1 Objetivo General

Reconocer la importancia de las incubadoras neonatales en la salud del neonato.

### 3.2 Objetivos Específicos

- Identificar las partes principales que componen una incubadora neonatal.
- Desarrollar un sistema que emule el modo de operación de una incubadora
neonatal.
- Evaluar cómo impacta el control de variables como temperatura, humedad y
flujo de aire en la salud del neonato.
---

## 4. Diseño de la incubadora neonatal a escala
# 1) 
Con base en las indicaciones de medida, con un minimo de 45cm x 20cm x22cm se eligío una caja plástica común de medidas exactas de 41cm x 29cm x 17.3cm, quedando corta en terminos de altura, esto se pretendía equilibrar con una base o cúpula que tuviera mayor altura, sin embargo por facilidad y simetría no se cambió. De igual forma la caja seleccionada es transparente, para poder tener la visibilidad deseada.

A continuación se realizó la implementación de la galga ó celda a presión, lo primero que se debe hacer es establecer una plataforma fija y estable, de tal manera que se eviten movimientos inestables, inclinaciones no deseadas o valores negativos por las mismas circunstancias. La base fija se realizó con retablos de madera para la base principal que esta fijada al suelo de la caja por medio de tornillos y roscas, también se utilizó una como área de pesaje otro retablo y fue fijado de la misma forma.

Al tener una base fija montada se procede a realizar la calibración de la celda, este mediante un código y un peso conocido, el proceso es colocar el peso sobre la celda y obtenemos un valor, este valor se divide en el peso real del objeto que utilizamos, de tal manera que se calibra. 
Después de calibrarla usamos otro código para que muestre el peso en tiempo real con un filtro suavizado para que no tarde en reflejar el peso real, todo esto cuidando la estructura y evitando la inestabilidad del sistema, de esta manera la celda de presión queda calibrada y funcionando de manera correcta.


<img width="370" height="160" alt="image" src="https://github.com/user-attachments/assets/a454797d-052b-4b0a-800f-4259608fa1d2" />


Para la parte del calentamiento se utilizó una bombilla de 53 watts, se realizó un orificio para su entrada exacta y que quedara en la parte alta de la incubadora, el bombillo incluye su conexión a tomacorriente.



<img width="960" height="1280" alt="image" src="https://github.com/user-attachments/assets/e4011d76-1f38-4811-b26d-5ef209d66e30" />

Foto bombilla

# 2)
Una vez se tiene como pesar y calentar, se implementan el sensor termocupla NTC 10k B3950, este nos permitiría saber a que temperatura se encuentra el interior de la incubadora, con lo anterior se incluye un sistema de enfriamiento consistente en un ventilador de 12V-100mA, este está instalado en un lateral centrado de la caja con la intención de que se encienda una vez alcanzados los 37 °C, con el fin de que nunca sobrepase el límite de los 37.5 °C, del mismo modo cuando llegué a bajar la temperatura, está programado para que el ventilador vuelva a apagarse, de tal forma que no sigue "enfirando" y así mantener el equilibrio. Esto se visualiza mejor en el código.

El ventilador es alimentado con baterías de 9v, también puede alimentarse con fuente mostrando mejores resultados.


<img width="960" height="1280" alt="image" src="https://github.com/user-attachments/assets/06b02677-80fd-4ad1-be65-d1ef8fe693f9" />



<img width="183" height="206" alt="image" src="https://github.com/user-attachments/assets/8941bb2e-f1e4-41bd-a5c2-92137c6f06af" />


```
#include <OneWire.h>
#include <DallasTemperature.h>
#include "HX711.h"
#include <Wire.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>

//oled
#define SCREEN_WIDTH 128
#define SCREEN_HEIGHT 64

Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, -1);

//TEMPERATURA
#define PIN_TEMP 18
#define PIN_FAN 23  
#define LED_VERDE 19
#define LED_BAJO 2
#define LED_ALTO 15 

OneWire oneWire(PIN_TEMP);
DallasTemperature sensors(&oneWire);

float temp;

//BALANZA
#define DT 4
#define SCK 5

HX711 celda;

float factor_calibracion = 433.91812865497;
float peso_filtrado = 0;

//
void setup() {
  Serial.begin(115200);

  // OLED
  Wire.begin(21, 22);
  if(!display.begin(SSD1306_SWITCHCAPVCC, 0x3C)) {
    Serial.println("Fallo OLED");
    while(true);
  }
  display.clearDisplay();
  display.setTextColor(WHITE); // 🔥 IMPORTANTE

  // Temperatura
  pinMode(LED_VERDE, OUTPUT);
  pinMode(LED_BAJO, OUTPUT);
  pinMode(LED_ALTO, OUTPUT);
  pinMode(PIN_FAN, OUTPUT);
  sensors.begin();

  // Balanza
  celda.begin(DT, SCK);
  celda.set_scale(factor_calibracion);

  delay(2000);
  celda.tare();

  Serial.println("Sistema listo");
}

//control 
void loop() {

  // TEMP
  sensors.requestTemperatures();
  temp = sensors.getTempCByIndex(0);

  Serial.print("Temp (C): ");
  Serial.print(temp);

  // CONTROL DE TEMPERATURA Y LEDS
  if (temp > 37.5) {
  
  digitalWrite(LED_VERDE, LOW);
  digitalWrite(LED_BAJO, LOW);
  digitalWrite(LED_ALTO, HIGH);
  } 
  else if (temp > 37) {
    digitalWrite(PIN_FAN, HIGH);

    digitalWrite(LED_VERDE, HIGH);
    digitalWrite(LED_BAJO, LOW);
    digitalWrite(LED_ALTO, LOW);
  }
  else if (temp > 36) {
    
    digitalWrite(LED_VERDE, HIGH);
    digitalWrite(LED_BAJO, LOW);
    digitalWrite(LED_ALTO, LOW);
  }
  else if (temp < 36) {
  digitalWrite(PIN_FAN, LOW);

  digitalWrite(LED_VERDE, LOW);
  digitalWrite(LED_BAJO, HIGH);
  digitalWrite(LED_ALTO, LOW);
  }
  else {
  // Dentro del rango
  digitalWrite(PIN_FAN, LOW);

  digitalWrite(LED_VERDE, HIGH);
  digitalWrite(LED_BAJO, LOW);
  digitalWrite(LED_ALTO, LOW);
  }

  //BALANZA
  float lectura = celda.get_units(3);

  peso_filtrado = 0.5 * peso_filtrado + 0.5 * lectura;

  if (abs(peso_filtrado) < 2.0) {
    peso_filtrado = 0;
  }

  Serial.print(" | Peso (g): ");
  Serial.println(peso_filtrado, 2);

  // OLED
  display.clearDisplay();

  //Temperatura T
  display.setTextSize(1);
  display.setCursor(0, 0);
  display.println("Temp");

  display.setTextSize(2);
  display.setCursor(15, 10);
  display.print(temp, 1);
  display.print(" C");

  // linea
  display.drawLine(0, 32, 128, 32, WHITE);

  // ---- PESO ----
  display.setTextSize(1);
  display.setCursor(0, 36);
  display.println("Peso");

  display.setTextSize(2);
  display.setCursor(15, 46);
  display.print(peso_filtrado, 1);
  display.print(" g");

  display.display();

  delay(150);
}

```
Mediante una pantalla OLED 128x64 se puede visualizar en directo la temperatura y el peso y como complemento esta el sistema de alerta consistente en un 3 leds. El led verde encendido significa que la temperatura está dentro del rango seguro, el led azul encendido significa que la temperatura esta por debajo de 36 °C y el led rojo encendido significa que sobrepaso el límite de los 37,5 °C.


<img width="303" height="404" alt="image" src="https://github.com/user-attachments/assets/f115dbb0-e5ad-4f26-be66-688699012884" />
Circuito


<img width="514" height="273" alt="image" src="https://github.com/user-attachments/assets/249c18f8-8665-4c30-811a-2a2e522b2f10" />
Temperatura baja y led azul encendido


<img width="660" height="342" alt="image" src="https://github.com/user-attachments/assets/86d40383-c536-4300-bec4-f9d6fcfe9fdd" />
Temperatura alta y led rojo encendido


<img width="389" height="249" alt="image" src="https://github.com/user-attachments/assets/124b8d7d-79f4-4a54-99be-aa504491819a" />
Temperatura en rango seguro y led verde encendido


# Resultado final:


<img width="1600" height="900" alt="image" src="https://github.com/user-attachments/assets/bd5e4753-89c9-4620-9f8c-4ad71f77c96f" />



<img width="960" height="1280" alt="image" src="https://github.com/user-attachments/assets/e0c8a391-9a8f-46f7-bbf7-94708382de85" />



<img width="1600" height="900" alt="image" src="https://github.com/user-attachments/assets/4f676d55-e08c-47bf-a4c5-b31aea33efbd" />



<img width="1600" height="900" alt="image" src="https://github.com/user-attachments/assets/c3cecc6d-a32c-4441-93c4-09f5973c98f2" />



<img width="494" height="311" alt="image" src="https://github.com/user-attachments/assets/f143a459-6db2-4ea1-b5e9-5ef2059c01d6" />


## 5) Costos y comparación

Se realizó el calculo del costo total del sistema desarrollado especificando también el costo
parcial de cada una de las partes, dando como resultado total yn gasto de 154850 Pesos Colombianos.

<img width="437" height="385" alt="image" src="https://github.com/user-attachments/assets/3e500250-b1a7-499f-aa1e-766c3d220ade" />

Al momento de comparar con los proveedores comerciales se puede ver que aunque directamente no publican los precios, ya que estos dependen de la ditribución, país y cotizante, igualmente tienen un rango que va desde los 18.000.000 hasta los 150.000.000 Pesos Colombianos, teniendo el precio más caro Dräger, con el modelo  Babyleo TN500 (150.000.000). Este modelo incluye todo lo de una incubadora normal, adicional tiene IncuWarmer, Modo canguro integrado, Fototerapia integrada, Conectividad UCIN y logicamente cuenta con todas las normativas de la más alta calidad.

Está claro que la diferencia entre el precio la incubadora de la presente practica y las incubadoras comerciales es gigante, del mismo modo conocemos las diferencias en calidad, de una incubadora neonatal se espera la más alta seguridad en sus mediciones, así como características "extra" que añaden beneficios al entorno de vida de una persona que requiera estos servicios de los cuales depende plenamente la vida de una neonato prematuro.

Dicho esto, no se espera que los precios sean parecidos a esta incubadora de fines académicos, pero si se puede tener en cuenta para cuestionarse que tan alta es la calidad, que tan grande y efectivo es dicho sistema como para que tengan dichos precios, aspi como analizar que diferencia unas líneas o marcas de otras, así como que tantas diferencias hay incluso entre las marcas comerciales como para que pueda haber diferencia de 132.000.000 pesos colombianos.

## 6)

PREGUNTAS PARA LA DISCUSIÓN
* Pregunta 1: ¿Qué otras variables (y por qué) además de las aquí
mencionadas son críticas en el monitoreo neonatal?

R/ Otras variables esenciales clave para una incubadora neonatal serían la humedad relativa debido a que se necesita controlar la perdida de agua por evaporación, también la concentración de oxigeno dada por FiO2 con el fin de evitar hipoxia o hiperoxia,  además del monitoreo de algunos signos vitales del bebé, como frecuencia cardiaca, frecuencia respiratoria, y saturación de oxígeno, por otra parte también variables que tienen que ver más con el dispositivo como las vibraciones pues estas pueden afectar el desarrollo cognitivo del bebé junto con ruido e iluminación. 

* Pregunta 2: ¿Qué haría falta para convertir el sistema desarrollado en una
incubadora neonatal real?

R/ Para convertir lo que tenemos en una incubadora real se necesita un isstema que lea y controle eficazmente las variables anteriormente mencionadas, y cumpla con las normas de bioseguridad dadas en las ISO.
* Pregunta 3: ¿Qué semejanzas hay entre una incubadora neonatal y una
servo-cuna?

R/Ambas se usan para el cuidado neonatal y tienen como función principal mantener la temperatura corporal del recién nacido. Las dos pueden trabajar con servo-control mediante sensor cutáneo, permiten monitoreo continuo, poseen alarmas de seguridad y se utilizan en unidades neonatales para bebés prematuros o de riesgo.

## 7) ANÁLISIS Y CONCLUSIONES

La incubadora dió resultados bastante positivos respecto a la temperatura, respondió correctamente a las instrucciones dadas, además de poder mantener el interior en la temperatura segura. Respecto al peso, este tenía un de error de aproximadamente del 3%. Este se revisó con una pesa de una 3000g como referencia, sin embargo es importante aclarar que la estabilidad de la base en donde esté la galga es completamente importante y ante ciertos movimientos podría desequilibrarse, incluso con ello consideramos un resultado positivo con enfoque a mejorar dicho defecto.

Reconocemos la importancia de controlar factores como la temperatura, identificando las variables vitales de las cuales un diagnóstico y la vida de un neonato dependen.

Es completamente factibles controlar variables como la temperatura y el peso, sin duda la correcta elección de insumos, espacios características y ambiente pueden hacer que mejoren los resultado, además que dichas variables son fácilmente comprobables fuera del sistema, por lo cual permite la comprobación cuantitativa y cualitativa de los datos para su calibración.

Por otro lado y como se mencionó anteriormente, en comparación con los fabricantes está bien decir que la incubadora cumple con su trabajo, sin embargo los fabricantes incluyen además controles de humedad, alarmas clíncias sonoras, monitoreo de signos vitales y muchas más características, pero esto también demuestra que los equipos, isntrumentación y dispositivos médicos pueden seguir avanzando y adquirir mayor capacidad de mejorar la calidad de vida de los usuarios.




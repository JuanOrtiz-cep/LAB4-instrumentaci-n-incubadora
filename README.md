 # LAB4-instrumentaci-n-incubadora


# README.md

## LAB 4 – Instrumentación Biomédica

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
Después de calibrarla usamos otro código para que muestre el peso en tiempo real con un filtro suavizado para que no tarde en reflejar el peso real, todo esto cuidando la estructura y evitando la inestabilidad del sistema, de esta manera la celda de presión queda calibrada y funcionando de manera correcta

<img width="370" height="160" alt="image" src="https://github.com/user-attachments/assets/a454797d-052b-4b0a-800f-4259608fa1d2" />

Para la parte del calentamiento se utilizó una bombilla de 53 watts, se realizó un orificio para su entrada exacta y que quedara en la parte alta de la incubadora, el bombillo incluye su conexión a tomacorriente.



<img width="960" height="1280" alt="image" src="https://github.com/user-attachments/assets/e4011d76-1f38-4811-b26d-5ef209d66e30" />

Foto bombilla

# 2)
Una vez se tiene como pesar y calentar, se implementan el sensor termocupla NTC 10k B3950, este nos permitiría saber a que temperatura se encuentra el interior de la incubadora, con lo anterior se incluye un sistema de enfriamiento consistente en un ventilador de 12V-100mA, este está instalado en un lateral centrado de la caja con la intención de que se encienda una vez alcanzados los 37 °C, con el fin de que nunca sobrepase el límite de los 37.5 °C, del mismo modo cuando llegué a bajar la temperatura, está programado para que el ventilador vuelva a apagarse, de tal forma que no sigue "enfirando" y así mantener el equilibrio. Esto se visualiza mejor en el código.

El ventilador es alimentado con baterías de 9v, también puede alimentarse con fuente mostrando mejores resultados.


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

<img width="514" height="273" alt="image" src="https://github.com/user-attachments/assets/249c18f8-8665-4c30-811a-2a2e522b2f10" />
Temperatura baja y led azul encendido

<img width="660" height="342" alt="image" src="https://github.com/user-attachments/assets/86d40383-c536-4300-bec4-f9d6fcfe9fdd" />
Temperatura alta y led rojo encendido

<img width="389" height="249" alt="image" src="https://github.com/user-attachments/assets/124b8d7d-79f4-4a54-99be-aa504491819a" />
Temperatura en rango seguro y led verde encendido

## 5) Costos y comparación


<img width="437" height="385" alt="image" src="https://github.com/user-attachments/assets/3e500250-b1a7-499f-aa1e-766c3d220ade" />

3. Calcule el costo total del sistema desarrollado especificando también el costo
parcial de cada una de las partes. Compare esto con soluciones comerciales
ofrecidas por proveedores como, por ejemplo, Dräguer, Instrumentalia S.A.S. y
LEEX Medical.



12.RESULTADOS DE LA PRÁCTICA:
Al finalizar esta práctica, el estudiante será capaz de:
1. Identificar las variables físicas que afectan directamente la supervivencia del
recién nacido.
2. Desarrollar un sistema capaz de imitar el modo de operación de una
incubadora neonatal.
3. Aplicar conocimientos de circuitos electrónicos y sistemas de control.
4. Comparar las prestaciones o capacidades del sistema desarrollado con las que
ofrecen sistemas comerciales.
5. Utilizar GitHub como herramienta de documentación y colaboración,
asegurando la visibilidad del trabajo individual y en grupo.
La presente práctica se evaluará bajo los siguientes criterios:


13. ANÁLISIS DE RESULTADOS
• Análisis 1: Evalúe la eficacia del sistema desarrollado para controlar la
temperatura de la cabina, así como también el error en el cálculo del peso,
empleando un patrón con peso conocido.
• Análisis 2: Compare el sistema desarrollado con los que ofrecen los
fabricantes sugeridos en términos de capacidades, limitaciones y precio.


14. CONCLUSIONES
Tras la realización de la práctica, el estudiante debe concluir incluyendo una breve
reflexión sobre la factibilidad de controlar con gran precisión variables como
temperatura y peso.
15. PREGUNTAS PARA LA DISCUSIÓN
• Pregunta 1: ¿Qué otras variables (y por qué) además de las aquí
mencionadas son críticas en el monitoreo neonatal?
• Pregunta 2: ¿Qué haría falta para convertir el sistema desarrollado en una
incubadora neonatal real?
• Pregunta 3: ¿Qué semejanzas hay entre una incubadora neonatal y una
servo-cuna?ados

* Fuente DC
* Ventilador pequeño
* Elemento calefactor resistivo
* Termistor
* LM317 / LM337
* Puente rectificador
* Capacitores 2200 µF
* Resistencias varias
* LEDs (verde y rojo)
* Protoboard
* Cables UTP
* Multímetro
* Osciloscopio
* Pantalla LCD o displays



## 6. Resultados Esperados

### 6.1 Control de Temperatura

El sistema logró mantener la temperatura dentro del intervalo requerido con oscilaciones pequeñas alrededor del punto de ajuste.

### 6.2 Sistema de Peso

La lectura simulada mostró respuesta proporcional al peso aplicado.

### 6.3 Señalización Visual

Los LEDs respondieron correctamente según la condición térmica interna.

---

## 7. Análisis de Resultados

El prototipo evidenció que el control térmico es una de las funciones más críticas en incubadoras neonatales. Pequeñas desviaciones de temperatura pueden comprometer la estabilidad fisiológica del neonato.

El uso de sensores térmicos junto con realimentación permitió automatizar el sistema y mantener condiciones cercanas a las requeridas clínicamente.

La medición de peso complementa el monitoreo integral, siendo indispensable en unidades neonatales.

Aunque el modelo construido es académico, reproduce principios fundamentales presentes en incubadoras comerciales modernas.

---

## 8. Comparación con Sistemas Comerciales

| Característica     | Prototipo | Comercial |
| ------------------ | --------- | --------- |
| Control térmico    | Sí        | Sí        |
| Medición peso      | Sí        | Sí        |
| Humedad controlada | No        | Sí        |
| Alarmas clínicas   | Básicas   | Avanzadas |
| Monitoreo vital    | No        | Sí        |
| Costo              | Bajo      | Alto      |

---

## 9. Aplicaciones Biomédicas

* Entrenamiento académico.
* Enseñanza de sistemas de control médico.
* Prototipado de bajo costo.
* Investigación en neonatología tecnológica.

---

## 10. Limitaciones

* No apta para uso clínico real.
* Sin control de humedad.
* Sin monitoreo cardíaco o respiratorio.
* Escalamiento simplificado.

---

## 11. Conclusiones

* Se diseñó exitosamente una incubadora neonatal a escala funcional.
* El sistema permitió regular temperatura mediante lazo cerrado.
* La medición de peso complementó el monitoreo básico neonatal.
* El laboratorio integró conocimientos de electrónica, control e instrumentación biomédica.
* Se comprendió la alta complejidad y responsabilidad asociada al diseño de equipos médicos neonatales.

---

## 12. Referencias

[1] C. G. K. Tran et al., “Designing a low-cost multifunctional infant incubator,” *J. Lab. Autom.*, 2014.

[2] L. Restrepo-Pérez et al., “Prototipo de incubadora neonatal,” *Revista Ingeniería Biomédica*, 2007.

[3] European Foundation for the Care of Newborn Infants, *Temperature management in newborn infants*, 2018.

[4] R. B. Knobel-Dail, “Role of effective thermoregulation in premature neonates,” *Research and Reports in Neonatology*, 2014.

[5] 

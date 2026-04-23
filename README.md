 # LAB4-instrumentaci-n-incubadora


# README.md

## LAB 4 – Instrumentación Biomédica

# Diseño y Construcción de una Incubadora Neonatal a Escala

Universidad Militar Nueva Granada
Ingeniería Biomédica

---

## 1. Introducción

En este laboratorio se diseñó y construyó un prototipo funcional de incubadora neonatal a escala, orientado al control de variables críticas para la supervivencia del recién nacido, principalmente temperatura y peso. El sistema fue desarrollado mediante principios de electrónica analógica, sensores biomédicos y sistemas de control en lazo cerrado.

### Contexto Teórico

Una incubadora neonatal es un dispositivo médico diseñado para proporcionar al neonato un ambiente controlado similar al vientre materno, garantizando condiciones térmicas adecuadas, protección frente al entorno externo y monitoreo constante de variables fisiológicas [1], [2].

Uno de los parámetros más importantes es la temperatura corporal, la cual debe mantenerse cercana a **37 °C**, especialmente en neonatos prematuros, quienes presentan menor capacidad de termorregulación debido a inmadurez fisiológica y baja cantidad de tejido adiposo [3], [4].

Para lograrlo, las incubadoras emplean sistemas de calefacción por convección forzada, sensores térmicos y controladores automáticos que ajustan el calentamiento según la temperatura interna.

Además del control térmico, también es importante el monitoreo del peso neonatal, ya que permite evaluar crecimiento, hidratación y evolución clínica.

La presente práctica consistió en diseñar una incubadora neonatal a escala capaz de regular temperatura entre **36 °C y 37.5 °C**, medir peso simulado y visualizar el estado operativo mediante indicadores luminosos.

---

## 2. Objetivos

### 2.1 Objetivo General

Desarrollar un sistema electromédico a escala que emule el funcionamiento básico de una incubadora neonatal mediante control automático de temperatura y medición de peso.

### 2.2 Objetivos Específicos

* Identificar las partes principales de una incubadora neonatal real.
* Diseñar un sistema de control térmico en lazo cerrado.
* Implementar una medición electrónica de peso.
* Construir una estructura física funcional a escala.
* Comparar el sistema desarrollado con incubadoras comerciales reales.

---

## 3. Marco Teórico

### 3.1 Importancia de la Termorregulación Neonatal

Los recién nacidos prematuros presentan alta susceptibilidad a:

* Hipotermia
* Hipertermia
* Deshidratación
* Estrés metabólico
* Inestabilidad cardiorrespiratoria

Por ello, la incubadora debe mantener temperatura estable dentro de rangos clínicamente seguros.

### 3.2 Sistema de Control en Lazo Cerrado

Un sistema de lazo cerrado compara la temperatura medida con una referencia deseada y corrige automáticamente el error.

e(t)=T_{ref}-T(t)

Donde:

* (T_{ref}): temperatura deseada
* (T(t)): temperatura real interna

### 3.3 Medición de Peso

El peso neonatal permite detectar alteraciones nutricionales, retención de líquidos o pérdida excesiva de masa corporal. Puede medirse mediante sensores resistivos o galgas extensiométricas.

---

## 4. Diseño del Sistema

## 4.1 Variables Controladas

| Variable       | Rango Deseado             |
| -------------- | ------------------------- |
| Temperatura    | 36 °C – 37.5 °C           |
| Peso           | Visualización electrónica |
| Estado térmico | LEDs                      |

---

## 4.2 Componentes Utilizados

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

---

## 4.3 Indicadores del Sistema

* **LED Verde:** temperatura dentro del rango.
* **LED Rojo Bajo:** temperatura menor a 36 °C.
* **LED Rojo Alto:** temperatura mayor a 37.5 °C.

---

## 5. Procedimiento Experimental

### Parte A – Diseño

1. Investigación bibliográfica sobre incubadoras reales.
2. Simulación del circuito de control térmico.
3. Simulación del sistema de medición de peso.

### Parte B – Construcción

1. Ensamble de la estructura física transparente.
2. Instalación del ventilador y calefactor.
3. Conexión del sensor térmico.
4. Implementación de LEDs indicadores.
5. Implementación del sistema de peso.

### Parte C – Validación

1. Medición de estabilidad térmica.
2. Verificación de respuesta ante cambios externos.
3. Comparación con valores patrón de peso.

---

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

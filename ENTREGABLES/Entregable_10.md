# AVANCE PROTOTIPADO ELECTRÓNICO
## Hardware Electrónico

<img src="/multimedia/hardware_electronico.jpg" alt="Gráfico de resultados" width="700">

## Software 

Evidencias del último laboratorio:

### Configuración del Sensor EMG
  
<img src="/multimedia/configuracion_sensor_emg.jpg" alt="Gráfico de resultados" width="700">

### Código correspondiente

#include <Servo.h>    // Using the Servo library

Servo elbowJoint;     // Naming our servo ‘elbowJoint’

int EMGsig;           // Store the EMG signal value

int servoPosition;    // The position (angle) value for the servo

int threshold = 300;  // Move the servo when EMG signal is above this threshold. Remember it ranges 0–1023.

void setup() {

 Serial.begin(9600); // Starting the communication with the computer
 
 elbowJoint.attach(9); // Tell the servo it is plugged into pin 9
 
}

void loop() {

 EMGsig = analogRead(A0); // Read the analog values of the rectified+integrated EMG signal (0–1023)
 
if (EMGsig < threshold){     // If EMG signal is below the threshold

    servoPosition = 20;       // Servo will remain at 20 degrees.
    
  } else{            // If the EMG signal is above the threshold,
  
   servoPosition=map(EMGsig,threshold,1023,20,160); 
   
  // The servo angle will be mapped with the EMG signal, 
  
  // changing the range of 300(our threshold)-1023 into the range of 20-160 degrees.
  
  // 20 and 160 can be switched depending on which direction of rotation you want.
  
}

 elbowJoint.write(servoPosition); 
 
  // Move the servo to the ‘servoPosition’ degree
  
 Serial.print(servoPosition);Serial.print(" degrees, with EMG: ");Serial.println(EMGsig); 
 
 // Display the servo and EMG values.
 
 delay(1000); 
 
  // 1 second (1000ms) delay to not cause it to move as frantically. 

# MODELADO 3D 

## DEDO PULGAR

<img src="/multimedia/dedo_pulgar.jpg" alt="Gráfico de resultados" width="700">

## DEDO INDICE

<img src="/multimedia/dedo_indice.jpg" alt="Gráfico de resultados" width="700">

## DEDO MEDIO

<img src="/multimedia/dedo_medio.jpg" alt="Gráfico de resultados" width="700">

## DEDO ANULAR

<img src="/multimedia/dedo_anular.jpg" alt="Gráfico de resultados" width="700">


# Plan de Usabilidad

## ¿Qué es?

Este plan detalla los aspectos clave para el diseño y la evaluación de un prototipo de **mano biomecánica controlada por señales electromiográficas (EMG)**. El objetivo es asegurar que el dispositivo sea usable, eficaz y seguro para las personas que han sufrido amputaciones o malformaciones en la mano.



## ¿Qué hacer?

El plan se divide en cuatro secciones principales: **Contexto de Uso**, **Perfil del Usuario**, **Análisis de Tareas** y **Criterios de Éxito**. Cada sección aborda preguntas específicas y define el tipo de evidencia necesaria para guiar el desarrollo del prototipo.



## ¿Qué evidencia deben incluir?

La evidencia incluirá desde **modelos 3D y bocetos** hasta **tablas con métricas de usabilidad y datos de casos**.



## 1. Contexto de Uso

### Describe cómo, dónde y quién usará el dispositivo.

Este dispositivo, una **mano biomecánica controlada por señales EMG**, está diseñado para ser utilizado principalmente por **pacientes con muñones o malformaciones en los dedos de la mano** que buscan recuperar la funcionalidad y la independencia en sus actividades diarias.

* **Quién usará el dispositivo:** El usuario principal será el **paciente**. También podrían interactuar con él **cuidadores** (para asistencia en la colocación o mantenimiento) y **profesionales de la salud** (durante terapias o ajustes).
* **Cómo se usará:** La mano biomecánica se controlará mediante las **señales mioeléctricas** generadas por los músculos residuales del antebrazo del usuario, como se menciona en las fuentes [1] y [2]. El dispositivo se ajustará al muñón y permitirá al usuario realizar movimientos de prensión y manipulación básicos.
* **Dónde se usará:** El uso principal será en el **hogar del paciente**, permitiéndole realizar actividades cotidianas. También se espera su uso en **entornos clínicos** durante sesiones de rehabilitación o para realizar ajustes y mantenimiento.
* **Frecuencia de uso:** El uso será **diario**, adaptándose a las necesidades del usuario para las actividades de la vida diaria, y con una frecuencia que dependerá del nivel de adaptación y comodidad.

### Evidencia a incluir:

* **Modelado 3D o boceto** que muestre la mano biomecánica colocada en un usuario, interactuando con objetos comunes en un entorno doméstico (ej. sosteniendo un vaso, manipulando un objeto).
* **Diagramas de flujo** que ilustren el proceso de colocación y retiro del dispositivo, y cómo se integraría en la rutina diaria del usuario.



## 2. Perfil del Usuario

### Características físicas, cognitivas y emocionales del usuario.

El perfil del usuario es crucial para adaptar el diseño del prototipo a sus necesidades específicas.

* **Características físicas:**
    * **Limitaciones motoras:** El usuario presenta la ausencia parcial de los dedos. La capacidad de generar señales EMG con los músculos residuales del antebrazo es fundamental [1], [2].
    * **Dimensiones del muñón:** Variabilidad en el tamaño y la forma del muñón, lo que requiere un diseño adaptable y personalizable del encaje.
    * **Sensibilidad:** Posible sensibilidad en la zona del muñón, lo que exige materiales biocompatibles y un ajuste cómodo para evitar úlceras o irritaciones.
* **Características cognitivas:**
    * **Capacidad de aprendizaje:** Disposición para aprender a controlar la mano a través de las señales EMG y adaptarse a nuevos patrones de movimiento.
    * **Atención:** La capacidad de mantener la concentración necesaria para el control fino del dispositivo.
* **Características emocionales:**
    * **Frustración:** Posible frustración inicial durante el proceso de adaptación y aprendizaje. El diseño debe minimizar esta frustración y promover la perseverancia.
    * **Confianza:** El dispositivo debe inspirar confianza en el usuario para que se sienta seguro al realizar tareas.
    * **Percepción de la imagen corporal:** La prótesis debe contribuir a una imagen corporal positiva y no generar sentimientos de estigmatización.

### Evidencia a incluir:

* **Datos del caso seleccionado:** Para un diseño específico, se deben incluir datos antropométricos del muñón, un breve historial médico (tipo de amputación, tiempo desde la amputación) y, si es posible, una evaluación cognitiva básica para entender las habilidades de aprendizaje del usuario.
* **Entrevistas o cuestionarios a usuarios potenciales** (o cuidadores) para recabar información sobre sus expectativas, desafíos actuales y preferencias de uso.



## 3. Análisis de Tareas

### Tareas necesarias para usar el prototipo correctamente.

Es fundamental identificar y analizar las tareas que el usuario realizará con la mano biomecánica para asegurar su correcto funcionamiento y minimizar riesgos.

* **Listado de tareas:**
    * **Colocación y ajuste del encaje:** El usuario debe poder colocarse y ajustarse el encaje de la prótesis de forma segura y cómoda.
    * **Activación y desactivación del dispositivo:** Encendido y apagado de la mano protésica.
    * **Control básico de movimientos:** Realizar movimientos de apertura y cierre de la mano mediante señales EMG [1], [2].
    * **Manipulación de objetos cotidianos:**
        * Sujetar un vaso o botella.
        * Coger y soltar objetos pequeños (ej. lápiz, moneda).
        * Abrir una puerta (agarrar pomo).
        * Realizar tareas de higiene personal (ej. sostener un cepillo de dientes).
    * **Ajuste de la fuerza de prensión:** Si el prototipo lo permite, controlar la intensidad de la fuerza para evitar aplastar objetos o que se caigan.
    * **Mantenimiento y carga:** Limpiar el dispositivo y cargar la batería.
* **Identificación de tareas críticas:** Son aquellas que, si se realizan incorrectamente, pueden causar daño al usuario o al dispositivo.
    * **Ajuste inadecuado del encaje:** Puede causar irritación, presión excesiva o úlceras en el muñón.
    * **Control deficiente de la fuerza de prensión:** Puede llevar a aplastar objetos (daño al objeto) o, en casos extremos, causar lesiones al propio usuario (si el objeto es frágil o peligroso).
    * **Mal uso del dispositivo en entornos peligrosos:** Ej. intentar manipular objetos calientes o afilados sin la debida precaución, causando quemaduras o cortes.
    * **Carga incorrecta o uso de cargadores no compatibles:** Riesgo de daño a la batería o al circuito, e incluso incendio.

### Evidencia a incluir:

* **Tabla de tareas y riesgos:** Una tabla detallada que liste cada tarea, describa los pasos clave, identifique los posibles errores y especifique el riesgo asociado (bajo, medio, alto).
* **Justificación de por qué son críticas:** Para cada tarea crítica, una breve explicación de las posibles consecuencias de su realización incorrecta.
* **Secuencias de video o fotografías** que muestren a un usuario realizando estas tareas con un prototipo o una mano simulada, destacando los puntos de interacción y posibles dificultades.



## 4. Criterios de Éxito (Requisitos de Usabilidad)

### Son los indicadores concretos para saber si el dispositivo es usable.

Para determinar si la mano biomecánica es exitosa en términos de usabilidad, se establecerán métricas claras y cuantificables.

* **Eficacia:** ¿La tarea se completó?
    * **Métrica:** Porcentaje de tareas completadas con éxito.
    * **Objetivo:** Por ejemplo, "El 90% de las tareas básicas (agarrar y soltar objetos) deben completarse con éxito en las primeras 5 sesiones de uso".
* **Eficiencia:** ¿En cuánto tiempo?
    * **Métrica:** Tiempo promedio para completar una tarea específica.
    * **Objetivo:** Por ejemplo, "El tiempo para colocar y ajustar la prótesis debe ser inferior a 2 minutos para el usuario experimentado". O "El tiempo promedio para agarrar un objeto de tamaño medio debe ser de 5 segundos o menos".
* **Satisfacción:** ¿Cómo lo evaluó el usuario?
    * **Métrica:** Puntuación en escalas de satisfacción del usuario, como el **System Usability Scale (SUS)**.
    * **Objetivo:** Por ejemplo, "Puntuación SUS superior a 70 (considerado "buena" usabilidad)".
    * **Métrica:** Retroalimentación cualitativa del usuario (comentarios sobre comodidad, facilidad de uso, estética).
    * **Objetivo:** "Comentarios predominantemente positivos sobre la comodidad del encaje y la facilidad de control".
* **Seguridad:** ¿Hubo errores?
    * **Métrica:** Número de errores críticos (aquellos que causan daño o imposibilitan el uso) durante las pruebas.
    * **Objetivo:** "0 lesiones o daños al usuario durante el período de prueba".
    * **Métrica:** Número de incidentes de mal funcionamiento del dispositivo o caídas de objetos.
    * **Objetivo:** "Menos de 3 caídas de objetos por cada 100 intentos de agarre".

### Evidencia a incluir:

* **Tabla con métricas objetivo:** Una tabla donde se definan claramente cada métrica, su objetivo numérico y cómo se medirá.
* **Protocolos de prueba:** Descripción detallada de cómo se llevarán a cabo las pruebas de usabilidad para recopilar los datos (ej. tareas específicas a realizar, duración de las sesiones, instrumentos de medición).
* **Resultados preliminares de pruebas (si ya se tienen):** Datos cuantitativos y cualitativos recopilados durante las primeras iteraciones del prototipo, comparándolos con los objetivos establecidos.





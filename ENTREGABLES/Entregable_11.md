# AVANCE DE FABRICACIÓN DIGITAL
## Impresión 3D de los dedos pulgar, indice, medio y anular

<img src="/multimedia/dedo_imagen.jpg" alt="Gráfico de resultados" width="700">

<img src="/multimedia/dedo_imagen1.jpg" alt="Gráfico de resultados" width="700">

<img src="/multimedia/dedo_imagen2.jpg" alt="Gráfico de resultados" width="700">

# PROTOTIPADO ELECTRÓNICO

## ¨rototipado electrónico funcional

<img src="/multimedia/electronica1.jpg" alt="Gráfico de resultados" width="700">

<img src="/multimedia/electronica2.jpg" alt="Gráfico de resultados" width="700">

## Código usado

#include <ESP32Servo.h>

// Crear objetos servo

Servo servo1;

Servo servo2;

// Pines

const int emgPin = 34;          // Entrada analógica (solo entrada)

const int servo1Pin = 18;

const int servo2Pin = 19;

// Rango de señal EMG (ajustar después de pruebas reales)

int emgMin = 250;               // Valor en reposo (ajusta esto)

int emgMax = 1200;              // Contracción máxima (ajusta esto)


// Ángulos del servo

const int servoMin = 0;

const int servoMax = 90;

// Suavizado (filtro exponencial)

float alpha = 0.1;              // Cuanto menor, más suave el movimiento

float filteredEMG = 0;

void setup() {

  Serial.begin(115200);
  
  servo1.attach(servo1Pin);
  
  servo2.attach(servo2Pin);
  
  servo1.write(servoMin);
  
  servo2.write(servoMin);
  
}

void loop() {

  int rawEMG = analogRead(emgPin);
  
  Serial.print("EMG crudo: ");
  
  Serial.println(rawEMG);

// Aplicar filtro exponencial (suavizado)

  filteredEMG = alpha * rawEMG + (1 - alpha) * filteredEMG;

  // Limitar señal dentro del rango útil
  
  filteredEMG = constrain(filteredEMG, emgMin, emgMax);

  // Mapear a ángulo proporcional
  
  float angle = mapFloat(filteredEMG, emgMin, emgMax, servoMin, servoMax);

  // Limitar el ángulo final por seguridad
  
  angle = constrain(angle, servoMin, servoMax);

  // Enviar al servo
  
  servo1.write(angle);
  
  servo2.write(angle);

  delay(30);
}

// Función para mapear decimales
float mapFloat(float x, float in_min, float in_max, float out_min, float out_max) {
  return (x - in_min) * (out_max - out_min) / (in_max - in_min) + out_min;
}


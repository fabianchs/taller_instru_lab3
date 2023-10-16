# Programacion
## Arduino
A continuacion se muestra el codigo en arduino usado para la implementacion:

```cpp
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27, 16, 2);  // Establece la dirección I2C del adaptador y el tamaño del LCD (16x2).

int pin1 = 2;
int pin2 = 3;
int pin3 = 4;
void setup() {
  lcd.init();                      // Inicializa el LCD.
  lcd.backlight();                 // Activa la retroiluminación del LCD.
  Serial.begin(9600);
  pinMode(pin1, OUTPUT);
  pinMode(pin2, OUTPUT);
  pinMode(pin3, OUTPUT);
}

void loop() {
  //Control de la ganancia programable
  if (Serial.available() > 0) {
    int val = Serial.parseInt();  // Lee un número de la comunicación serie
    if (val == 1) {
      digitalWrite(pin1, LOW);
      digitalWrite(pin2, LOW);
      digitalWrite(pin3, LOW);
    }if (val == 2) {
      digitalWrite(pin1, LOW);
      digitalWrite(pin2, LOW);
      digitalWrite(pin3, HIGH);
    }if (val == 3) {
      digitalWrite(pin1, LOW);
      digitalWrite(pin2, HIGH);
      digitalWrite(pin3, LOW);
    }if (val == 4) {
      digitalWrite(pin1, LOW);
      digitalWrite(pin2, HIGH);
      digitalWrite(pin3, HIGH);
    }if (val == 5) {
      digitalWrite(pin1, HIGH);
      digitalWrite(pin2, LOW);
      digitalWrite(pin3, LOW);
    }if (val == 6) {
      digitalWrite(pin1, HIGH);
      digitalWrite(pin2, LOW);
      digitalWrite(pin3, HIGH);
    }
  }

  // Leer el valor de tensión en el pin analógico A1
  int valorAnalogicoA1 = analogRead(A1);

  // Convertir los valores leídos a voltajes (0-1023 a 0-5V en este caso)
  float voltajeA1 = (valorAnalogicoA1)*0.0926083107;

  //Tiempo
  unsigned long tiempoActualMillis = millis(); // Obtener el tiempo actual en milisegundos
  unsigned long tiempoActualSegundos = tiempoActualMillis / 1000; // Convertir a segundos
 
  String datos = String(tiempoActualSegundos) + "," + String(voltajeA1);
  Serial.println(datos);
  

  lcd.setCursor(0,0);
  lcd.print("Temp 1: ");
  lcd.print(voltajeA1,2);
  lcd.print(" C");


  delay(1000);
}

```
## Python

El archivo `gui.py` crea la interfaz necesaria para comunicar software y hardware via USB.

Descripcion de `conexion_sqlite3.py`

Descripcion de `send_data.py`


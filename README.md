# Practica-No.4
## Introduccion
Descripción
 Utilizamos un simulador llamado WOKWI, Dentro de este utilizaremos una tarjeta  Esp32 y  un sensor (Ultrasonico) para medir la distancia; esta misma se vera reflejada dentro del LCD 
-.Para realizar esta practica necesitas lo siguiente:
 ° WOKWI
 °Tarjeta ESP32
 °Sensor HC-SR04
 °LCD16x2(I2C)
 
- "NOTA" :Para poder usar este repositorio necesitas entrar a la plataforma WOKWI.
### Instrucciones de preparación de entorno
- 1.Abrir la terminal de programación y colocar el siguente codigo de programación:

#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 15;   //Pin digital 3 para el Echo del sensor
LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);
void setup() {
  Serial.begin(9600);//iniciailzamos la comunicación
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0
  lcd.init();
  lcd.backlight();
}
void loop()
{
  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros
  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);
  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo a una distancia en cm

  Serial.print("Distancia: ");
  Serial.print(d);      //Enviamos serialmente el valor de la distancia
  Serial.print("cm");
  Serial.println();
  delay(1000);          //Hacemos una pausa de 100ms
 
  lcd.setCursor(0, 0);
  lcd.print("Distancia: " +String(d) + "cm  ");
  lcd.print("Wokwi Online IoT");
  delay(1000);
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("ING.Wilber ");
  lcd.setCursor(0, 1);
  lcd.print("Industrial");
  delay(2000);
  lcd.clear();
}

Posteriormente :

1.Instalar la libreria DHT sensor library for ESPx y LiquidCrystal I2C como se muestra en la siguente imagen.
![](https://github.com/AmaiCisneros/Practica-4/blob/main/10.png)

2. Hacer la conexión entre los componentes:
![](https://github.com/AmaiCisneros/Practica-4/blob/main/111111.png)

Inicia el simulador para asi mismo poder observar el valor que indicamos en la pantalla 
Resultados
![](https://github.com/AmaiCisneros/Practica-4/blob/main/111111.png)



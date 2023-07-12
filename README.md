### 📄Documentación del recuperatorio del segundo parcial para la materia Sistemas de procesamiento de datos - UTN Tecnicatura Superior en Programación.

### Nombre: Torres Matías Daniel

### **Sistema de Procesamiento de Datos (SPD)**

![Arduino](https://github.com/matiasdtorres/RECU-2-SPD/blob/fadcf87b728d5b2968905f6cd988bb7e0d3b8ed4/ArduinoTinkercad.jpg)

### Setteo de temperaturas funcional

![Setteo de temperaturas](https://github.com/matiasdtorres/RECU-2-SPD/blob/fadcf87b728d5b2968905f6cd988bb7e0d3b8ed4/imagen_2023-05-18_121209060.png)
### 🦴Modelo esquematico del Setteo de temperaturas

![Setteo de temperaturas](https://github.com/matiasdtorres/RECU-2-SPD/blob/fadcf87b728d5b2968905f6cd988bb7e0d3b8ed4/RECU-2DO%20PARCIAL.png)

## 📄Consigna Setteo de temperaturas:
Se nos pide restar de la temperatura actual con cualquier numero que eligamos. El
objetivo es que pueda recibir temperaturas del [TEMP36] y que se muestre en la primera fila
display lcd, y en la segunda fila un numero del 0-99 que recibe del keypad. y el resultado
de la resta se debe mostrar en el monitor en serie.

### 🚀Codigo del proyecto
``` C++
#include <LiquidCrystal.h>
#include <Keypad.h>

#define sensor A1

const byte FILAS = 4;
const byte COLUMNAS = 4;
char keys[FILAS][COLUMNAS] = {
  {'1','2','3','A'},
  {'4','5','6','B'},
  {'7','8','9','C'},
  {'*','0','#','D'}
};

byte pinesFilas[FILAS] = {11, 10, 9, 8};
byte pinesColumnas[COLUMNAS] = {7, 6, 5, 4};
Keypad teclado = Keypad(makeKeymap(keys), pinesFilas, pinesColumnas, FILAS, COLUMNAS);

LiquidCrystal lcd(3, A0, A2, A3, A4, A5);

int medicion;
String ingreso = "";

void setup()
{
  Serial.begin(9600);
  
  lcd.begin(16, 2);
  
  pinMode(sensor, INPUT);
}

void loop()
{
  medicion = analogRead(sensor);
  medicion = map(medicion, 20, 358, -40, 125);
  
  char TECLA = teclado.getKey();

  if (TECLA)
  {
    
    if (isdigit(TECLA) && ingreso.length() < 2) {
      ingreso += TECLA;
    }
    
    else if (TECLA == 'A')
    {
      if (ingreso.length() > 0)
      {
        int setTemp = ingreso.toInt();
        Serial.println(medicion - setTemp);
      }
    }
    
    else if (TECLA == 'B')
    {
      ingreso = "";
      lcd.setCursor(0, 1);
      lcd.clear();
    }
    
  }
  
  display(medicion, ingreso);
  delay(25);
}

void display(int temp, String set)
{
  lcd.setCursor(0, 0);
  lcd.print("TEMP:");
  lcd.setCursor(5, 0);
  lcd.print(temp);
  
  lcd.setCursor(0, 1);
  lcd.print("SET:");
  lcd.print(set);
}
```
### 🤖Funcionando
![Setteo de temperaturas](https://github.com/matiasdtorres/RECU-2-SPD/blob/fadcf87b728d5b2968905f6cd988bb7e0d3b8ed4/2023-07-11-20-32-46.gif)

### 🧠Explicacion

``` C++
#include <LiquidCrystal.h>
#include <Keypad.h>

#define sensor A1

const byte FILAS = 4;
const byte COLUMNAS = 4;
char keys[FILAS][COLUMNAS] = {
  {'1','2','3','A'},
  {'4','5','6','B'},
  {'7','8','9','C'},
  {'*','0','#','D'}
};

byte pinesFilas[FILAS] = {11, 10, 9, 8};
byte pinesColumnas[COLUMNAS] = {7, 6, 5, 4};
Keypad teclado = Keypad(makeKeymap(keys), pinesFilas, pinesColumnas, FILAS, COLUMNAS);

LiquidCrystal lcd(3, A0, A2, A3, A4, A5);

int medicion;
String ingreso = "";

void setup()
{
  Serial.begin(9600);
  
  lcd.begin(16, 2);
  
  pinMode(sensor, INPUT);
}

void loop()
{
  medicion = analogRead(sensor);
  medicion = map(medicion, 20, 358, -40, 125);
  
  char TECLA = teclado.getKey();

  if (TECLA)
  {
    
    if (isdigit(TECLA) && ingreso.length() < 2) {
      ingreso += TECLA;
    }
    
    else if (TECLA == 'A')
    {
      if (ingreso.length() > 0)
      {
        int setTemp = ingreso.toInt();
        Serial.println(medicion - setTemp);
      }
    }
    
    else if (TECLA == 'B')
    {
      ingreso = "";
      lcd.setCursor(0, 1);
      lcd.clear();
    }
    
  }
  
  display(medicion, ingreso);
  delay(25);
}
```
hola

``` C++
// FUNCIONES
void display(int temp, String set)
{
  lcd.setCursor(0, 0);
  lcd.print("TEMP:");
  lcd.setCursor(5, 0);
  lcd.print(temp);
  
  lcd.setCursor(0, 1);
  lcd.print("SET:");
  lcd.print(set);
}

// FIN FUNCIONES
```

La función **display()** se utiliza para mostrar las variables temp y set en el display lcd.

``` C++
## <img src="tinkercad.png" alt="Tinkercad" height="32px"> Link al proyecto

- [Proyecto](https://www.tinkercad.com/things/0G7hVhANbad)

### 📄Parcial:

[Enunciado](https://github.com/matiasdtorres/RECU-2-SPD/blob/fadcf87b728d5b2968905f6cd988bb7e0d3b8ed4/Enunciado.pdf)

### 📄Fuentes

- [Youtube](https://www.youtube.com)
- [arduino](https://www.arduino.cc/reference/en/language/variables/data-types/string/functions/toint/)
- [Utn](http://www.sistemas-utnfra.com.ar/#/home)

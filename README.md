# Esp32-Pwm
Genera una señal cuadrada, modulacion por ancho de pulso

* 0 a 15 canales disponibles en total 16 canales
* Frecuencia minima y maxima 1 minima y maxima 40.000 khz
* Resolucion se pueden elegir de 1-16
* La resolucion 8 signfica 8 bit que es de 0-255
* Todo los puertos pueden funcionar como salidas pwm excepto los pines d35(gpio35),d34(gpio34),vn(gpio39),vp(gpio36) que sirven solamente como entradas

```c++
int frecuencia = 5000; //1-40.000 khz
int canal = 0; //0-15 canales
int resolucion = 8; //1-16 bits
int ledPin = 23; //pin donde esta el led

void setup()
{
  //Configuracion inicial
  ledcSetup(canal, frecuencia, resolucion);

  //Se selecciona el pin y el canal
  ledcAttachPin(ledPin, canal);
}

void loop()
{
  for (int ciclo = 0; ciclo <= 255; ciclo++)
  {
    ledcWrite(canal, ciclo);
    delay(10);
  }
}
```
### Para agregar otro led simplemente se le agrega 
* Se agrega esta linea ```ledcAttachPin(ledPin2, canal); ```

```c++
int frecuencia = 5000; //1-40.000 khz
int canal = 0; //0-15 canales
int resolucion = 8; //1-16 bits
int ledPin = 23; //pin donde esta el led
int ledPin2 = 22;

void setup()
{
  //Configuracion inicial
  ledcSetup(canal, frecuencia, resolucion);

  //Se selecciona el pin y el canal
  ledcAttachPin(ledPin, canal);
  ledcAttachPin(ledPin2, canal);
}

void loop()
{
  for (int ciclo = 0; ciclo <= 255; ciclo++)
  {
    ledcWrite(canal, ciclo);
    delay(10);
  }
}
```
### El problema de usar el mismo canal, es que siempre todos los led de todo el canal van a tener la misma señal pwm la solucion utilizar otro canal
```c++
int frecuencia = 5000; //1-40.000 khz
int canal = 0; //0-15 canales
int canal2 = 1;
int resolucion = 8; //1-16 bits
int ledPin = 23; //pin donde esta el led
int ledPin2 = 22;

void setup()
{
  //Configuracion inicial
  ledcSetup(canal, frecuencia, resolucion);
  //ledcSetup(canal2, frecuencia, resolucion); //No se deben declarar dos veces es un error solamente se puede hacer una declaracion

  //Se selecciona el pin y el canal
  ledcAttachPin(ledPin, canal);
  ledcAttachPin(ledPin2, canal2);
}

void loop()
{
  //Pin del canal 2 encendido siempre
  ledcWrite(canal2, 255); 
  
  for (int ciclo = 0; ciclo <= 255; ciclo++)
  {
    ledcWrite(canal, ciclo);
    delay(10);
  }
}
```

# Esp32-Pwm
Genera una señal cuadrada, modulacion por ancho de pulso

* Informacion no verificada
* Tiene 16 puertos para crear 16 señales pwm pero la verdad que nose se tendria que verificar
* No son 16 puertos son 16 canales y cada puerto de salida se puede utilizar para crear una señal pwm
* 0 a 15 canales disponibles en total 16 canales
* Frecuencia minima y maxima 1 minima y maxima 40.000 khz
* Resolucion se pueden elegir de 1-16
* La resolucion 8 signfica 8 bit que es de 0-255
* Todo los puertos pueden funcionar como salidas pwm excepto los pines d35(gpio35),d34(gpio34),vn(gpio39),vp(gpio36) que sirven solamente como entradas

```c++
// setting PWM properties
const int freq = 5000;
const int ledChannel = 0;
const int resolution = 8;
 
void setup(){
  // configure LED PWM functionalitites
  ledcSetup(ledChannel, freq, resolution);
  
  // attach the channel to the GPIO to be controlled
  ledcAttachPin(ledPin, ledChannel);
  //ledcAttachPin(ledPin2, ledChannel);
  //ledcAttachPin(ledPin3, ledChannel);
}
 
void loop(){
  // increase the LED brightness
  for(int dutyCycle = 0; dutyCycle <= 255; dutyCycle++){   
    // changing the LED brightness with PWM
    ledcWrite(ledChannel, dutyCycle);
    delay(15);
  }
  }
```

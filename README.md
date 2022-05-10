# Esp32-Pwm
Genera una señal cuadrada, modulacion por ancho de pulso

* Informacion no verificada
* Tiene 16 puertos para crear 16 señales pwm pero la verdad que nose se tendria que verificar
* No son 16 puertos son 16 canales y cada puerto de salida se puede utilizar para crear una señal pwm

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

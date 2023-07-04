# Segundo parcial de SPD
![imagen de arduino y tinkercad](tinkercad-arduino.png "arduino en tinkercad")
<!-- UL-->
## Alumno:
---
* Rodrigo Omar Escobar

## Proyecto Sistema de Incendio con Arduino
---
![imagen del proyecyo](proyecto.png "proyecto hecho en tinkercad")
![diagrama del proyecyo](diagrama.png "diagrama hecho en tinkercad")
## Descripcion
---
El proyecto es un sistema de incendio, posee un sensor de temperatura, que va a captar la temperatura en el sector ubicado, un sensor IR (infrarrojo) que va a capturar las señales del control remoto IR, un servo motor que va a ser usado para simular una respuesta en caso de un incendio, una pantalla LCD 16 x 2, que nos a indicar todo lo que esta pasando en el sistema (temperatura actual, rangos de temp. segun la estacion del año, si el sistema esta encendido o apagado y tambien cuando se detecta el incendio), por ultimo se instalaron 2 led, uno verde que indica que el sistema esta encendido y otro rojo que se enciendo cuando el sistema esta apagado.
## Funcion principal
---
La funcion principal es el uso del control ir, ya que permite elegir la configuracion del sistema,
los botones que se usan son: el de encendido, el 1,2,3,4 y el boton play, este ultimo va actuar como boton de enmergencia, en caso de que el sensor de temperatura esta dañado o no detecta el incendio por "X" motivo, este boton enciende el sistema de riego (en este caso los servomotores), los botonos del 1 al 4 son para a seleccionar la estacion del año, donde cada estacion tiene un limite de temperatura diferente
<!-- Bloque de codigos -->
```c++
void usar_control () // Funcion de los botones del control ir
{
    incendio(); // Funcion de incendio
  	encender_led (led_verde, HIGH); // Led verde encendido

    switch (lectura_control)
    {
      case boton_power: // Boton de encendido / estado 0
      lcd.setCursor(0, 0);
      lcd.print("Elija estacion");
      lcd.setCursor(0,1);
      lcd.print("Precione 1,2,3,4     ");
      estadoIncendio = false;
      myservo.write(90);
      break;
      case boton_1: // Boton 1 = Estacion Verano
      if (temperatura > TempMaxVerano)
      {
        estadoIncendio = true;
      }
      else
      {
        lcd.setCursor (5,0);
        lcd.print(" Verano          ");
        lcd.setCursor (14,2);
        lcd.print(TempMaxVerano);
        estadoIncendio = false;
      }
      break;
      case boton_2: // Boton 2 = Estacion Otonio
      if (temperatura > TempMaxOtonio)
      {
      	estadoIncendio = true;
      }
      else
      {
        lcd.setCursor (5,0);
        lcd.print(" Otonio          ");
        lcd.setCursor (14,2);
        lcd.print(TempMaxOtonio);
        estadoIncendio = false;
      }
      break;
      case boton_3: // Boton 3 = Estacion Invierno
      if (temperatura > TempMaxInvierno)
      {
        estadoIncendio = true;
      }
      else
      {
        lcd.setCursor (5,0);
        lcd.print(" Invierno          ");
        lcd.setCursor (14,2);
        lcd.print(TempMaxInvierno);
        estadoIncendio = false;
      }
      break;
      case boton_4: // Boton 4 = Estacion Primavera
      if (temperatura > TempMaxPrimavera)
      {
        estadoIncendio = true;
      }
      else
      {
        lcd.setCursor (5,0);
        lcd.print(" Primavera          ");
        lcd.setCursor (14,2);
        lcd.print(TempMaxPrimavera);
        estadoIncendio = false;
      }
      break;
      case boton_play: // Boton play / es un boton de emergencia en caso que el sensor no funcione
      if (receptorIR.decode())
      {
        if (estadoIncendio == false) // Activa la funcion incendio solo si esta apagado
        {
        estadoIncendio = true;
        }
        else // En caso de volver apretar el boton se reinicia el sistema
        {
          estadoIncendio = false;
          lectura_control = boton_power; // Estado 0, vuelve a preguntar que estacion elegir
          myservo.write(90);
        }
        break;
      }
    receptorIR.resume();  // Reinicia el receptor ir y espera otra señal    
  } 
}
```

## Link del proyecto de tinkercad
---
* [Tinkercad](https://www.tinkercad.com/things/dBL6WebkRg6)

## Link del GBD
---
* [GDB](https://onlinegdb.com/al2YG95kS)

## Link del video funcionando
---
* [Youtube](https://youtu.be/DSy8zLC1euA)

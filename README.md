# iSemáforo
El trabajo trata de dos semáforos, uno para vehículos y otro para peatones. El primero está en verde de forma continua hasta que algún peatón pulse el botón para poder cruzar. En este momento el semáforo de los coches se pone en ámbar y a continuación en rojo. En este instante el semáforo de los peatones se pone en verde y se activa un panel mostrando una cuenta atrás del tiempo que falta para ponerse en rojo otra vez, a la vez que suena una alarma indicando que se puede cruzar.
El semáforo de los automóviles contará con un sensor de velocidad (a una cierta distancia), si se supera dicha velocidad máxima provoca que el semáforo se ponga en rojo hasta que el vehículo no se detenga, una vez detenido, el semáforo se pone en verde.

## Integrantes del equipo
Guillermo Martín Lechuga 54727
Noelia López Rúa 54705

## Objetivos del trabajo
Simular un cruce de una carretera con control de velocidad y semáforos.
Programar en Arduino y estabecer una comunicación con C.

## Lista de componentes
Cables macho y hembra,
resistencias,
leds de diferentes colores,
Active buzzer (la alarma),
pulsadores,
Sensor ultrasonido,
pantalla LCD display,
7 segment display,
Arduino 1 y
2 protoboards

## Sensores y Actuadores
Sensor de Ultrasonidos:
  Sería usado como un radar de velocidad.
  El sensor funcionará de la siguiente manera:
    1º El sensor emitirá un pulso de alta freciencia.
    2º Este pulso rebota en los objetos cercanos y es reflejado hacia el sensor.
    3º Midiendo el tiempo entre pulsos y conociendo la velocidad del sonido podemos estimar la distancia del objeto.
    4º Este proceso se repetirá varias veces para hacer una estimación de la velicidad del objeto.
  
  La velocidad del objeto se calculará de la sigueinte forma:
    1º Se realizarán 2 mediciones para calcular la distancia recorrida en un intervalo de tiempo.
    2º Se calculará la velocidad con la fórmula: v=d/t.
    
  En el caso de que el objeto llever una velocidad superior a la permitida el semáforo para los coches se pondrá en rojo hasta que el vehículo de detenga.

Pulsadores:
  Se usarán 2 pulsadores, uno a cada lado del paso de cebra. Estos serán utilizados para que el semáforo se ponga en rojo para  los coches y en verde para los peatones. 
  Funcionamiento de los pulsadores:
    1º Se acciona uno de los pulsadores.
    2º En el semáforo de los coches se apaga el led verde y se enciende durante unos segundos el led ambar.
    3º Se apaga el led ambar y se enciende el led rojo.
    4º En los semáforos de los peatones se apaga el led rojo y se enciende el verde.
    5º El led verde (peatones) y rojo (coches) estarán encendidos durante 30 segundos. Durante este tiempo un zumbador reproducirá un sonido para que la gente con diversidad funcional sepa que puede cruzar.
    6º En el semáforo de los coches se apagará el led verde y se encenderá el led verde, y en los d elos peatones se apagarán los verdes y se encenderán los rojos.

Zumbador:
  Este elemento reproducirá un sonido para indicar a la gente con diversidad funcional que puede cruzar.

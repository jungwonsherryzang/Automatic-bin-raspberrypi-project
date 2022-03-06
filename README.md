# Automatic-bin-raspberrypi-project
Developing an automatic bin with Raspberry Pi


Trash can is the necessary thing in our life, but there are innumerable germs in trash can itself. 
Therefore, it is necessary to consider how to avoid contacting with those germs and keep ourselves safe and clean.

## MATERIALS
-Raspberry Pi3 Board

-Servo Motor

-Ultrasonic Sensor

-Trash can

## PROCESS
1. Install the Raspbian into the Raspberry Pi3 Board
2. Connect the bread board and the ultrasonic sencor using with resistance 1K and 2K.

 -Ultrasonic Echo pin can't hold the 5V, which means that it can be burned.
 
 -It is important to give the resistance and drop the volt
 
3. Write the Ultrasonic code
``` python
import RPi.GPIO as GPIO
import time
GPIO.setmode(GPIO.BCM)

TRIG = 23
ECHO = 24

print "Distance Measurement In Progress"

GPIO.setup(TRIG,GPIO.OUT)
GPIO.setup(ECHO,GPIO.IN)

GPIO.output(TRIG, False)
print "Waiting For Sensor To Settle"
time.sleep(2)

GPIO.output(TRIG, True)
time.sleep(0.00001)
GPIO.output(TRIG, False)

while GPIO.input(ECHO)==0:
	pulse_start = time.time()

while GPIO.input(ECHO)==1:
        pulse_end = time.time()
        
pulse_duration = pulse_end - pulse_start

distance = pulse_duration * 17150

distance = round(distance, 2)

print "Distance:", distance,"cm"

GPIO.cleanup()
```
4. Write the Servo Motor code and connect it
``` python
import RPi.GPIO as GPIO
import time

pin = 18 # PWM pin num 18

GPIO.setmode (GPIO.BCM)
GPIO.setup(pin, GPIO.OUT)
p = GPIO.PWM(pin, 50)
p.start (0)
cnt = 0
try:
    while True:
        p.ChangeDutyCycle(1)
        print "angle : 0"
        time.sleep(1)
        p.ChangeDutyCycle(8)
        print "angle : -360"
        time.sleep(1)
except KeyboardInterrupt:
    p.stop ()
GPIO.cleanup ()
```
5. After connecting successfully, make a combined code for both Servo motor and Ultrasonic code
6. Put the Ultrasonic in front of the trash can
7. Fix the bread board inside the bin
8. Make a mini basket for Raspberry Pi3 board and put it in
9. Finish!

![image info](./final picture.jpg)

